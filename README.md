# Task 3 – Data Cleaning with Python

## Project Overview

This project focuses on cleaning a messy dataset and preparing it for further analysis. I used the Titanic dataset from Kaggle to practice data cleaning techniques using Python.

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
| `Task_3_Data_Cleaning.ipynb` | Jupyter Notebook containing the complete cleaning process |
| `titanic_cleaned.csv` | Final cleaned dataset |

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
