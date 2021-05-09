---
layout: post
title:  "Answers to HackerRank Practice Questions on Python"
date:   2021-05-09 16:41:36 +0800
categories: Python
---

One of the best ways to absorb and retain more of the new concepts and information that I have learnt about coding in `Python` is through documentation! As part of my journey to future-proof my data career by being more proficient in the python language and also to prepare for potential technical assessments/ interviews, I have been spending my free time solving coding challenges on HackerRank. 
In this blog post, I will share the answers to some of the practice questions which I have completed and successfully passed the code in the compiler on **HackerRank**. Do click on "Read More" or the title of this blog post for the solutions which I've created in `python`

{: class="table-of-content"}
* TOC
{:toc}

# Python Introduction Questions

## Python If-Else

**Task**
Given an integer, , perform the following conditional actions:

If `n` is odd, print Weird
If `n` is even and in the inclusive range of `2` to `5`, print Not Weird
If `n` is even and in the inclusive range of `6` to `20`, print Weird
If `n` is even and greater than `20`, print Not Weird

Input Format
A single line containing a positive integer, `n`.

Constraints
- `1 <= n <= 100 `

Output Format
Print `Weird` if the number is weird. Otherwise, print `Not Weird`.


**Answer:**
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
