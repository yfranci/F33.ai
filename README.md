
# Cleanup HubSpot Data Script

This script contains a series of operations and transformations on data sourced from HubSpot.

## Dependencies and Initial Configuration
- The script utilizes the following Python libraries:
  - pandas
  - sqlite3
  - requests
  - io
- The script originated from a Jupyter notebook hosted on Google Colaboratory.

## Main Processes and Functionality

### 1. Reading Data from Google Drive
- A helper function named `read_csv_from_gdrive()` fetches CSV content from Google Drive and returns it as a pandas DataFrame.

### 2. Comparing Two Columns: "SOW ID" and "SOW #"
- Identifies discrepancies between the `SOW ID` and `SOW #` columns.
- Stores these discrepancies along with their row numbers in a separate DataFrame.

### 3. Storing Discrepancies in an SQLite Database
- Discrepancies are stored in an SQLite database named `discrepancies.db` in a table called `Discrepancies`.

### 4. Data Cleanup
- A new DataFrame is created with the columns `Deal Name` and `SOW #`.
- Another dataset, the DealID Sheet, is fetched, cleaned, and combined with the main dataset.
  - Duplicate rows are removed.
  - Missing values are filled with the string "Unknown".
  - Text data is standardized: converted to uppercase and white spaces are trimmed.
  - Rows with `SOW` values exceeding 10 characters are removed.

### 5. Resolving Discrepancies
- A boolean `Discrepancy` column is added to the main DataFrame to indicate discrepancies between the `SOW ID` and `SOW #` columns.
- Rows with discrepancies have their `SOW ID` values overwritten with `SOW #` values.
- The script also filters out rows where the `SOW` format doesn't match the expected pattern (4 digits, a hyphen, then 3 digits).

## Objective
The main goal of the script is data cleaning and normalization, particularly concerning the `SOW ID` and `SOW #` columns. Discrepancies between these columns are highlighted, stored, and subsequently resolved. The script also integrates data from different sources, ensuring it's cleaned and standardized.
