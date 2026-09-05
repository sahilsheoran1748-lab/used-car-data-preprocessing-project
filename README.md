# 🚗 Used Car Data Preprocessing Project

## 📌 Project Overview

This project demonstrates a complete **Data Acquisition, Data Cleaning, and Data Preprocessing workflow** using Python.

The project uses a **Used Car Market Dataset** containing vehicle-related information such as price, mileage, year, make, model, fuel type, transmission, and condition.

The main objective is to transform raw and messy data into a **clean, structured, and machine-learning-ready dataset**.

---

## 🎯 Project Objectives

The main objectives of this project are:

* 📥 Load and explore the dataset
* 🧹 Clean inconsistent and incorrect data
* ❓ Handle missing values
* 🚫 Detect and handle invalid entries
* 📊 Identify and treat outliers
* 🔤 Convert categorical data into numerical format
* 📏 Scale numerical features
* 🤖 Prepare the dataset for Machine Learning and Data Analysis

---

# 📂 Dataset Features

The dataset contains information related to used cars.

Some important features include:

* **Price**
* **Mileage**
* **Year**
* **Make**
* **Model**
* **Fuel_Type**
* **Transmission**
* **Condition**
* **Engine_Size**

The dataset may contain approximately **50,000 records and multiple columns** representing numerical and categorical vehicle information.

---

# 🔍 Technologies Used

This project was developed using:

* 🐍 Python
* 🐼 Pandas
* 🔢 NumPy
* 📊 Matplotlib
* 📈 Seaborn
* 🤖 Scikit-learn

---

# ⚙️ Project Workflow

## 1️⃣ Data Collection

The Used Car Sales dataset is loaded into Python using Pandas.

```python
import pandas as pd

df = pd.read_csv('used_cars_raw.csv')
```

---

## 2️⃣ Initial Data Exploration

The dataset is explored to understand its structure and identify potential problems.

```python
print(df.info())
print(df.describe())
print(df.head())
```

This helps identify:

* Missing values
* Incorrect data types
* Invalid values
* Outliers
* Inconsistent formatting

---

## 3️⃣ Data Cleaning

### 🚗 Cleaning the Mileage Column

The Mileage column may contain values such as:

```text
50,000 km
```

These characters are removed before converting the values into numerical format.

```python
df['Mileage'] = df['Mileage'].astype(str).str.replace(' km', '', regex=False)
df['Mileage'] = df['Mileage'].str.replace(',', '', regex=False)

df['Mileage'] = pd.to_numeric(
    df['Mileage'],
    errors='coerce'
)
```

---

### 📅 Handling Invalid Year Values

Invalid vehicle years are converted into missing values.

```python
current_year = 2024

df.loc[
    (df['Year'] > current_year) |
    (df['Year'] < 1990),
    'Year'
] = np.nan
```

---

### 💰 Handling Invalid Prices

Negative or zero prices are considered invalid.

```python
df.loc[df['Price'] <= 0, 'Price'] = np.nan
```

---

# ❓ Handling Missing Values

Missing values are first analyzed.

```python
missing_percentages = (
    df.isnull().sum() / len(df)
) * 100

print(missing_percentages)
```

### Numerical Columns

Median values are used for numerical columns.

```python
df['Mileage'] = df['Mileage'].fillna(
    df['Mileage'].median()
)

df['Price'] = df['Price'].fillna(
    df['Price'].median()
)
```

### Categorical Columns

Mode values are used for categorical columns.

```python
df['Condition'] = df['Condition'].fillna(
    df['Condition'].mode()[0]
)
```

### Critical Missing Values

Rows with missing **Make** or **Model** are removed.

```python
df = df.dropna(
    subset=['Make', 'Model']
)
```

---

# 📊 Outlier Detection and Treatment

The **Interquartile Range (IQR)** method is used to identify and handle outliers.

```python
def cap_outliers_iqr(dataframe, column):

    Q1 = dataframe[column].quantile(0.25)
    Q3 = dataframe[column].quantile(0.75)

    IQR = Q3 - Q1

    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR

    dataframe[column] = np.where(
        dataframe[column] > upper_bound,
        upper_bound,
        dataframe[column]
    )

    dataframe[column] = np.where(
        dataframe[column] < lower_bound,
        lower_bound,
        dataframe[column]
    )

    return dataframe
```

The function is applied to:

```python
df = cap_outliers_iqr(df, 'Price')
df = cap_outliers_iqr(df, 'Mileage')
```

---

# 🔤 Data Preprocessing

## One-Hot Encoding

Categorical variables are converted into numerical values.

```python
df_encoded = pd.get_dummies(
    df,
    columns=valid_cat_cols,
    drop_first=True
)
```

---

## 📏 Feature Scaling

Numerical features are standardized using **StandardScaler**.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

df_encoded[valid_num_cols] = scaler.fit_transform(
    df_encoded[valid_num_cols]
)
```

---

# 📈 Final Output

After completing the preprocessing steps, the dataset becomes:

✅ Cleaned
✅ Structured
✅ Free from invalid values
✅ Missing values handled
✅ Outliers treated
✅ Categorical variables encoded
✅ Numerical features scaled
✅ Ready for Machine Learning

---

# 🛠️ Installation

Clone this repository:

```bash
git clone YOUR_REPOSITORY_URL
```

Move into the project folder:

```bash
cd Data-Preprocessing-Project
```

Install the required libraries:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

---

# ▶️ How to Run the Project

1. Clone or download this repository.
2. Install all required Python libraries.
3. Place the dataset file inside the project folder.
4. Open the Python notebook or script.
5. Run all cells or execute the program.
6. The cleaned and preprocessed dataset will be ready for further analysis.

---

# 📁 Project Structure

```text
Data-Preprocessing-Project/
│
├── README.md
├── Data_Preprocessing_Project_Report.pdf
├── used_cars_raw.csv
├── data_preprocessing.ipynb
│
└── requirements.txt
```

---

# 🧠 Key Learning Outcomes

Through this project, the following Data Science concepts were practiced:

* Data Acquisition
* Data Exploration
* Data Cleaning
* Missing Value Handling
* Data Imputation
* Outlier Detection
* IQR Method
* Feature Encoding
* Feature Scaling
* Data Preprocessing
* Preparing Data for Machine Learning

---

# 🚀 Future Improvements

Possible future improvements include:

* 📊 Advanced Exploratory Data Analysis (EDA)
* 🤖 Machine Learning Model Development
* 💰 Used Car Price Prediction
* 📈 Data Visualization Dashboard
* 🧠 Feature Engineering
* 🔍 Hyperparameter Optimization

---

# 👨‍💻 Author

**Sahil Kumar**

---

# ⭐ Conclusion

This project demonstrates a complete and practical **Data Cleaning and Data Preprocessing workflow using Python**.

The raw Used Car dataset is transformed into a clean and machine-learning-ready dataset by handling missing values, correcting inconsistent data, treating outliers, encoding categorical variables, and scaling numerical features.

This project provides a strong foundation for further **Data Analysis, Machine Learning, and Used Car Price Prediction models**.

---


