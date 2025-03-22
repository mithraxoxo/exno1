# Ex. 1 Data Cleaning and Outlier Detection & Removal

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

# Coding and Output:
# Data cleaning
~~~
import pandas as pd
exp=pd.read_csv("/content/SAMPLEIDS.csv")
exp
~~~
![image](https://github.com/user-attachments/assets/05882a13-721e-4a9b-b997-565cb033b696)
~~~
exp.isnull().sum()
~~~
![Screenshot 2025-03-06 202920](https://github.com/user-attachments/assets/ec52c3c0-1102-4260-9a00-c0e44fa2d940)
~~~~
exp.isnull().any()
~~~~
![image](https://github.com/user-attachments/assets/4328c4b0-8e86-4434-98b2-d4e31f28918a)
~~~
exp.dropna()
~~~
![image](https://github.com/user-attachments/assets/f170ff35-5e1e-4eb4-a650-7dc00f981913)
~~~
exp.fillna(0)
~~~
![image](https://github.com/user-attachments/assets/37034086-22f4-4f94-beea-d6768ea7a450)
~~~
exp.fillna(method="ffill")
~~~
![image](https://github.com/user-attachments/assets/fec3e14e-2952-40b9-bc59-50a7370b766d)
~~~
exp.fillna(method="bfill")
~~~
![image](https://github.com/user-attachments/assets/d85355d3-8633-450e-a663-7ac4bde134bb)
~~~
exp_dropped=exp.dropna()
exp_dropped
~~~
![image](https://github.com/user-attachments/assets/bc56c7ee-1a5a-49a0-9eff-486dd38257b7)
~~~
exp.fillna({'NAME':'MOHAN','GENDER':'MALE','ADDRESS':'THIRUVOTTIYUR','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
~~~
![image](https://github.com/user-attachments/assets/e47dcb72-4a0f-4526-a6cf-2b676f47450b)

# IQR(Inter Quartile Range)

~~~
import pandas as pd
ir=pd.read_csv("/content/iris.csv")
ir
~~~
![image](https://github.com/user-attachments/assets/99fee4b7-7a8f-4017-9408-2a671b29b38b)
~~~
ir.describe()
~~~
![image](https://github.com/user-attachments/assets/f928476f-dc3d-4aa3-b6bc-dd481db64ee2)
~~~
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
~~~
![image](https://github.com/user-attachments/assets/5ba6ef3f-147c-4827-a11b-f6db4a4983e3)
~~~
q1=ir.sepal_width.quantile(0.25)
q3=ir.sepal_width.quantile(0.75)
iqr=q3-q1
print(iqr)
~~~
![image](https://github.com/user-attachments/assets/a1723ce4-7b65-4d23-ab6d-fc54bbb0f24d)
~~~
outlier=ir[((ir.sepal_width<(q1-1.5*iqr))|(ir.sepal_width>(q3+1.5*iqr)))]
outlier['sepal_width']
~~~
![image](https://github.com/user-attachments/assets/0c50b222-6146-490d-8b1e-fcda1ed2eb95)
~~~
o=ir[~((ir.sepal_width<(q1-1.5*iqr))|(ir.sepal_width>(q3+1.5*iqr)))]
print(o)
~~~
![image](https://github.com/user-attachments/assets/0abfcdf7-74b6-472d-befa-f1708592e2f1)
~~~
sns.boxplot(x='sepal_width',data=o)
~~~
![image](https://github.com/user-attachments/assets/af2961e6-389c-405b-a72c-42e9c9721bdf)

# Z-Score

~~~
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
data_set=pd.read_csv("/content/heights.csv")
data_set
~~~
![image](https://github.com/user-attachments/assets/416eef78-2fbe-4a79-8440-5f03cb87d5c1)
~~~
z=pd.read_csv("/content/heights.csv")
q1=z['height'].quantile(0.25)
q2=z['height'].quantile(0.50)
q3=z['height'].quantile(0.75)
iqr=q3-q1
print(iqr)
~~~
![image](https://github.com/user-attachments/assets/0175302b-65ed-4d46-9418-f3b72263dc0e)
~~~
low = q1-1.5*iqr
print(low)
~~~
![image](https://github.com/user-attachments/assets/7d5f05c5-3ebd-41e9-8357-aa66dbed5a83)
~~~
high = q3+1.5*iqr
print(high)
~~~
![image](https://github.com/user-attachments/assets/3bbfc5e0-098a-4fb8-bd6d-ba1a7ba09adc)
~~~
z1=z[((z['height']>=low)&(z['height']<=high))]
z1
~~~
![image](https://github.com/user-attachments/assets/ca0e2ed1-073e-4e53-a485-9f06e0e72c34)
~~~
z=np.abs(stats.zscore(z['height']))
z
~~~
![image](https://github.com/user-attachments/assets/dc185b03-f8d1-4326-91d8-ab18d8ba9c2d)
~~~
z1=z[z<3]
z1
~~~
![image](https://github.com/user-attachments/assets/02a045df-0269-46db-80a0-19340cd1591d)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
