# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

#Reading the Data Set
df = pd.read_csv("Data_set.csv")
df

#Filling NULL values using fillna() method
df_fill = df.fillna(0)
df_fill

#Filling NULL values using fillna() method with their  mean() values.
df['watchers'] = df['watchers'].fillna(df['watchers'].mean())
df

#Updating the Datasetby removing NULL values
df2_dropna = df.dropna()
df2_dropna.to_csv('clean_data_2.csv', index=False)


#Outliers Removal using IQR technique
ir = pd.read_csv("Data_set.csv")
Q1 = ir['watchers'].quantile(0.25) 
Q3 = ir['watchers'].quantile(0.75) 
IQR = Q3 - Q1
print("IQR:", IQR)

outliers_iqr = ir[ (ir['watchers'] < (Q1 - 1.5 * IQR)) | (ir['watchers'] > (Q3 + 1.5 * IQR)) ]
outliers_iqr

ir_cleaned = ir[ ~((ir['watchers'] < (Q1 - 1.5 * IQR)) | (ir['watchers'] > (Q3 + 1.5 * IQR))) ]
ir_cleaned


#Outliers Removal using Z-Score technique
df1 = pd.read_csv('Data_set.csv')
numerical_cols = ['num_episodes', 'rating', 'current_overall_rank', 'lifetime_popularity_rank', 'watchers']

z_scores = df1[numerical_cols].apply(lambda x: (x - x.mean()) / x.std())

outliers = (z_scores.abs() > 3).any(axis=1)

df_cleaned = df[~outliers]
df_cleaned
```
<img width="1288" height="737" alt="image" src="https://github.com/user-attachments/assets/872f7819-1e3f-46de-a672-af551b6aba75" />
<img width="286" height="209" alt="image" src="https://github.com/user-attachments/assets/fc3fd85d-f8c7-4593-889e-99d119d7b367" />
<img width="1180" height="459" alt="image" src="https://github.com/user-attachments/assets/0be38805-bbcb-45fd-80c2-43d3829b21ed" />
<img width="1222" height="663" alt="image" src="https://github.com/user-attachments/assets/cf9871b8-4569-4b40-992f-49f8c9b12c5a" />
<img width="1200" height="25" alt="image" src="https://github.com/user-attachments/assets/d4edac2d-8e5e-432b-b340-bf25971ede42" />
<img width="1224" height="466" alt="image" src="https://github.com/user-attachments/assets/a2c4f6f9-17ac-40b8-8971-1714de28929f" />
<img width="1224" height="664" alt="image" src="https://github.com/user-attachments/assets/1adb862a-a9a2-4830-b574-2cc14a16e7c5" />


# Result
Thus, the data cleaning process is completed successfully.
