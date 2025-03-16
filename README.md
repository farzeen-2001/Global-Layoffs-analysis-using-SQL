# Global-Layoffs-analysis-using-SQL
World Layoffs Data Cleaning and Analysis using SQL

Overview

This project focuses on cleaning, transforming, and analyzing a dataset containing global layoff data. The dataset is processed using MySQL, and various SQL techniques are applied to remove duplicates, standardize data, and extract insights.

Steps Involved:

* DATA CLEANING:

1. Creating a Staging Table

2. Removing Duplicates
Duplicates are identified using ROW_NUMBER() with PARTITION BY, and a new table (layoffs_staging2) is created to store the cleaned data
After identifying duplicates, they are removed

3. Standardizing Data
Removing spaces using TRIM()
Standardizing industry names 

4. Converting Date Format
The date column is stored as text and converted to a proper DATE format

5. Handling Null and Blank Values
Identifying and updating missing industry values
Removing rows with null values in key columns

* EXPLORATORY DATA ANALYSIS
  -Key insights
  1. maximum layoffs and percentage laid off
  2. companies with highes layoffs
  3. layoffs by industry,country and stage
  4. layoffs per year
  5. rolling total layoffs

* FINDINGS
  1. Amazon has the highest Layoffs
  2. Consumer industry was the most affected industry
  3. US recorded the highest layoffs followed by India and Netherlands
  4. the layoffs started in 2020 and peaked in 2023



