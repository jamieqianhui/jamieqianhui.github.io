---
layout: post
title:  "Data Wrangling with Transact-SQL"
date:   2019-06-05 13:24:36 +0800
categories: t-SQL
---
Wondering how to build data wrangling pipelines in t-SQL? This post explains on how to convert `nvarchar` to `date` and `decimal` format, as well as **pivoting** the data from long to wide format. Click on the blog post title to find out more!<br>


Let's take the dataframe of your database table (in long format) to be the following:<br>
![tab_longformat]({{ '/assets/tab_longformat.PNG' | relative_url }}) 

The format of the dataframe are all in `nvarchar(100)`. In order to do any calculation based on date and amount $, we will have to convert the format accordingly. <br>

**Step 1: Convert nvarchar for 'Date of Rent Collected' column to date format** <br> 
First, we need to set the data into `YYYY-MM-DD HH:MM:SS` format then parse `nvarchar` to `datetime` format.
```sql
 SELECT CONVERT(DATETIME, 
  			SUBSTRING([Date of Rent Collected], 7, 4) + '-' + SUBSTRING([Date of Rent Collected], 4, 2) + '-' + SUBSTRING([Date of Rent Collected],1, 2) 
  			+ ' ' + 
  			SUBSTRING([Date of Rent Collected], 12, 2) + ':' + SUBSTRING([Date of Rent Collected], 15, 2) + ':' + SUBSTRING([Date of Rent Collected], 18, 2), 120) 
  			AS [date_rent_collected]
 
 FROM 	dbo.TAB_Rent_LongFormat
```
Now, we will be able to order the dataset based on datetime:
```sql
 SELECT [date_rent_collected]
 FROM 	dbo.TAB_Rent_LongFormat
 ORDER BY [date_rent_collected]
```
The output will look like this: <br>
![tab_dateformat]({{ '/assets/tab_dateformat.PNG' | relative_url }})  <br>


Next, if we need to sum up the total rent amount collected for each project, we will have to convert `nvarchar` amount to `decimal`: 
<br>
**Step 2: Convert nvarchar for 'Rent Amount' to decimal** <br>
The special characters $ and ',' will need to be replaced with ''
```sql
 SELECT CAST(REPLACE(LEFT(
 						   REPLACE(LEFT([Rent Amount], LEN([Rent Amount]) - 3), ',', ''), '$', '')
                           AS decimal(18, 2)) AS [Gross Rent]
 FROM 	dbo.TAB_Rent_LongFormat
```

**Step 3: Pivot dataset from long to wide format (gather rows into columns)** <br>

```sql
 SELECT [Project], [date_rent_collected], [Currency],
 		p.[Furniture & Fittings] AS [FF]
 		p.[Area]                 AS [Area]
 		p.[Service]			  	 AS [Service]
 		p.[Maintenance Charge]   AS [MC]
 FROM 
 	( SELECT [Project], [date_rent_collected], [Rent Type], [Rent Amount] [Currency],
 		FROM 	dbo.TAB_Rent_LongFormat ) t

 PIVOT 
 ( SUM([Rent Amount])
 	FOR [Rent Type] IN ([Furniture & Fittings],[Area],[Service],[Maintenance Charge])
 	) as p
```

There you go, a clean dataframe in wide format! <br>
