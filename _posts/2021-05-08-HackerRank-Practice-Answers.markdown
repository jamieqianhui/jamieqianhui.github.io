---
layout: post
title:  "Answers to HackerRank Practice Questions on SQL"
date:   2021-05-08 17:01:36 +0800
categories: MySQL
---
Documenting the answers to the practice questions which I have successfully completed and passed the code in the compiler on **HackerRank**. If you have not heard of HackerRank, it is a leading technical assessment platform used by hiring companies to conduct online coding tests and interviews aiming to choose the best among coding talents. Check out this blog post for my correct answers to the **`SQL`** Category on Basic and Advanced Select!


{: class="table-of-content"}
* TOC
{:toc}

# SQL Basic Select Questions

## Weather Observation Station

### Weather Observation Station 7

Query the list of **CITY** names ending with vowels `(a, e, i, o, u)` from **STATION**. Your result cannot contain duplicates.

The **STATION** table is described as follows:

**Field** | **Type** 
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

### Weather Observation Station 8

Query the list of **CITY** names from **STATION** which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

The **STATION** table is described as the same as the table above in *Weather Observation Station 7*.

**Answer:**

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE LEFT(CITY,1) IN ('a','e','i','o','u') AND RIGHT(CITY,1) IN ('a','e','i','o','u') 
```

### Weather Observation Station 9

Query the list of **CITY** names from **STATION** that do not start with vowels. Your result cannot contain duplicates.

The **STATION** table is described as the same as the table above in *Weather Observation Station 7*.

**Answer:**
```sql
SELECT DISTINCT CITY
FROM STATION 
WHERE LEFT(CITY,1) NOT IN ('a','e','i','o','u')
```


### Weather Observation Station 10

Query the list of **CITY** names from **STATION** that do not end with vowels. Your result cannot contain duplicates.

The **STATION** table is described as the same as the table above in *Weather Observation Station 7*.

**Answer:**
```sql
SELECT DISTINCT CITY
FROM STATION 
WHERE RIGHT(CITY,1) NOT IN ('a','e','i','o','u')
```

### Weather Observation Station 11

Query the list of `CITY` names from **STATION** that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

**Answer:**
```sql
SELECT DISTINCT CITY
FROM STATION 
WHERE LEFT(CITY,1) NOT IN ('a','e','i','o','u') OR RIGHT(CITY,1) NOT IN ('a','e','i','o','u')
```
### Weather Observation Station 12

Query the list of `CITY` names from `STATION` that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

**Answer:**
```sql
SELECT DISTINCT CITY
FROM STATION 
WHERE LEFT(CITY,1) NOT IN ('a','e','i','o','u') AND RIGHT(CITY,1) NOT IN ('a','e','i','o','u')
```

## Higher Than 75 Marks
Query the Name of any student in `STUDENTS` who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

The `STUDENTS` table is described as follows:  

| **ID** | **Name** | **Marks** |
|:------- |:--------|:----------|
 1  | Ashley | 81
 2 | Samantha | 75 
4 | Julia | 76 
 3 | Belvet | 84

The Name column only contains uppercase (A-Z) and lowercase (a-z) letters.

**Answer:**
```sql
SELECT Name
FROM STUDENTS
WHERE Marks > 75 
ORDER BY RIGHT(Name, 3), ID ASC
```
## Employee Salaries 
Write a query that prints a list of employee names (i.e.: the name attribute) for employees in `Employee` having a salary greater than `$2000` per month who have been employees for less than `10` months. Sort your result by ascending employee_id.

The Employee table containing employee data for a company is described as follows:

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.

Sample Output
```java
Angela
Michael
Todd
Joe
```
**Explanation**:
Angela has been an employee for `1` month and earns `$3443`  per month.
Michael has been an employee for `6` months and earns `$2017` per month.
Todd has been an employee for `5`  months and earns `$3396` per month.
Joe has been an employee for `9` months and earns `$3573` per month.

We order our output by ascending `employee_id`.

**Answer:**
```sql
SELECT name
FROM EMPLOYEE
WHERE salary > 2000 and months < 10
ORDER BY employee_id ASC
```

# SQL Advanced Select Questions

## Type of Triangle

Write a query identifying the type of each record in the `TRIANGLES` table using its three side lengths. Output one of the following statements for each record in the table:

- **Equilateral**: It's a triangle with `3` sides of equal length.
- **Isosceles**: It's a triangle with `2` sides of equal length.
- **Scalene**: It's a triangle with `3` sides of differing lengths.
- **Not A Triangle**: The given values of A, B, and C don't form a triangle.

**Answer:**
```sql
SELECT 
  CASE 
    WHEN A + B <= C OR A + C <= B OR B + C <= A THEN 'Not A Triangle'
    WHEN A = B AND B = C THEN 'Equilateral'
    WHEN A = B OR A = C OR B = C THEN 'Isosceles'
    ELSE 'Scalene'
  END
FROM TRIANGLES;
```

## The PADS 

Generate the following two result sets:

Query an alphabetically ordered list of all names in `OCCUPATIONS`, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: `AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).`
Query the number of ocurrences of each occupation in `OCCUPATIONS`. Sort the occurrences in ascending order, and output them in the following format:

```java
There are a total of [occupation_count] [occupation]s.
```
where [occupation_count] is the number of occurrences of an occupation in `OCCUPATIONS` and [occupation] is the **lowercase** occupation name. If more than one Occupation has the same [occupation_count], they should be **ordered alphabetically**.

*Note: There will be at least two entries in the table for each type of occupation.*

**Answer:**
```sql
SELECT CONCAT(Name,'(',LEFT(Occupation,1),')')
FROM OCCUPATIONS
ORDER BY Name ASC
;

SELECT CONCAT('There are a total of ', COUNT(Occupation), ' ', LOWER(Occupation), 's.')
FROM OCCUPATIONS
GROUP BY Occupation
ORDER BY COUNT(Occupation) , Occupation ASC
;
```
