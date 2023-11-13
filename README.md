# Ex-08-Data-Visualization-
# AIM
To Perform Data Visualization on a complex dataset and save the data to a file.

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
## STEP 1
Read the given Data

## STEP 2
Clean the Data Set using Data Cleaning Process

## STEP 3
Apply Feature generation and selection techniques to all the features of the data set

## STEP 4
Apply data visualization techniques to identify the patterns of the data.

# CODE
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files
uploaded = files.upload()
df=pd.read_csv("SuperStore.csv",encoding='unicode_escape')
df
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/f3f18839-7353-4b8b-bbe6-2d74d1442247)
```
df.isnull().sum()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/ef4d2fa7-1c88-4a1b-9842-f662bbd267ec)
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/81554c40-4298-4c1f-9bd2-96701aeb30be)
```
#detecting and removing outliers in current numeric data
plt.figure(figsize=(8,8))
plt.title("Data with outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/95c77939-897e-4d56-a4af-5290d08a4f5e)
```
plt.figure(figsize=(8,8))
cols = ['Sales','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/45fd5b85-5a70-45a5-8f0f-6a04106aa925)
## Which Segment has Highest sales?
```
sns.lineplot(x="Segment",y="Sales",data=df,marker='o')
plt.title("Segment vs Sales")
plt.xticks(rotation = 90)
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/1e515801-12bd-4cc8-bca0-c75fe448e78b)
```
sns.barplot(x="Segment",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/2e0a8e05-ff60-4f23-859f-66941d0a3a7d)
## Which City has Highest profit?
```
df.shape
df1 = df[(df.Profit >= 60)]
df1.shape
```
```
plt.figure(figsize=(30,8))
states=df1.loc[:,["City","Profit"]]
states=states.groupby(by=["City"]).sum().sort_values(by="Profit")
sns.barplot(x=states.index,y="Profit",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("City")
plt.ylabel=("Profit")
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/de65a4df-feca-4034-8fca-508b963724f2)
## Which ship mode is profitable?
```
sns.barplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/702bba9c-e3e8-4093-a182-6f7d96ed71f8)
```
sns.lineplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/291fd812-2a87-41ba-8c1d-3bcc58837d88)
```
sns.violinplot(x="Profit",y="Ship Mode",data=df)
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/58c517fa-73d4-41f4-ad5f-28982b1e1dde)
```
sns.pointplot(x=df["Profit"],y=df["Ship Mode"])
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/8c2417ed-975d-4a1c-b341-b28b1843579f)
## Sales of the product based on region
```
states=df.loc[:,["Region","Sales"]]
states=states.groupby(by=["Region"]).sum().sort_values(by="Sales")
sns.barplot(x=states.index,y="Sales",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("Region")
plt.ylabel=("Sales")
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/91664482-3697-40dd-b21f-c94ea33ed4d3)
```
df.groupby(['Region']).sum().plot(kind='pie', y='Sales',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/3a0344e0-8aad-497d-91ec-20e2da0ec148)
## Find the relation between sales and profit.
```
df["Sales"].corr(df["Profit"])
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/7740460d-09f6-41ed-818e-9d3ede6a8595)
```
df_corr = df.copy()
df_corr = df_corr[["Sales","Profit"]]
df_corr.corr()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/e6edcf95-bd47-43e1-970c-53048c6dfcaa)
```
sns.pairplot(df_corr, kind="scatter")
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/cf3b051d-6476-457e-9ac9-6f43ee94e049)
## Heatmap
```
df4=df.copy()

encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/9ecb1440-2df4-4c3a-b290-7395039f5961)
## Find the relation between sales and profit based on the following category.
### Segment
```
grouped_data = df.groupby('Segment')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/c255b358-5aad-461e-8f93-7b6dbe84a204)
### City
```
grouped_data = df.groupby('City')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('City')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/c0eabd70-fda8-492c-b5b3-836c6b9b7462)
### States
```
grouped_data = df.groupby('State')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('State')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/44a56bbc-0b80-43da-8236-9aa99859d685)
## Segment and Ship Mode
```
grouped_data = df.groupby(['Segment', 'Ship Mode'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index='Segment', columns='Ship Mode', values=['Sales', 'Profit'])
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
pivot_data.plot(kind='bar', ax=ax)
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
plt.legend(title='Ship Mode')
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/2df8b807-d26e-4c90-b710-e6a4361ecd5e)
## Segment, Ship mode and Region
```
grouped_data = df.groupby(['Segment', 'Ship Mode','Region'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index=['Segment', 'Ship Mode'], columns='Region', values=['Sales', 'Profit'])
sns.set_style("whitegrid")
sns.set_palette("Set1")
pivot_data.plot(kind='bar', stacked=True, figsize=(10, 5))
plt.xlabel('Segment-Ship Mode')
plt.ylabel('Value')
plt.legend(title='Region')
plt.show()
```
![image](https://github.com/mathes6112004/ODD2023-Datascience-Ex-08/assets/119477782/91ced2a9-1ceb-4a12-83d5-a25743dd4059)

# RESULT:
Thus, Data Visualization is performed on the given dataset and save the data to a file.
