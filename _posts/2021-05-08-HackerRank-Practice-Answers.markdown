---
layout: post
title:  "Answers to HackerRank Practice Questions on SQL"
date:   2021-05-08 17:01:36 +0800
categories: MySQL
---
Documenting the answers to the practice questions which I have successfully completed and passed the code in the compiler on **HackerRank**. If you have not heard of HackerRank, it is a leading technical assessment platform used by hiring companies to conduct online coding tests and interviews aiming to choose the best among coding talents. Check out this blog post for my correct answers to the **`SQL`** Category on Basic Select!


{: class="table-of-content"}
* TOC
{:toc}

**SQL Basic Select** 

## Weather Observation Station 7

Query the list of **CITY** names ending with vowels `(a, e, i, o, u)` from **STATION**. Your result cannot contain duplicates.

Input Format

The **STATION** table is described as follows:

| **Field** | **Type** |
|:------- |:----------|
 ID  | NUMBER 
 CITY  | VARCHAR2(21) 
 STATE  | VARCHAR2(2)  
 LAT_N  | NUMBER  
 LONG_W | NUMBER  

where LAT_N is the northern latitude and LONG_W is the western longitude.

**Answer:**
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE RIGHT(CITY,1) IN ('a','e','i','o','u')
```

Alternatively, this answer is acceptable too albeit a less efficient syntax:
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE RIGHT(CITY,1) = 'a' OR
RIGHT(CITY,1) = 'e' OR
RIGHT(CITY,1) = 'i' OR
RIGHT(CITY,1) = 'o' OR
RIGHT(CITY,1) = 'u'
```

## Weather Observation Station 8

Query the list of **CITY** names from **STATION** which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

The **STATION** table is described as the same as the table above in *Weather Observation Station 7*.

**Answer:**

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE LEFT(CITY,1) IN ('a','e','i','o','u') AND RIGHT(CITY,1) IN ('a','e','i','o','u') 
```

## Weather Observation Station 9

Query the list of **CITY** names from **STATION** that do not start with vowels. Your result cannot contain duplicates.

The **STATION** table is described as the same as the table above in *Weather Observation Station 7*.

**Answer:**
```sql
SELECT DISTINCT CITY
FROM STATION 
WHERE LEFT(CITY,1) NOT IN ('a','e','i','o','u')
```


## Weather Observation Station 10

Query the list of **CITY** names from **STATION** that do not end with vowels. Your result cannot contain duplicates.

The **STATION** table is described as the same as the table above in *Weather Observation Station 7*.

**Answer:**
```sql
SELECT DISTINCT CITY
FROM STATION 
WHERE RIGHT(CITY,1) NOT IN ('a','e','i','o','u')
```

## Weather Observation Station 11

Query the list of `CITY` names from **STATION** that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

**Answer:**
```sql
SELECT DISTINCT CITY
FROM STATION 
WHERE LEFT(CITY,1) NOT IN ('a','e','i','o','u') OR RIGHT(CITY,1) NOT IN ('a','e','i','o','u')
```
## Weather Observation Station 12

Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

**Answer:**
```sql

SELECT DISTINCT CITY
FROM STATION 
WHERE LEFT(CITY,1) NOT IN ('a','e','i','o','u') AND RIGHT(CITY,1) NOT IN ('a','e','i','o','u')
```
