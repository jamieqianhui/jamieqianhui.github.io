---
layout: post
title:  "Answers to HackerRank Practice Qns on SQL"
date:   2021-05-08 17:01:36 +0800
categories: SQL
---
Documenting the answers to the practice questions which I have successfully completed on HackerRank. If you have not heard of HackerRank, it is a leading technical assessment platform used by hiring companies to conduct online coding Tests and interviews aiming to choose the best among coding talents. Check out this blog post for the answers to the `SQL` Category on Basic Select!


{: class="table-of-content"}
* TOC
{:toc}

# **SQL Basic Select** 

### Weather Observation Station 7

Query the list of **CITY** names ending with vowels (a, e, i, o, u) from **STATION**. Your result cannot contain duplicates.

Input Format

The **STATION** table is described as follows:

| **Field** | **Type** |
| ------------- | ------------- |
| ID  | NUMBER |
| CITY  | VARCHAR2(21)  |
| STATE  | VARCHAR2(2)  |
| LAT_N  | NUMBER  |
| LONG_W | NUMBER  |

where LAT_N is the northern latitude and LONG_W is the western longitude.

#### Answer:

```MySql
SELECT DISTINCT CITY
FROM STATION
WHERE RIGHT(CITY,1) = 'a' OR
RIGHT(CITY,1) = 'e' OR
RIGHT(CITY,1) = 'i' OR
RIGHT(CITY,1) = 'o' OR
RIGHT(CITY,1) = 'u'
```
