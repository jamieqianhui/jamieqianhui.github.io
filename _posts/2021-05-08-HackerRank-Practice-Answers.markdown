#**SQL Basic Select** 

###Weather Observation Station 7

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

####Answer:

```MySql
SELECT DISTINCT CITY
FROM STATION
WHERE RIGHT(CITY,1) = 'a' OR
RIGHT(CITY,1) = 'e' OR
RIGHT(CITY,1) = 'i' OR
RIGHT(CITY,1) = 'o' OR
RIGHT(CITY,1) = 'u'
```
