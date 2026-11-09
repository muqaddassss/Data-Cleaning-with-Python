# Task 3 – Data Cleaning with Python

## Project Overview

This project focuses on cleaning a messy dataset and preparing it for further analysis. I used the Titanic dataset from Kaggle to practise data cleaning techniques using Python.

The main goal was to identify data quality issues, handle missing values, remove duplicates, standardise inconsistent values, detect outliers, and correct data types.

## Dataset

- **Dataset:** Titanic Dataset
- **Source:** [Kaggle – Titanic Dataset](https://www.kaggle.com/competitions/titanic/data)
- **File:** `train.csv`

## Tools & Technologies

- Python
- Pandas
- NumPy
- Google Colab / Jupyter Notebook

## Data Cleaning Steps

I performed the following steps to clean the dataset:

1. **Data Quality Report:** Checked missing values, duplicate records, data types, and unusual values.
2. **Missing Values:** Used median imputation for Age and Fare, mode imputation for Embarked, and removed Cabin because it contained too many missing values.
3. **Duplicate Removal:** Identified and removed duplicate rows.
4. **Standardisation:** Standardised gender values and removed unnecessary spaces from text columns.
5. **Outlier Detection:** Used the IQR method to identify outliers in Age and Fare. Retained genuine outliers to avoid losing useful information.
6. **Data Type Correction:** Converted passenger IDs and text columns to string and corrected numerical column types.
7. **Data Validation:** Checked the dataset again after cleaning.
8. **Before vs. After Comparison:** Compared missing values, duplicate records, row counts, and data type accuracy.

## Project Files

| File | Description |
|---|---|
| `train.csv` | Original Titanic dataset |
| `Task_3_Data_Cleaning.ipynb` | Notebook containing the complete cleaning process |
| `titanic_cleaned.csv` | Final cleaned dataset |

## Python Code

The complete Python code used for this project is included below.

### 1. Import Libraries and Load Dataset

```python
import pandas as pd
import numpy as np

# Load the dataset
df = pd.read_csv("train.csv")

# Display the first five rows
df.head()
```

### 2. Data Quality Report

```python
# Check dataset information
df.info()

# Create a data quality report
quality_report = pd.DataFrame({
    "Missing Values": df.isnull().sum(),
    "Data Types": df.dtypes,
    "Unique Values": df.nunique()
})

# Display duplicate rows
print("Duplicate Rows:", df.duplicated().sum())

quality_report
```

```python
# Check numeric values and their ranges
df.describe()
```

```python
# Check unusual values
print("Negative Ages:", (df["Age"] < 0).sum())
print("Negative Fares:", (df["Fare"] < 0).sum())

print("Invalid Passenger Classes:",
      (~df["Pclass"].isin([1, 2, 3])).sum())

print("Invalid Survival Values:",
      (~df["Survived"].isin([0, 1])).sum())
```

### 3. Store Original Dataset Information

```python
# Save original dataset statistics for comparison
before_rows = len(df)
before_nulls = df.isnull().sum().sum()
before_duplicates = df.duplicated().sum()
before_dtypes = df.dtypes.copy()
```

### 4. Handle Missing Values

```python
# Fill missing numerical values
df["Age"] = df["Age"].fillna(df["Age"].median())
df["Fare"] = df["Fare"].fillna(df["Fare"].median())

# Fill missing categorical values
df["Embarked"] = df["Embarked"].fillna(
    df["Embarked"].mode()[0]
)

# Remove Cabin because it has too many missing values
df.drop(columns=["Cabin"], inplace=True)

# Check remaining missing values
df.isnull().sum()
```

### 5. Remove Duplicate Rows

```python
# Count duplicates before removing them
duplicates_before = df.duplicated().sum()

# Remove duplicate records
df.drop_duplicates(inplace=True)

# Check how many duplicates were removed
print("Duplicates Removed:", duplicates_before)
print("Remaining Duplicates:", df.duplicated().sum())
```

### 6. Standardisation

```python
# Standardise gender values
df["Sex"] = df["Sex"].astype("string").str.strip().str.lower()

df["Sex"] = df["Sex"].replace({
    "male": "Male",
    "female": "Female",
    "m": "Male",
    "f": "Female"
})

# Standardise Embarked values
df["Embarked"] = df["Embarked"].astype("string").str.strip().str.upper()

# Remove unnecessary spaces from text columns
for col in ["Name", "Ticket"]:
    df[col] = df[col].astype("string").str.strip()

# Check standardised values
print(df["Sex"].unique())
print(df["Embarked"].unique())
```

### 7. Outlier Detection Using IQR

```python
# Identify outliers using the IQR method
numeric_columns = ["Age", "Fare"]

outlier_counts = {}

for col in numeric_columns:

    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)

    IQR = Q3 - Q1

    lower_limit = Q1 - 1.5 * IQR
    upper_limit = Q3 + 1.5 * IQR

    outliers = df[
        (df[col] < lower_limit) |
        (df[col] > upper_limit)
    ]

    outlier_counts[col] = len(outliers)

    print(f"\n{col} Outliers:", len(outliers))
    print("Lower Limit:", lower_limit)
    print("Upper Limit:", upper_limit)

# Display outlier counts
outlier_counts
```

### 8. Data Type Correction

```python
# Convert passenger ID into string
df["PassengerId"] = df["PassengerId"].astype("string")

# Convert text columns into string
for col in ["Name", "Sex", "Ticket", "Embarked"]:
    df[col] = df[col].astype("string")

# Convert numerical columns into appropriate types
df["Survived"] = df["Survived"].astype("int64")
df["Pclass"] = df["Pclass"].astype("int64")
df["Age"] = pd.to_numeric(df["Age"])
df["SibSp"] = df["SibSp"].astype("int64")
df["Parch"] = df["Parch"].astype("int64")
df["Fare"] = pd.to_numeric(df["Fare"])

# Check corrected data types
df.dtypes
```

### 9. Final Data Validation

```python
# Check missing values
print("Missing Values:", df.isnull().sum().sum())

# Check duplicates
print("Duplicate Rows:", df.duplicated().sum())

# Check final row count
print("Total Rows:", len(df))

# Check invalid values
print("Negative Ages:", (df["Age"] < 0).sum())
print("Negative Fares:", (df["Fare"] < 0).sum())
```

### 10. Before vs. After Comparison

```python
# Define expected data types
expected_dtypes = {
    "PassengerId": "string",
    "Survived": "int",
    "Pclass": "int",
    "Name": "string",
    "Sex": "string",
    "Age": "float",
    "SibSp": "int",
    "Parch": "int",
    "Ticket": "string",
    "Fare": "float",
    "Embarked": "string"
}

# Check data type accuracy
def dtype_accuracy(data_types, expected):

    correct = 0

    for col, dtype in expected.items():

        actual = data_types[col]

        if dtype == "string" and str(actual) == "string":
            correct += 1

        elif dtype == "int" and pd.api.types.is_integer_dtype(actual):
            correct += 1

        elif dtype == "float" and pd.api.types.is_float_dtype(actual):
            correct += 1

    return round((correct / len(expected)) * 100, 2)


# Calculate original and cleaned data type accuracy
before_accuracy = dtype_accuracy(before_dtypes, expected_dtypes)
after_accuracy = dtype_accuracy(df.dtypes, expected_dtypes)

# Create comparison table
comparison = pd.DataFrame({
    "Before Cleaning": [
        before_rows,
        before_nulls,
        before_duplicates,
        f"{before_accuracy}%"
    ],

    "After Cleaning": [
        len(df),
        df.isnull().sum().sum(),
        df.duplicated().sum(),
        f"{after_accuracy}%"
    ]

}, index=[
    "Total Rows",
    "Null Values",
    "Duplicate Rows",
    "Data Type Accuracy"
])

comparison
```

### 11. Save Cleaned Dataset

```python
# Save the cleaned dataset as a new CSV file
df.to_csv("titanic_cleaned.csv", index=False)

print("Cleaned dataset saved successfully!")

# Load and verify the cleaned file
cleaned_df = pd.read_csv("titanic_cleaned.csv")

cleaned_df.head()
```

## Final Output

After completing the cleaning process, I saved the cleaned dataset as `titanic_cleaned.csv`.

The final dataset is more organised and consistent, with missing values handled, duplicate records removed, and data types corrected. It is now ready for further data analysis.

## What I Learned

Through this project, I gained practical experience in:

- Working with real-world datasets.
- Identifying and handling data quality issues.
- Using Pandas and NumPy for data cleaning.
- Understanding different missing value treatment methods.
- Detecting outliers using the IQR method.
- Comparing data quality before and after cleaning.

This project helped me understand that data cleaning is an important part of data analysis because good analysis starts with good-quality data.
