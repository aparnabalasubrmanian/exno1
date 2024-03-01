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


            
# DATA CLEANIN
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![Screenshot (222)](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/7b656242-baea-4e9d-ab48-8eabef6a8814)
```
data = pd.get_dummies(data)
data.isnull().sum()
```
![Screenshot (223)](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/b95be498-7dcf-4f1b-b8fa-18dd6c961728)
```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![307660899-deddaf55-87f4-42dc-b4ce-280775cc04b5](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/c97ff983-bca5-401c-bad1-537b54cc593b)
```
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
#IQR
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```
![307661018-93d4d44c-8a8e-42ba-b50e-0d427a929e41](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/e0ab58a3-f6c4-4150-9ec1-fc360883f213)
```
ir.describe()
```
![307661079-82718575-7497-43ea-b6b0-0c048b061dd6](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/14c52f26-49d7-4773-a3dc-691df7888d24)
```
sns.boxplot(x='sepal_width',data=ir)
```
![307661160-2a264b0b-1be7-4cb5-993a-edfb54c7369d](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/3b4d7891-2bb0-4c00-a5f4-02e0be6035f6)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![307661214-ec87fae6-5baa-4b0a-9c09-1c4e1c893ad8](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/a525ca98-7554-4860-98cb-b417ec6f6de5)
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![307661252-a6e1a0ff-84f2-47ae-a39a-f8037875611e](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/265bcde4-895d-4333-8226-7a2f24d6196d)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![307661285-8becd206-ddc7-4a58-85fc-b9cb1b63a53f](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/8985d070-d77f-4bd7-b9c5-b9f4860ca979)
```
sns.boxplot(x='sepal_width',data=delid)
```
![307661338-53b3e4cc-9961-4b92-af15-afa9dca57f97](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/89bb915b-d491-42d2-b988-71cc15bd0a78)


# Z SCORE
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![307661405-65296f84-d620-42a2-91e9-825f3313e72c](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/827293f2-76d9-4d1c-a7a3-0c0ea93a0838)
```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![307661484-b9d6b692-7f29-4303-8e22-335186cf6ae3-1](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/dbc944ae-4f89-4498-814d-0d00d4147a7f)
```
low = q1 - 1.5*iqr
low
```
![307661531-3f341bea-42c2-4cbd-928a-9e1fa576cfaf](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/a62dd212-32e8-4f6e-a9bb-cd4e5be1c40e)
```
high = q3 + 1.5*iqr
high
```
![307661569-ae80602f-3344-443c-a723-d5cef7928731](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/74bb2438-286d-417c-9a8f-7511df91f02e)
```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![307661642-3e5ce1e1-567e-4253-82bb-192c04024d35](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/e14fa31d-adf2-4da4-aa7f-17beac6b0a1d)
```
z = np.abs(stats.zscore(df['height']))
z
```
![307661670-ef207f0d-fcc0-452e-bbd3-5f3c48a03515](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/0bbf349d-f89c-4069-b6dc-bfa65b58d8f1)


# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.       
