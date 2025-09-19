# Dirty Cafe Sales Dataset: Cleaning and Database Integration

This project demonstrates a complete workflow for cleaning a "dirty" dataset, saving it to a PostgreSQL database, and retrieving it for further analysis. The dataset used is a synthetic cafe sales dataset from Kaggle, intentionally created with missing values, errors, and inconsistencies to simulate a real-world data cleaning scenario.

**Source**: Kaggle  
**Link**: [Download Dataset](https://www.kaggle.com/datasets/ahmedmohamed2003/cafe-sales-dirty-data-for-cleaning-training)

---

## Project Goals

The main objectives of this project were:
1.  **Clean the Dataset**: Address inconsistencies, errors, and missing values to prepare the data for analysis.
2.  **Database Storage**: Save the cleaned data into a local PostgreSQL database.
3.  **Data Retrieval**: Retrieve the data from the database back into a pandas DataFrame.

---

## Data Cleaning Process

The initial dataset contained 10,000 rows and 8 columns with various issues. The following steps were taken to clean the data:

### 1. Data Type Conversion
The data types of several columns were incorrect. They were converted as follows:
-   **Numerical Columns**: `Quantity`, `Price Per Unit`, and `Total Spent` were converted to numeric types. Any non-numeric values (e.g., 'ERROR') were coerced into `NaN`.
-   **Date Column**: `Transaction Date` was converted to a pandas datetime object.
-   **Categorical Columns**: Other columns were confirmed as object types.

### 2. Handling Missing & Inconsistent Values
After data type conversion, missing values (`NaN`) and inconsistent entries (`UNKNOWN`, `ERROR`) were handled:
-   **Numerical Columns (`Quantity`, `Price Per Unit`, `Total Spent`)**: Missing values were filled with the **mean** of their respective columns.
-   **Categorical Columns (`Location`, `Payment Method`)**: `NaN` values and `'UNKNOWN'` entries were replaced with the **mode** (the most frequent value) of their respective columns.
-   **Item Column**: Rows with `NaN` values were dropped. `'UNKNOWN'` entries were replaced with the column's **mode**.
-   **Transaction Date Column**: Rows with `NaN` values were dropped to ensure every transaction has a valid date.

### 3. Cleaning Summary
After the cleaning process was complete, **775 rows were dropped**, which accounts for about **7.75%** of the original dataset. The final cleaned dataset contains 9,225 rows with no missing values.

---

## Database Integration with PostgreSQL

**SQLAlchemy** was used to connect to a PostgreSQL database.

-   **Saving Data**: The cleaned pandas DataFrame was saved to a new table named `cafe_sale` in the database using the `to_sql()` function. If the table already existed, it was replaced.
-   **Retrieving Data**: The data was loaded back from the `cafe_sale` table into a new DataFrame using the `read_sql_table()` function to verify the operation.

---

## Getting Started

To run this project on your local machine, follow these steps.

### Prerequisites
-   Python 3.x
-   A running instance of PostgreSQL.

### Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Elthiero/Cafe-Sales---Dirty-Data-for-Cleaning-Training-kaggle.git
    cd Cafe-Sales---Dirty-Data-for-Cleaning-Training-kaggle
    ```
    check if the file "dirty_cafe_sales.csv" exist.

2.  **Install the required Python packages:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Configure the database connection:**
    Create a file named `postgres_config.py` and add your database credentials in the following format:
    ```python
    db_config = {
        'user': 'postgres',      # your username (e.g., postgres)
        'password': 'your_password', # your database password
        'host': 'localhost',     # your database URL (e.g., localhost)
        'port': '5432',          # your database port (e.g., 5432)
        'name': 'db_name'        # your database name (e.g., cafe_db)
    }
    ```

### Running the Notebook
Open and run the `Cafe_Sales.ipynb` notebook in a Jupyter environment (like Jupyter Notebook or VS Code) to see the entire process from cleaning to database interaction.

---

## Dependencies

The project relies on the following libraries, listed in `requirements.txt`:
