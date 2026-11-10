# Data Cleaning with Python

## Project Overview

In this project, I worked on cleaning a messy dataset and preparing it for further analysis. I used the Titanic dataset from Kaggle to get hands-on experience with Python and practise different data cleaning techniques.

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

I followed these steps to clean the dataset and improve its overall quality:

1. **Data Quality Report:** Checked missing values, duplicate records, data types, and unusual values to understand the condition of the original dataset.

2. **Missing Values:** Used median imputation for Age and Fare, mode imputation for Embarked, and removed Cabin because it contained too many missing values.

3. **Duplicate Removal:** Identified and removed duplicate rows to avoid unnecessary repetition in the dataset.

4. **Standardisation:** Standardised gender values and removed unnecessary spaces from text columns to make the data more consistent.

5. **Outlier Detection:** Used the IQR method to identify outliers in Age and Fare. Genuine outliers were retained to avoid losing potentially useful information.

6. **Data Type Correction:** Converted passenger IDs and text columns to string and corrected numerical column types where needed.

7. **Data Validation:** Checked the dataset again after cleaning to make sure missing values, duplicates, and invalid values were handled properly.

8. **Before vs. After Comparison:** Compared missing values, duplicate records, row counts, and data type accuracy to understand the improvements made during the cleaning process.

## Project Files

| File | Description |
|---|---|
| `train.csv` | Original Titanic dataset |
| `Task_3_Data_Cleaning.ipynb` | Notebook containing the complete cleaning process and Python code |
| `titanic_cleaned.csv` | Final cleaned dataset |

## Final Output

After completing the cleaning process, I saved the cleaned dataset as `titanic_cleaned.csv`.

The final dataset is more organised and consistent, with missing values handled, duplicate records removed, and data types corrected. It is now ready for further data analysis.

## What I Learned

Through this project, I gained practical experience in:

- Working with real-world datasets.
- Identifying and handling data quality issues.
- Using Pandas and NumPy for data cleaning.
- Understanding different methods of handling missing values.
- Detecting outliers using the IQR method.
- Comparing data quality before and after cleaning.

This project helped me understand that data cleaning is an important part of data analysis. Before finding insights or performing any analysis, it is important to make sure the data is clean, consistent, and reliable.

It was a great hands-on learning experience, and I look forward to applying these skills in more data analytics projects.
