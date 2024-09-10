# Exno:1
Data Cleaning Process

# Reg no:212223040228

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
df=pd.read_csv("/content/SAMPLEIDS (1).csv")
df
```
![image](https://github.com/user-attachments/assets/dc5296a4-128d-4c39-8b8b-d0aa80b63a6a)
```
df.head(3)
df.tail(3)
```
![image](https://github.com/user-attachments/assets/81d33253-2e51-4d07-a78c-761f9be374f9)
```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/da3b02c1-2150-4a19-92c5-6a79be289848)
```
df.dropna(how='any').shape
```
![image](https://github.com/user-attachments/assets/a13d7913-81c6-43e1-ae11-39fcddf71d1a)
```
df.shape
```
![image](https://github.com/user-attachments/assets/799072d5-9bfe-4909-8698-210f92418bd1)
```
mn=df.TOTAL.mean()
mn
```
![image](https://github.com/user-attachments/assets/629e2312-bac1-4b29-96dc-eb29baa15a66)
```
df.TOTAL.fillna(mn,inplace=True)
df
```
![image](https://github.com/user-attachments/assets/b8a09927-ffc0-4674-b02b-d58b0a417735)
```
df.drop_duplicates(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/8d29b176-92a4-4f05-b9b4-78d78049f729)
```
df.duplicated()
```
![image](https://github.com/user-attachments/assets/728c5a9a-aea1-4c8a-9e44-192eb12851f9)
```
df['DOB']
```
![image](https://github.com/user-attachments/assets/e3a82faa-7c9b-4707-902a-6b013e09fe32)
```
df['DOB'] = pd.to_datetime(df['DOB'], format='%Y-%m-%d',errors='coerce')
df['DOB']
```
![image](https://github.com/user-attachments/assets/58c7c907-30e5-4f2f-96ae-1c396697d52e)
```
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![image](https://github.com/user-attachments/assets/b535faa9-03b7-44b1-88f2-0afe9dfc76a5)
```
import pandas as pd
import seaborn as sns
import numpy as np
```
```
age = [1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af= pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/9bf7ee04-3282-46dc-b0fa-d0b4ef47e4f2)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/051ee6a7-7366-4af4-b27f-b28138bfdca8)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/06c119e7-1628-48ff-93d1-1354899a534d)
```
sns.scatterplot(data=af)
```
![image](https://github.com/user-attachments/assets/8d44f7c5-24d4-4941-bf1f-532c78e5ea87)
```
q1=af.quantile(0.25)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/8f92f101-6526-4829-ab02-21cafea105e3)
```
Q1 = np.quantile(af, 0.25)
Q3 = np.quantile(af, 0.75)
IQR = Q3 - Q1
IQR
```
![image](https://github.com/user-attachments/assets/51d8a833-1b73-4aca-9080-e54ed44f5e4a)
```
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
```
```
lower_bound
```
![image](https://github.com/user-attachments/assets/cc3e48aa-6970-486a-9d9a-abb36da6a8be)


```
upper_bound
```
![image](https://github.com/user-attachments/assets/3ff5242b-6407-4d13-864b-eb5861a838b8)
```
outliers = [x for x in age if x < lower_bound or x > upper_bound]
```
```
print("Q1:",Q1)
print("Q3:",Q3)
print("IQR:",IQR)
print("Lower Bound:",lower_bound)
print("Upper Bound:",upper_bound)
print("Outliers:",outliers)
```
![image](https://github.com/user-attachments/assets/9f2b5fec-0d94-4fdf-910d-f2251c935709)
```
af=af[((af >= lower_bound)&(af <= upper_bound))]
af
```
![image](https://github.com/user-attachments/assets/91e9ae95-fc5e-44ae-b43f-4c572e0d83b1)
```
af.dropna()
```
![image](https://github.com/user-attachments/assets/28f93c7a-a549-4698-80c4-1974494905a3)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/37c000c9-9d02-4a49-bcda-794c4602d03c)
```
data = [1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean = np.mean(data)
std = np.std(data)
print('mean of the dataset is',mean)
print('std.deviation is',std)
```
![image](https://github.com/user-attachments/assets/820f14f8-553c-479b-b8f0-d5a0728e58aa)
```
threshold = 3
outlier = []
for i in data:
  z_score = (i-mean)/std
  if np.abs(z_score) > threshold:
    outlier.append(i)
print('outlier in dataset is',outlier)
```
![image](https://github.com/user-attachments/assets/c8bfd829-77d4-406b-a7c1-d799cbe41708)
```
import pandas as pd
import numpy as np
import seaborn as sns
import pandas as pd
from scipy import stats
```
```
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
```
```
df=pd.DataFrame(data)
```
```
df
```
![image](https://github.com/user-attachments/assets/f75d6dc4-a064-49fc-b4a5-b7c8cddb1271)

# Result
         Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score
method.
