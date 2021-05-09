---
layout: post
title:  "Solutions to HackerRank Coding Challenges in Python"
date:   2021-05-09 16:41:36 +0800
categories: Python 3
---

One of the best ways to absorb and retain more of the new concepts that I have learnt about coding in `Python` is through documentation! As part of my journey to future-proof my data career by levelling up my proficiency in the python language and also to prepare for potential technical interviews, I have been spending my free time solving coding challenges on [HackerRank][hackerrank]. 
In this blog post, I will share the solutions to some of the practice challenges which I have completed and successfully passed the code in the compiler on **HackerRank**. Do click on *Read More* or the title of this blog post for the Python 3 solutions created by me.

{: class="table-of-content"}
* TOC
{:toc}

# Python Introduction (Easy) Questions

## If-Else

**Task**

Given an integer, `n` , perform the following conditional actions:

- If `n` is odd, print Weird
- If `n` is even and in the inclusive range of `2` to `5`, print Not Weird
- If `n` is even and in the inclusive range of `6` to `20`, print Weird
- If `n` is even and greater than `20`, print Not Weird

*Input Format:* A single line containing a positive integer, `n`.

Constraints:
- `1 <= n <= 100 `

*Output Format:* Print `Weird` if the number is weird. Otherwise, print `Not Weird`.


**Solution:**
```python
#!/bin/python3

import math
import os
import random
import re
import sys



if __name__ == '__main__':
    n = int(input().strip())
    # First we use modulus % operator to find the odd numbers and label them as 'Weird'. Odd numbers will return a remainder that is not zero.
    if n%2 != 0:
        print("Weird")
    # Next we find the criteria for the rest of the integer as stated
    else :
        if(n>=2 and n<=5):
            print("Not Weird")
        elif(n>=6 and n<=20):
            print("Weird")
        elif(n>20):
            print("Not Weird")
    
```

## Arithmetic Operators

**Task**

The provided code stub reads two integers from STDIN, `a` and `b` . Add code to print three lines where:

1. The first line contains the sum of the two numbers.
2. The second line contains the difference of the two numbers (first - second).
3. The third line contains the product of the two numbers.

Example:

`a = 3`

`b = 5`

Print the following:
```java
8
-2
15
```
*Input Format:* The first line contains the first integer, `a`. The second line contains the second integer, `b`.

*Output Format:* Print the three lines as explained above.

Sample Input 0
```java
3
2
```
Sample Output 0
```java
5
1
6
```

**Solution:**
```python
if __name__ == '__main__':
    a = int(input())
    b = int(input())
    
    print(a + b)
    print(a - b)
    print(a * b)
```

## Division

**Task**

The provided code stub reads two integers from STDIN, `a` and `b` . Add logic to print two lines. The first line should contain the result of integer division, `a//b` . The second line should contain the result of float division,  `a/b` .

No rounding or formatting is necessary.

Example:

`a = 3`

`b = 5 `

- The result of the integer division `3//5 = 0`.
- The result of the float division is `3/5 = 0.6`.

Print:
```java
0
0.6
```

**Input Format**

The first line contains the first integer, `a` .
The second line contains the second integer, `b` .

**Output Format**

Print the two lines as described above.

**Solution:**
```python
if __name__ == '__main__':
    a = int(input())
    b = int(input())
    
    print(a//b)
    print(a/b)
```

## Loops

**Task**

The provided code stub reads and integer,`n`, from STDIN. For all non-negative integers `i < n` , print `i**2`.

Example

`n = 3`

The list of non-negative integers that are less than `n = 3` is `[0,1,2]` . Print the square of each number on a separate line.
```java
0
1
4
```
*Input Format:* The first and only line contains the integer, `n`.

*Constraints:* `1 <= n <= 20`

*Output Format:* Print `n` lines, one corresponding to each `i`.

Sample Input 0
```java
5
```
Sample Output 0
```java
0
1
4
9
16
```

**Solution:**
```python
if __name__ == '__main__':
    n = int(input())

for i in range(n):
    print (i ** 2)
```

[hackerrank]: https://www.hackerrank.com/dashboard
