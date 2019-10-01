# Loading Libaries


```python
#Common imports
import sys
import os
# Numpy for stastics 
import numpy as np

#Python Data Analysis Library
import pandas as pd

#Data visualization
%matplotlib inline 
#sets the backend of matplotlib to the 'inline' backend
#%matplotlib notebook
import matplotlib 
import seaborn as sns
import matplotlib.pyplot as plt

# Ignore useless warnings (see SciPy issue #5998)
import warnings
warnings.filterwarnings(action="ignore", message="^internal gelsd")

```

# Data import and cleaning

## Data Import


```python
df = pd.read_excel('E:/nikhitha/datasets/CGC/CGC Total Power comsumption.xlsx', sheetname='Sheet1') #loaded or readed the data

```

### View the Dataset

 df.head()

df.info()

## Removing the Unnecessary columns


```python
df1 =df.drop(columns = ["UOM","Type of Data", "Tag"]) # drop the unnecessary columns
```

## Finding Dimensions of data

df1.shape

This data consisting of 37 rows and 1181 columns,which is unstructed form, so we need to make them into structed form by converting rows to columns and vice versa

# Transpose of data

df1 = df1.T.reset_index() # transpose the dataset converting rows to colmns and columns to rows
df1.head()

 ### Assigning the first row of the dataset to  Column header

 header = df1.iloc[0] # assigning the first row of the dataset to header
 header

### Loading the data of all rows and columns

df1 = df1[1:] # loading the data of all rows and columns
df1.head()

### Assigning the column names to the transposed data set

df1 =df1.rename(columns = header)  # Assigning the column names to the transposed data set
df1.head()

# Renaming the Column names


```python
df1=df1.rename(columns={"Description": "DateTime"}) # renamimg the columns names

```


```python
df1.columns = df1.columns.str.replace(' ', '')
```


```python
df1.columns = df1.columns.str.replace('-', '')
```

### View the Column names

df1.columns

### Finding the Structure of data after transpose

df1. shape

After Transpose od data, we got 1180 rows and 38 columns

## Finding the datatype of variables

df1.dtypes

## Datatype Conversion


```python
a = ('1stStageSuctionTemperature','1stStageSuctionPressure','1stStageDischargeTemperature','1stStageDischargePressure','2ndStageSuctionTemperature','2ndStageSuctionPressure','2ndStageDischargeTemperature','2ndStageDischargePressure','3rdStageSuctionTemperature','3rdStageSuctionPressure','3rdStageDischargeTemperature','3rdStageDischargePressure','4thStageSuctionTemperature','4thStageSuctionPressure','4thStageDischargeTemperature', '4thStageDischargePressure','5thStageSuctionTemperature','5thStageSuctionPressure','5thStageDischargeTemperature','5thStageDischargePressure','1stStageDischargeFlow', '3rdStageDischargeFlow','5thStageDischargeFlow','C3SplitterPurgeto4thStageSuction','C2SplitterPurgeto5thStageSuction','CWSupplyTemperature','CWFlowtoOlefins','CWPressure','CompressorSpeed','UHPSteamFlowtoKT1','UHPSteamPressure','UHPSteamTemperature','HPSteamExtractionFlowfromKT1', 'HPSteamExtractionPressure','HPSteamExtractionTemperature','E24PGInletTemperature','TotalPower')
for i in a:
   # df1[i] =  df1[i].astype(float)
    df1[i] = pd.to_numeric(df1[i], errors = " Coerce")
```


```python
# Converting into datetime format
df1['DateTime'] =  pd.to_datetime(df1['DateTime'], format='%Y%m%d:%H:%M:%S.%f')
```

## Numerical variables

num_cols = df1._get_numeric_data().columns #finding the numerical data types in the dataset
num_cols

### Getting Datatypes of variables

df1.dtypes

## Finding the Missing Values

df1.isnull().sum()

CWSupplyTemperature:126,CWFlowtoOlefins:61,CWPressure:65,CompressorSpeed:9,UHPSteamFlowtoKT1:20,UHPSteamPressure:9,UHPSteamTemperature:9,HPSteamExtractionFlowfromKT1:11,HPSteamExtractionPressure:9,HPSteamExtractionTemperature:9,E24PGInletTemperature:13,C3SplitterPurgeto4thStageSuction:9,C2SplitterPurgeto5thStageSuction:9

## Drop the NA values


```python
df1 = df1.dropna()
```

df1.isnull().sum()

## Descriptive statistics

df1.describe()
