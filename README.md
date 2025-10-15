# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT

# Step 1: Import necessary libraries
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# Step 2: Load the Titanic dataset
df = pd.read_csv("titanic_dataset.csv")

# Display basic info
print("Dataset shape:", df.shape)
print("\nFirst 5 rows of the dataset:")
print(df.head())

# Step 3: Check for missing values
print("\nMissing values in each column:")
print(df.isnull().sum())

# Step 4: Fill missing values
# Fill numeric columns with median, categorical with mode
for col in df.columns:
    if df[col].dtype in ['int64', 'float64']:
        df[col].fillna(df[col].median(), inplace=True)
    else:
        df[col].fillna(df[col].mode()[0], inplace=True)

print("\nAfter filling missing values:")
print(df.isnull().sum())

# Step 5: Boxplot to detect outliers
plt.figure(figsize=(10,6))
sns.boxplot(data=df.select_dtypes(include=['int64', 'float64']))
plt.title("Boxplot - Detecting Outliers")
plt.show()

# Step 6: Remove outliers using IQR
Q1 = df.quantile(0.25)
Q3 = df.quantile(0.75)
IQR = Q3 - Q1
df_clean = df[~((df < (Q1 - 1.5 * IQR)) | (df > (Q3 + 1.5 * IQR))).any(axis=1)]

print("\nShape before removing outliers:", df.shape)
print("Shape after removing outliers:", df_clean.shape)

# Step 7: Countplot for categorical data
categorical_cols = df_clean.select_dtypes(include='object').columns
for col in categorical_cols:
    plt.figure(figsize=(7,4))
    sns.countplot(x=col, data=df_clean)
    plt.title(f"Countplot for {col}")
    plt.xticks(rotation=45)
    plt.show()

# Step 8: Displot for numerical columns
numeric_cols = df_clean.select_dtypes(include=['int64', 'float64']).columns
for col in numeric_cols:
    sns.displot(df_clean[col], kde=True)
    plt.title(f"Distribution of {col}")
    plt.show()

# Step 9: Cross-tabulation between Survived and Sex (example)
if 'Survived' in df_clean.columns and 'Sex' in df_clean.columns:
    ct = pd.crosstab(df_clean['Survived'], df_clean['Sex'])
    print("\nCross Tabulation between Survived and Sex:")
    print(ct)

# Step 10: Correlation heatmap
plt.figure(figsize=(10,6))
sns.heatmap(df_clean.corr(), annot=True, cmap='coolwarm')
plt.title("Heatmap - Correlation between Numerical Features")
plt.show()

<img width="2000" height="1200" alt="heatmap" src="https://github.com/user-attachments/assets/ea639ed4-d14c-40a7-b5e6-c8958edb5d75" />
<img width="1600" height="4000" alt="countplots_combined" src="https://github.com/user-attachments/assets/04565b05-af99-4fda-b2ea-d1addd0ae100" />
<img width="1000" height="1000" alt="displot" src="https://github.com/user-attachments/assets/6d6db42a-2db5-4130-82e2-7720849866b1" />
<img width="2000" height="1200" alt="boxplot" src="https://github.com/user-attachments/assets/f5287600-aaf7-49b5-8271-f524f4fe3084" />




# RESULT
The above program was executed successfully.
