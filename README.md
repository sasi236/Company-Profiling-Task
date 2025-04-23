# CluedIn Final Task – Company Validation and Enrichment via Companies House API

## Overview

This solution is built to validate, enrich, and profile UK company data using the Companies House API. It handles real-world scenarios such as messy input data, potential duplicates, and unmatched records, while providing clean, visual insights into the results of company matching.

Implemented in Python (Jupyter Notebook), the solution processes input data, performs hybrid company name matching via the Companies House API, enriches the dataset with key company attributes, and generates visual summaries to highlight match status and data distribution.

The full implementation can be found in the Jupyter Notebook: Company_Matching_Solution.ipynb

---

## Features & Workflow

### 1. Configuration-Driven Execution
- Uses a `Configuration.csv` file to manage input/output paths, batch size, API key, and other settings.
- Makes the pipeline adaptable without changing the code.

### 2. Data Preparation
- Reads input company data (`input_file`) from a CSV.
- Cleans column names, trims spaces, and standardizes company names.
- Handles missing or blank `CompanyNumber` values.
- Deduplicates records based on `CompanyName` and `PostCode`.

### 3. Hybrid Matching Logic
- For each company:
  - Sends a query to the Companies House API.
  - Checks for exact match via `CompanyNumber`.
  - Falls back to name-based matching using fuzzy logic.
- Captures:
  - Match status (`Exact match`, `Name match only`, `No match`)
  - Confidence score
  - Company status, number, and address.

### 4. Batch Processing
- Processes data in configurable batches with delay (`api_delay`) to respect API rate limits.

### 5. Result Structuring
- Final dataset includes enriched fields:
  - `Matched`, `MatchStatus`, `MatchedCompanyNumber`, `CompanyStatus`, etc.
- Saves unmatched and duplicate records separately.

### 6. Visual Analytics
- Generates and saves:
  - Bar Chart: Breakdown of match statuses
  - Pie Chart: Match status distribution
- Charts are saved to the output directory defined in config.

---

## Output Files

- `enriched_companies_output.csv`: Final enriched dataset with match details
- `duplicate_records.csv`: All identified duplicate records
- `unmatched_records.csv`: Records that didn’t match any API results
- `company_match_bar_chart.png`: Bar chart of match status
- `company_match_pie_chart.png`: Pie chart of match status

---

## Tech Stack

- Python 3
- pandas, requests, tqdm
- matplotlib, seaborn
- Companies House API

---

## How to Run

1. Ensure your `Configuration.csv` has all required paths and keys.
2. Place the input CSV (`input_file`) in the specified path.
3. Run the notebook or script.
4. Check the output directory for results and visuals.

---

## Execution

- The script tracks and logs total runtime.
- Handles exceptions and shows status updates for batches.

## Notes
I have used the following references to learn Python and the associated tech stack used in this solution:

- Python Programming: Python Official Documentation for mastering Python basics and advanced concepts: https://docs.python.org/3/

- Data Manipulation with Pandas and NumPy: Pandas Documentation and NumPy Documentation for efficient data processing and handling.
  https://pandas.pydata.org/pandas-docs/stable/

- Data Visualization: Matplotlib Documentation and Seaborn Documentation for creating insightful data visualizations.
  https://matplotlib.org/stable/index.html