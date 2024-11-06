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
Register number: 212223230175
Name: T.Roshini

import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/bb2c8d93-a543-4041-9f91-da2301328e07)
```
df.shape
```
![Screenshot 2024-08-28 104445](https://github.com/user-attachments/assets/e2b6a539-de3a-4b53-a180-01a6ddcad46f)
```
df.describe()
```
![image](https://github.com/user-attachments/assets/f4bc234b-1606-4020-9153-78f0e523e810)
```
df.info()
```
![Screenshot 2024-08-28 104632](https://github.com/user-attachments/assets/3ad77a58-4af8-4b96-a5bb-5b5d8613ef48)
```
df.head(5)
```
![Screenshot 2024-08-28 104719](https://github.com/user-attachments/assets/c54eea01-b430-4fe9-91b5-ccf97f9ff009)
```
df.tail(5)
```
![Screenshot 2024-08-28 104759](https://github.com/user-attachments/assets/cbe07d12-6ad6-4f21-ac8a-1e72358df70a)
```
df.isnull().sum()
```
![Screenshot 2024-08-28 105152](https://github.com/user-attachments/assets/b8b62abc-1a50-4c5e-9bea-74d4ac5c3ec4)
```
df.dropna(how='any').shape
```
![Screenshot 2024-08-28 105423](https://github.com/user-attachments/assets/b8f5c487-0194-4c84-85da-9a2b63640303)
```
mn=df.TOTAL.mean()
mn
```
![Screenshot 2024-08-28 105430](https://github.com/user-attachments/assets/458b8400-72a4-41d5-b658-f098429df47b)
```
df.TOTAL.fillna(mn,inplace=True)
df
```
![Screenshot 2024-08-28 105328](https://github.com/user-attachments/assets/f9d44ce6-102c-4560-9889-96d384aedaff)
```
df['M1']
```
![Screenshot 2024-08-28 105901](https://github.com/user-attachments/assets/3df0b70d-414b-43dd-9fc0-80312a5d5e40)
```
df.duplicated()
```
![Screenshot 2024-08-28 105911](https://github.com/user-attachments/assets/6e19fac7-f72e-4f98-8acc-0aadaffded64)

```
df.drop_duplicates(inplace=True)
df
```
![Screenshot 2024-08-28 095108](https://github.com/user-attachments/assets/6ee7ccc1-b183-4693-ad67-416ccb4f81a1)
```
df.duplicated()
```
![Screenshot 2024-08-28 111553](https://github.com/user-attachments/assets/a2fd35fd-f7b7-41ef-a4bc-223cdc71e1b8)
```
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![Screenshot 2024-08-28 111650](https://github.com/user-attachments/assets/37d270d6-e9df-4d61-a71d-ae7390fa9f43)
```
df.dropna(inplace=True)
df
```
![Screenshot 2024-08-28 111733](https://github.com/user-attachments/assets/86695d99-7828-44da-b821-f545dd0a27c0)
```
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![Screenshot 2024-08-28 111814](https://github.com/user-attachments/assets/00c4fedc-bdc1-4426-af61-bbd52f64a307)

## Outliers detection and removal using IQR
```
import pandas as pd
import seaborn as sns
import numpy as np
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
afd removal using IQR
```
![Screenshot 2024-08-28 112807](https://github.com/user-attachments/assets/976ecdab-6e06-4ec2-9c5a-142b997797b7)
```
sns.boxplot(data=af)
```
![Screenshot 2024-08-28 112842](https://github.com/user-attachments/assets/86915e35-4957-473c-b7d8-1c7d20793a07)
```
sns.scatterplot(data=af)
```
![Screenshot 2024-08-28 112910](https://github.com/user-attachments/assets/cb10a3b1-a3d2-4f45-af4e-8e2fa261ad76)
```
Q1=np.percentile(af,25)
Q2=np.percentile(af,50)
Q3=np.percentile(af,75)
IQR=Q3-Q1
IQR
```
![Screenshot 2024-08-28 113508](https://github.com/user-attachments/assets/8810e8bd-ff0a-4b06-9f41-e3512019fe7a)
```
lower_bound=Q1-(1.5*IQR)
upper_bound=Q3+(1.5*IQR)
lower_bound,upper_bound
```
![Screenshot 2024-08-28 113517](https://github.com/user-attachments/assets/e18a074e-fc80-48b5-9883-c18bc4388f8e)
```
outliers = [x for x in age if (x < lower_bound) or (x > upper_bound)] # Removed .iloc[0] as lower_bound and upper_bound are not series.
print("q1",Q1)
print("q3",Q3)
print("iqr",IQR)
print("lower bound",lower_bound)
print("upper bound",upper_bound)
print("outliers",outliers)

af=af[((af>=lower_bound)&(af<=upper_bound))]
af.dropna()
```
![Screenshot 2024-08-28 113653](https://github.com/user-attachments/assets/bcbdf35a-78f7-4b01-a46c-f3798963afda)
```
data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print('mean of the dataset is',mean)
print('std.deviation is',std)
```
![Screenshot 2024-08-28 113700](https://github.com/user-attachments/assets/020027b0-0353-4679-afbe-e0074a297ab1)
```
threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z>threshold:
    outlier.append(i)
    print('Outlier in dataset is:',outlier)
```
![Screenshot 2024-08-28 113707](https://github.com/user-attachments/assets/92d19ab0-c20a-4ac6-b38c-2e5af05b3606)
```
import pandas as pd
import numpy as np
import seaborn as sns
import pandas as pd
from scipy import stats

data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
```
![Screenshot 2024-08-28 114159](https://github.com/user-attachments/assets/72e5d64e-1b89-4501-a072-0e55d3d4ee98)
```
df=pd.DataFrame(data)
df

z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
```
![Screenshot 2024-08-28 114226](https://github.com/user-attachments/assets/ae810c82-2267-4a68-b882-a83ce54964a2)
```
val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]

import numpy as np
out=[]
def d_o(val):
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out

op=d_o(val)

op
```
![Screenshot 2024-08-28 114234](https://github.com/user-attachments/assets/20d0d656-d838-45e9-81a1-af5db1cf1af4)


# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.














