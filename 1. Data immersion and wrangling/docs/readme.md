# 1. Data Quality Asessment
**Dataset: Retail Store Sales**

The objective of this step is to perform an initial profiling of the dataset to identify critical data quality issues such as missing values, duplicate records, inconsistent formatting, and outliers before proceeding to data cleaning and transformation.

## 1.1 Dataset overview:
-> Total records: 12,575

-> Total columns: 11

-> Data types:

     8 object (categorical / text)

     3 numeric (float64)

-> Each row represents a single retail transaction.

## 1.2 Missing Values:
Based on non-null counts, the following missing values were identified:

| Column Name      | Total Records | Non-Null | Missing |
| ---------------- | ------------- | -------- | ------- |
| Item             | 12,575        | 11,362   | 1,213   |
| Price Per Unit   | 12,575        | 11,966   | 609     |
| Quantity         | 12,575        | 11,971   | 604     |
| Total Spent      | 12,575        | 11,971   | 604     |
| Discount Applied | 12,575        | 8,376    | 4,199   |
     
-> Findings:

    Discount Applied has a significant number of missing values.

    Pricing and quantity-related columns contain missing values, which can impact revenue calculations.

    Item contains missing entries, which affects item-level analysis.
    
  ## 1.3 Duplicate records:
-> All rows contain non-null Transaction ID values.

-> Duplicate checks will be performed using Transaction ID.

-> Initial assumption:
    Each transaction is unique; however, explicit duplicate checks are required to confirm.

-> Findings:
    The dataset contains no duplicate records. This was confirmed using the df.duplicated() function in Pandas.
 
##  1.4 Data type consistency
-> Findings:

    1. Transaction Date is stored as object, but should be converted to datetime.

    2. Quantity is stored as float64, but should ideally be integer.

    3. Discount Applied is categorical but contains missing values and may require standardization (Yes/No).
    
    4.Categorical columns (Category, Payment Method, Location, Discount Applied) may contain inconsistent casing or spacing.

    5. Standardization is required to avoid duplicate categories during analysis.

## 1.5 Logical Consistency
-> Potential business rule validations:
    
    Total Spent should equal Price Per Unit × Quantity
    
    Transactions with missing Price Per Unit or Quantity may result in incorrect Total Spent.

-> Findings:
    
    Dataset contains of 1213 rows where Total Spent is not equal to Price Per Unit × Quantity

<br>
<br>

# 2. Data Cleaning & Transformation
The objective of this step is to clean and prepare the dataset by addressing the data quality issues identified in Step 2. This ensures the data is accurate, consistent, and ready for analysis.

## 2.1 Handling Missing Values

-> Actions Taken:
    
    Rows with missing values in critical numeric columns (Price Per Unit, Quantity) were removed.

    Missing values in Discount Applied were filled with "No", assuming no discount when not specified.

    Rows with missing Item names were removed as item-level analysis would be affected.

Code:
#####  Remove rows with missing critical numeric values
    df = df.dropna(subset=['Price Per Unit', 'Quantity'])

 ##### Fill missing discount values with 'No'
    df['Discount Applied'] = df['Discount Applied'].fillna(False)

 ##### Remove rows with missing item names
    df = df.dropna(subset=['Item'])

## 2.2 Data Type Conversion
-> Actions Taken:

    Converted Transaction Date from object to datetime format.

    Converted Quantity from float to integer after cleaning.

Code:
 #####  ~ Convert Transaction Date to datetime
    df['Transaction Date'] = pd.to_datetime(df['Transaction Date'], errors='coerce')

######  Convert Quantity to integer
    df['Quantity'] = df['Quantity'].astype(int)

## 2.3 Standardizing Categorical Values
-> Actions Taken:

    Standardized categorical text fields by trimming spaces and applying consistent casing.

    Ensured Discount Applied contains only "True" or "False" values.

-> Code:
    
    categorical_cols = ['Category', 'Payment Method', 'Location', 'Discount Applied']

    for col in categorical_cols:
        df[col] = df[col].astype(str).str.strip().str.title()`
    
    
    df['Discount Applied']=df['Discount Applied'].replace({'True':'Yes' , 'False':'No'})

## 2.4 Logical Consistency Validation

->Actions Taken:

Validated that Total Spent equals Price Per Unit × Quantity.

Recalculated Total Spent where discrepancies were found.

->Code:
    df['Total Spent'] = df['Price Per Unit'] * df['Quantity']

## 2.5 Final Validation

-> Actions Taken:

    Verified absence of missing values in critical columns.

    Confirmed correct data types and logical consistency.

-> Code:
    df.info()
    df.isnull().sum()