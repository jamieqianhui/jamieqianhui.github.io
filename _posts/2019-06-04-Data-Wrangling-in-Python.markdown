---
layout: post
title:  "Data Wrangling with Pandas"
date:   2019-06-04 13:24:36 +0800
categories: Python Pandas
---
Sharing a few simple tips on data wrangling using Python `Pandas` library! Does having to clean excel datasets that were manually maintained sounds familiar to you? This post will explain how to convert dataframes from wide to long format, standardising column names and dividing column values evenly across duplicated Indexes.
[Read More][Read More]

### Step 1: Import the required libraries 

```Javascript
import pandas as pd
```

### Step 2: Import excel and read as dataframe 'df' 
```Python
df = pd.read_excel('yourexcelfile.xlsx', sheet_name='Sheet1')
```
Let's take the dataframe of your excel sheet to be as follow:
> df = 

### Step 3: Convert df from wide to long format (gather columns into rows)
We will use pd.melt to gather columns into rows. Identify all the columns which you want to retain (no changes made), these will be labelled as `id_vars`. Identify the column which you want to convert from columns to rows format, this will be labelled as `var_name`.
Assign a name to the value of your converted column as `value_name`.
```Python
mdf = pd.melt (df, id_vars=["col 1", "col 2","col 3"], var_name="Period", value_name= "Monthly Budget")
```

### Step 3: Replace '' spaces and `/` in mdf column names with `_` (underscores)
Let's standardise the column names with lower case and replacing all special characters with underscores

```Python
mdf.columns = mdf.columns.str.strip().str.lower().str.replace(' ','_').str.replace('/','')
print(mdf.columns)
```
mdf['mg_id'] = mdf['co_code'].map(str) +'-'+ mdf['project'].map(str) + '-' + mdf['gl_account'].map(str)

### Step 4: Split "material_group" column, expand it, stack it, then join back to the original mdf
```Python
sdf = mdf.drop('material_group', axis=1).join(mdf['material_group'].str.split(', ', expand=True).stack().reset_index(level=1, drop=True).rename('material_grp'))
```
### Step 5: Parse values in str to int
```Python
sdf['monthly_budget'] = pd.to_numeric(sdf['monthly_budget'], errors ='coerce')
```
### Step 6: Divide monthly budget value evenly across duplicated indexes
```Python
sdf['budget'] = sdf.groupby([sdf.index])['monthly_budget'].apply(lambda x: x / len(x))
```
### Step 7: Drop monthly budget column
```Python
res = sdf.drop('monthly_budget',axis =1)
```
### Step 8: Export res to csv, removing index column
```Python
res.to_csv('Budget_2019.csv',index = False)
```
### There you go, a clean dataframe!

[Read More]: https://jamieqianhui.github.io/python/pandas/2019/06/04/Data-Wrangling-in-Python.html
