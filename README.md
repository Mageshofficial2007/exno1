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

```python

import pandas as pd
df = pd.read_csv('Data_set.csv')
df.head()
```

![Screenshot 2025-03-14 161057](https://github.com/user-attachments/assets/99deeff5-1df8-47a6-80d8-aa520b0e8934)

```python
df = pd.read_csv('Data_set.csv')
df.tail()
```

![Screenshot 2025-03-14 161134](https://github.com/user-attachments/assets/c2e989a4-dd18-4e2f-998d-15ee1be759af)

```python
df.info()
print()
df.describe()
```

![Screenshot 2025-03-14 161150](https://github.com/user-attachments/assets/7edb3edf-aea8-4d96-a0da-c305c37edbb3)

```python
df.isnull().sum()
```

![Screenshot 2025-03-14 161201](https://github.com/user-attachments/assets/59819892-66b9-4a38-8dda-67da48a9a98c)

```python
df.isnull().sum(axis=1)
```

![image](https://github.com/user-attachments/assets/a8a0bf23-d3fa-4de2-857b-896c966d2ace)

```python
df_dropna = df.dropna()
df_dropna
```

![Screenshot 2025-03-14 161244](https://github.com/user-attachments/assets/9671a5b6-9341-4d06-9952-2ba8d10fd915)

```python
df_filled_const = df.fillna("")
df_filled_const
```

![Screenshot 2025-03-14 161310](https://github.com/user-attachments/assets/3bd648ab-19a3-4458-8ed3-d8cd684e078f)

```python
df_bfill = df.bfill()
print(df_bfill)
```

![Screenshot 2025-03-14 161342](https://github.com/user-attachments/assets/536c9af7-54c6-49e7-9db9-057b7ecd4e7b)

```python
column_name = "your_column" 
if column_name in df.columns and df[column_name].dtype in ['int64', 'float64']:
    df[column_name].fillna(df[column_name].mean(), inplace=True)
df
```

![Screenshot 2025-03-14 161406](https://github.com/user-attachments/assets/feeaf774-524d-4b2d-b4f0-e6bb22e98f29)

```python
age = [1, 3, 28, 27, 25, 92, 30, 39, 40, 50, 26, 24, 29, 94]
af = pd.DataFrame(age, columns=['Age'])
af
```

![Screenshot 2025-03-14 161424](https://github.com/user-attachments/assets/9a38b7a3-c3a6-45b1-a651-ddeb52a056ee)

```python
plt.figure(figsize=(5, 4))
sns.boxplot(y=af["Age"])
plt.title("Boxplot Before Removing Outliers")
plt.show()
```

![Screenshot 2025-03-14 161443](https://github.com/user-attachments/assets/26991cea-185d-4e75-92a1-91187c62b3e1)

```python
Q1 = af["Age"].quantile(0.25)
Q3 = af["Age"].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = af[(af["Age"] < lower_bound) | (af["Age"] > upper_bound)]
print(outliers)
```

![Screenshot 2025-03-14 161455](https://github.com/user-attachments/assets/53a05ab8-ec5b-4750-8736-6b0f5c0991f0)

```python
af_no_outliers = af[(af["Age"] >= lower_bound) & (af["Age"] <= upper_bound)]
print(af_no_outliers)
```

![Screenshot 2025-03-14 161505](https://github.com/user-attachments/assets/f6d0090c-4962-4032-b093-822c73b46dcb)

```pthon
plt.figure(figsize=(5, 4))
sns.boxplot(y=af_no_outliers["Age"])
plt.title("Boxplot After Removing Outliers")
plt.show()
```

![Screenshot 2025-03-14 161520](https://github.com/user-attachments/assets/01ef8a6d-b5ac-4489-8571-34c4bcecebb6)

```python
data = [1, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54, 57, 60,
        63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99, 158]
df = pd.DataFrame(data, columns=["Values"])
df
```

![Screenshot 2025-03-14 161603](https://github.com/user-attachments/assets/5772744d-bb35-4e5a-bad1-fc2bdbcb36af)

```python
plt.figure(figsize=(5, 4))
sns.boxplot(y=df["Values"])
plt.title("Boxplot Before Removing Z-Score Outliers")
plt.show()
```

![Screenshot 2025-03-14 161618](https://github.com/user-attachments/assets/3e4f6752-2f45-4469-b4ea-665880dca618)

```python
from scipy import stats 
df["Z_Score"] = stats.zscore(df["Values"])
print(df["Z_Score"])
```

![Screenshot 2025-03-14 161632](https://github.com/user-attachments/assets/793b66ee-d588-4f48-933b-ec2ca23f5154)

```python
outliers_z = df[abs(df["Z_Score"]) > 3]
outliers_z
```

![Screenshot 2025-03-14 161657](https://github.com/user-attachments/assets/7e958c2e-aa9d-43eb-93ac-13006eab0a9a)

```python
df_no_outliers = df[abs(df["Z_Score"]) <= 3].drop(columns=["Z_Score"])
df_no_outliers
```

![Screenshot 2025-03-14 161722](https://github.com/user-attachments/assets/a780d9c4-66c9-4129-a026-b011cdba4098)

```python
plt.figure(figsize=(5, 4))
sns.boxplot(y=df_no_outliers["Values"])
plt.title("Boxplot After Removing Z-Score Outliers")
plt.show()
```

![Screenshot 2025-03-14 161734](https://github.com/user-attachments/assets/7be34459-629b-4189-8852-441abd4e3c1c)

# Result
Thus,The given data is read and data cleaning process , outlier deduction and removal is performed successfully.
         
