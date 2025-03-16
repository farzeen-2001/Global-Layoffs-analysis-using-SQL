# Global-Layoffs-analysis-using-SQL
World Layoffs Data Cleaning and Analysis using SQL

Overview

This project focuses on cleaning, transforming, and analyzing a dataset containing global layoff data. The dataset is processed using MySQL, and various SQL techniques are applied to remove duplicates, standardize data, and extract insights.

Steps Involved

1. Creating a Staging Table

To ensure the raw data remains unaffected, a staging table (layoffs_staging) is created as a duplicate of the original layoffs table:

CREATE TABLE layoffs_staging LIKE layoffs;
INSERT INTO layoffs_staging SELECT * FROM layoffs;

2. Removing Duplicates

Duplicates are identified using ROW_NUMBER() with PARTITION BY, and a new table (layoffs_staging2) is created to store the cleaned data:

WITH duplicate_cte AS (
    SELECT *,
           ROW_NUMBER() OVER(PARTITION BY country, location, industry, total_laid_off, percentage_laid_off, `date`, stage, funds_raised_millions) AS row_num
    FROM layoffs_staging
)
SELECT * FROM duplicate_cte WHERE row_num > 1;

After identifying duplicates, they are removed:

DELETE FROM layoffs_staging2 WHERE row_num > 1;

3. Standardizing Data

Removing spaces using TRIM():

UPDATE layoffs_staging2 SET company = TRIM(company);

Standardizing industry names 
(e.g., replacing "Cryptocurrency" with "Crypto"):

UPDATE layoffs_staging2 SET industry = 'Crypto' WHERE industry LIKE 'Crypto%';

Cleaning country names 
(e.g., removing trailing periods from "United States."):

UPDATE layoffs_staging2 SET country = TRIM(TRAILING '.' FROM country) WHERE country LIKE 'United States%';

4. Converting Date Format

The date column is stored as text and converted to a proper DATE format:

UPDATE layoffs_staging2 SET `date` = STR_TO_DATE(`date`, '%m/%d/%Y');
ALTER TABLE layoffs_staging2 MODIFY COLUMN `date` DATE;

5. Handling Null and Blank Values

Identifying and updating missing industry values:

UPDATE layoffs_staging2 t1
JOIN layoffs_staging2 t2 ON t1.company = t2.company
SET t1.industry = t2.industry
WHERE t1.industry IS NULL AND t2.industry IS NOT NULL;

Removing rows with null values in key columns:

DELETE FROM layoffs_staging2 WHERE total_laid_off IS NULL AND percentage_laid_off IS NULL;



