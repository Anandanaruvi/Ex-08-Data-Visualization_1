### Ex-08-Data-Visualization-

### AIM

To Perform Data Visualization on a complex dataset and save the data to a file. 

### Explanation

Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

### ALGORITHM

### STEP 1

Read the given Data

### STEP 2

Clean the Data Set using Data Cleaning Process

### STEP 3

Apply Feature generation and selection techniques to all the features of the data set

### STEP 4

Apply data visualization techniques to identify the patterns of the data.

### PROGRAM:

NAME:A.ARUVI

REG.NO:212222230014

### CODE
```
# loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
```

### removing unnecessary data variables

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

df.isnull().sum()
```

### detecting and removing outliers in current numeric data
```
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
### data visualization

### line plots
```
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```

### Histogram
```
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```

### count plot
```
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```

### BARPLOTS
```
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```

### KDE plot

```
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```
### point plot
```
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```

### Pie Chart
```
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
#HeatMap
df4=df.copy()
```

### encoding
```
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
```
### scaling
```
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])
```
### Heatmap
```
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
### OUPUT

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/0791595d-5fda-4663-bab5-15fb35fa64cd)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/6abaed08-45cb-43d5-8161-f78fdf7ffac0)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/0068cf7c-fe9e-40e9-89ac-f9f7e105ce41)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/73683966-0229-413f-82c8-de8140ff921d)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/8af1b511-3f65-40f6-9dcf-490de203cf5d)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/1ea77774-fb2d-40f2-9552-3f467376e0ed)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/a4191e4a-32a7-4370-b6b7-b2f98e4f2a7d)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/cefb749b-2a61-4463-96a7-e68995ee5fc9)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/a1342f8f-7b99-4251-9916-634939cf2ae1)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/693760e7-b086-4f76-a148-76a893435aac)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/cd08d2ed-cba5-4fe6-83a8-7eea096e507b)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/c388eb1f-b0b7-45cd-a092-7380d7858734)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/2d999852-5804-4edc-855f-091c5588ed44)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/cfb433ea-ca1d-4528-9cbc-68afdc661b92)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/2d4b4d2d-7938-4e64-9866-88ef4dd1932f)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/f63e790e-3e4e-4b3d-bf3d-7bf675946f88)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/43e67898-e85e-4b83-8ff0-733711d8b65b)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/ad9cf2c7-9f23-484c-b2b6-25e542da87a1)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/66b6513f-6d73-4af0-b2ef-e0d084325cc7)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/fc1528df-9bb7-46b9-accb-a74b99ad4432)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/c6f10776-ce91-490a-9ce8-4c6368a6c49f)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/e1b55699-8fa8-4e08-adfd-e686d469a9e4)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/34a36d32-ffcf-4a76-af6e-45ab61701414)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/2b907569-2a34-45dd-b12f-2beafd3321b9)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/3909c45c-cf16-4bca-a25c-9fe2a44812e3)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/42d1c8a8-17f9-4814-b7ae-33e083c895a5)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/12d0466c-c0db-4ab4-b3fa-5e42237c1803)

![image](https://github.com/Anandanaruvi/Ex-08-Data-Visualization_1/assets/120443233/2ca55051-f51d-48ab-ab21-f4490eaeb425)

### Result:

Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file
