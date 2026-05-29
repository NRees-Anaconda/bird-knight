---
name: analyze-data
description: Analyze CSV, JSON, or tabular data files to produce summary statistics, data quality assessments, and actionable insights. Covers numeric distributions, categorical frequencies, missing values, outliers, and correlations.
---

# Data Analyzer

Analyze the data file provided by the user.

## Supported Formats
- CSV / TSV files
- JSON (array of objects or newline-delimited)
- Parquet (if pandas is available)

## Analysis Steps

### 1. Schema Overview
- Column names and inferred types (numeric, categorical, datetime, boolean, text)
- First 3 sample values per column
- Total row/record count

### 2. Numeric Columns
For each numeric column, compute:
- Min, Max, Mean, Median
- Standard deviation
- Null/missing count and percentage
- Distribution shape (note obvious skew or outliers)

Use Python one-liners via shell if pandas is available:
```bash
python3 -c "import pandas as pd; df = pd.read_csv('file.csv'); print(df.describe())"
```

Fall back to reading the file and computing manually if pandas is not available.

### 3. Categorical Columns
For each categorical column:
- Unique value count
- Top 5 values by frequency (with counts and percentages)
- Null/missing count

### 4. Data Quality Assessment
- **Missing values** — columns with >5% nulls flagged
- **Duplicates** — exact duplicate rows
- **Outliers** — values beyond 3 standard deviations in numeric columns
- **Inconsistencies** — mixed formats (e.g., dates as "2024-01-01" and "Jan 1, 2024"), mixed case in categories, leading/trailing whitespace
- **Cardinality issues** — "categorical" columns with nearly unique values (possible IDs)

### 5. Relationships (if multiple numeric columns exist)
- Note any obvious correlations (positive or negative)
- Flag columns that appear to be derived from others

## Output Format

Present as a clean data profile report with sections. End with:

**Suggested next steps:**
- Visualizations that would be useful (histograms, scatter plots, etc.)
- Potential data cleaning actions
- Questions the data might answer
