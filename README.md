# Medical Insurance Data Analysis 
 
## Overview 
 
This project focuses on exploratory data analysis, data cleaning, preprocessing, feature engineering, data visualization, feature scaling, and statistical analysis of a medical insurance dataset. 
 
The complete analysis is performed using Python in a Jupyter Notebook. 
 
The dataset contains information about individuals including age, sex, BMI, number of children, smoking status, residential region, and medical insurance charges. 
 
--- 
 
## Dataset 
 
The dataset contains **1338 records** and **7 columns** before duplicate removal. 
 
### Features 
 
| Feature | Description | 
|---------|-------------| 
| `age` | Age of the individual | 
| `sex` | Sex of the individual | 
| `bmi` | Body Mass Index | 
| `children` | Number of children/dependents | 
| `smoker` | Smoking status | 
| `region` | Residential region | 
| `charges` | Medical insurance charges | 
 
The target variable considered in the analysis is: 
 
    charges

---

## Data Analysis Workflow

The project follows the following data analysis workflow:

1. Data Loading
2. Exploratory Data Analysis
3. Data Cleaning
4. Data Encoding
5. Feature Engineering
6. Feature Scaling
7. Correlation Analysis
8. Chi-Square Statistical Analysis
9. Final Feature Selection

---

## 1. Data Loading

The dataset is loaded using Pandas:

    import pandas as pd

    df = pd.read_csv('insurance.csv')

The dataset initially contains **1338 rows and 7 columns**.

---

## 2. Exploratory Data Analysis

Several exploratory analysis techniques are performed to understand the dataset.

### Dataset Shape

    df.shape

### First Five Rows

    df.head()

### Dataset Information

    df.info()

### Statistical Summary

    df.describe()

### Missing Values

    df.isnull().sum()

### Column Names

    df.columns

These steps help identify the structure of the dataset, data types, missing values, and basic statistical characteristics.

---

## 3. Correlation Analysis

A correlation heatmap is generated to visualize the relationships between numerical variables.

    plt.figure(figsize=(8,6))
    sns.heatmap(df.corr(numeric_only=True), annot=True)
    plt.show()

The heatmap helps identify the strength and direction of linear relationships among numerical features.

---

## 4. Data Cleaning

A copy of the original dataset is created before performing cleaning operations.

    df_cleaned = df.copy()

Duplicate records are removed using:

    df_cleaned.drop_duplicates(inplace=True)

After duplicate removal, the dataset contains **1337 records**.

---

## 5. Data Encoding

Categorical variables are converted into numerical representations.

### Sex Encoding

The `sex` column is encoded as:

- `male` → `0`
- `female` → `1`

The column is then renamed to:

    is_female

### Smoking Status Encoding

The `smoker` column is encoded as:

- `no` → `0`
- `yes` → `1`

The column is then renamed to:

    is_smoker

### Region Encoding

The `region` column is converted into one-hot encoded variables using:

    pd.get_dummies(
        df_cleaned,
        columns=['region'],
        drop_first=True
    )

The resulting region features include:

- `region_northwest`
- `region_southeast`
- `region_southwest`

---

## 6. BMI Feature Engineering

BMI values are converted into categorical groups.

The BMI categories used in the analysis are:

| BMI Category | Description |
|--------------|-------------|
| Underweight | Low BMI |
| Normal | Normal BMI |
| Overweight | Higher than normal BMI |
| Obese | High BMI |

The categorical BMI feature is used for further statistical analysis.

The resulting encoded features include:

- `bmi_category_Normal`
- `bmi_category_Overweight`
- `bmi_category_Obese`

---

## 7. Feature Scaling

Standardization is applied to selected numerical features using `StandardScaler`.

The features selected for scaling are:

- `age`
- `bmi`
- `children`

The scaling process standardizes these numerical features so that they have a comparable scale.

---

## 8. Pearson Correlation Analysis

Pearson correlation analysis is performed using:

    from scipy.stats import pearsonr

The analysis examines the relationship between selected features and the target variable `charges`.

The features considered include:

- `age`
- `bmi`
- `children`
- `is_female`
- `is_smoker`
- `region_northwest`
- `region_southeast`
- `region_southwest`
- `bmi_category_Normal`
- `bmi_category_Overweight`
- `bmi_category_Obese`

The target variable is:

    charges

Pearson correlation is used to measure the linear relationship between each selected feature and medical insurance charges.

---

## 9. Chi-Square Statistical Analysis

Chi-Square analysis is performed to examine the relationship between categorical variables and categorized insurance charges.

The required statistical function is imported using:

    from scipy.stats import chi2_contingency

The `charges` variable is divided into four groups using quartiles:

    charges_bin = pd.qcut(
        df_cleaned['charges'],
        q=4,
        labels=False
    )

The significance level used for the statistical test is:

    alpha = 0.05

Categorical features are then tested against the categorized insurance charges.

A p-value below the significance level indicates a statistically significant association between the categorical feature and the categorized `charges` variable.

---

## 10. Final Feature Selection

After performing preprocessing, feature engineering, correlation analysis, and statistical analysis, the final selected features are:

- `age`
- `is_female`
- `bmi`
- `children`
- `is_smoker`
- `charges`
- `region_southeast`
- `bmi_category_Obese`

These features are stored in the final dataset:

    final_df

---

## Tools and Technologies

The project was developed using the following tools and libraries:

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Scikit-learn

---

## Key Analysis Areas

The project covers the following major areas:

- Exploratory Data Analysis (EDA)
- Data Cleaning
- Duplicate Removal
- Categorical Encoding
- One-Hot Encoding
- Feature Engineering
- BMI Categorization
- Feature Scaling
- Correlation Analysis
- Pearson Correlation
- Chi-Square Test
- Statistical Feature Analysis
- Feature Selection
- Data Visualization

---

## Project Structure

    Medical-Insurance-Data-Analysis/
    │
    ├── Data_Analysis.ipynb
    ├── insurance.csv
    └── README.md

---

## How to Run

### 1. Clone the Repository

    git clone https://github.com/marzansamin/Medical-Insurance-Data-Analysis.git

### 2. Navigate to the Project Directory

    cd Medical-Insurance-Data-Analysis

### 3. Install Required Libraries

    pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter

### 4. Open the Jupyter Notebook

    jupyter notebook

Open `Data_Analysis.ipynb` and run the cells sequentially.

---

## Conclusion

This project demonstrates a complete data analysis workflow on a medical insurance dataset, starting from data loading and exploratory analysis through data cleaning, preprocessing, feature engineering, visualization, feature scaling, statistical testing, and final feature selection.

The analysis provides a structured understanding of the dataset and prepares relevant features for further analysis or machine learning applications.
