# SQL-Data-Cleaning-Layoffs

This project focuses on cleaning and standardising a real-world dataset of tech layoffs using SQL. The goal is to prepare the data for accurate analysis by identifying and removing duplicates, fixing formatting issues, handling null values, and standardising inconsistent entries.

📦 Dataset: layoffs
The raw dataset includes company-level layoff data, such as:

- Company name

- Location and country

- Industry

- Total laid off and percentage

- Stage and funding raised

- Layoff date

📋 Cleaning Steps
✅ Step 1: Remove Duplicates

- Used ROW_NUMBER() with PARTITION BY to identify duplicate rows based on key fields

- Deleted duplicate entries from a staging table

- Created new clean tables (layoffs_staging, layoffs_staging2) for safe transformations

✅ Step 2: Standardise Formatting

- Trimmed extra spaces from text fields (company, etc.)

- Unified inconsistent naming (e.g., "Crypto - Blockchain" → "Crypto", "United States of America" → "United States")

- Converted date from TEXT to proper DATE format using STR_TO_DATE()

✅ Step 3: Handle Missing or Null Values

- Identified rows where total_laid_off and percentage_laid_off were null

- Imputed missing industry values by joining on company name

- Removed rows with no useful data after imputation

✅ Step 4: Final Cleanup

- Deleted completely empty rows (no layoffs data)

- Dropped temporary columns (e.g., row_num) used for processing

🧠 Key Skills Demonstrated

- Advanced SQL: CTEs, window functions, joins, conditional updates

- Data profiling and cleansing logic

- Schema management and data staging best practices

- Preparing raw datasets for business analysis

Data cleaning logic suitable for ETL pipelines or analytics staging layers

🧪 Example Queries
sql
Copy
Edit
-- Remove leading/trailing spaces from company names
UPDATE layoffs_staging2
SET company = TRIM(company);

-- Convert date from string to date format
UPDATE layoffs_staging2
SET `date` = STR_TO_DATE(`date`, '%m/%d/%Y');
