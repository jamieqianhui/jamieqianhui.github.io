---
layout: post
title:  "Data Wrangling with Pandas"
date:   2019-06-04 13:24:36 +0800
categories: Python Pandas
---
Sharing a few simple tips on data wrangling using `Python Pandas` library! Does having to clean messy excel datasets sound familiar to you? This post explains on how to convert dataframes from wide to long format, standardising column names and dividing column values evenly across duplicated Indexes. Click on the blog post title to find out more!<br>


**Step 1: Import the Pandas libraries** 

```python
import pandas as pd
```

**Step 2: Import excel and read as dataframe 'df'** 
```python
df = pd.read_excel('yourexcelfile.xlsx', sheet_name='Sheet1')
```
Let's take the dataframe of your monthly budget excel sheet (in wide format) to be the following:<br>
![DFwideFormat](DF_wideformat.png)
| Project Name    | Project I/D   | G/L Account   | Jan-19 | Feb-19 | ... | Dec-19|<br>
| --------------- | ------------- | ------------- | ------ | ------ | --- | ----- |<br>
| Office Space A  | 200589        | 1000400       |  $1600 |   $900 | ... | $1100 |<br>
| Office Space A  | 200589        | 8000800       |   $120 |   $100 | ... |  $200 |<br>
| Office Space B  | 320999        | 2222800       |  $3000 |  $3200 | ... | $3100 |


**Step 3: Convert df from wide to long format (gather columns into rows)** <br>
We will use pd.melt to gather columns into rows. First, identify all the columns which you want to retain (no changes made), these will be labelled as `id_vars`. Next, identify the column which you want to convert from columns to rows format, this will be labelled as `var_name`.
Then, assign a name to the value of your converted column as `value_name`.
```python
mdf = pd.melt (df, id_vars=["Project", "Project I/D"], 
	  var_name="Period", value_name= "Monthly Budget")
```

**Step 4: Replace '' spaces and `/` in mdf column names with `_` (underscores)** <br>
Let's standardise the column names with lower case and replacing all special characters with underscores

```python
mdf.columns = mdf.columns.str.strip().str.lower().str.replace(' ','_').str.replace('/','')
print(mdf.columns)
```
**Step 5: Create a new ID column by concatenating `Project Name`, `Project I/D` and `G/L Account`**<br>
Store the new ID column as `proj_gl_id`
```python
mdf['proj_gl_id'] = mdf['project_name'].map(str) +'-'+ mdf['project_id'].map(str) + '-' + mdf['gl_account'].map(str)
```
**Step 6: Split "material_group" column, expand it, stack it, then join back to the original mdf**
```python
sdf = mdf.drop('material_group', axis=1).join(mdf['material_group'].str.split(', ', expand=True).stack().reset_index(level=1, drop=True).rename('material_grp'))
```
**Step 7: Parse values in str to int**
```python
sdf['monthly_budget'] = pd.to_numeric(sdf['monthly_budget'], errors ='coerce')
```
**Step 8: Divide monthly budget value evenly across duplicated indexes**
```python
sdf['budget'] = sdf.groupby([sdf.index])['monthly_budget'].apply(lambda x: x / len(x))
```
**Step 9: Drop the 'wide format' monthly budget column**<br>
Store the updated dataset as `res`
```python
res = sdf.drop('monthly_budget',axis =1)
```
**Step 10: Export res to csv, removing index column**
```python
res.to_csv('Budget_2019.csv',index = False)
```
There you go, a clean dataframe in long format!

[Read More]: https://jamieqianhui.github.io/python/pandas/2019/06/04/Data-Wrangling-in-Python.html
