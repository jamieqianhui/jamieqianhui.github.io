---
layout: post
title:  "Exponential Smoothing Model for analyzing time series data"
date:   2022-03-06 15:53:58 +0800
categories: R TimeSeries
---

As part of my analytics master studies, I took a module which covered a topic on how to build an **exponential smoothing model** to help us make a judgment of whether the unofficial end of summer has gotten later in Atlanta, Georgia, United States. I've learnt a great deal from this course and would like to share some of the takeaways that I've understood from the module. In one of the weekly homework, we are tasked to determine whether the summer period has ended later over the 20 years, using daily high temperature data for Atlanta (July through October) and by coding in R. Click on *'Read more'* below to continue reading this post!

{: class="table-of-content"}
* TOC
{:toc}

Well, to honor the learning process, I will **not** be sharing the completed codes in R on how I finished the assignment. Instead, I will be sharing on the key concepts and logic flow on what I learnt, how I approach the assignment and eventually derived at the solution. A huge part of the content written about the ES model concept will be based on the course's lecture.


## Using Exponential Smoothing Model to determine temperature change (time series data)

### 1: Understanding Exponential Smoothing Model
The price of a stock every few seconds, daily sales of hamburgers at a fast food restaurant, and the highest temperature reading at the Atlanta Airport each day are some examples of time series data. These data values might have trends over time such as increasing when the economy's performance improves (higher stock price, higher burger sales, more human traffic at Atlanta Airport due to higher demand). These data values might also have cyclical variations such as having more burger sales on weekends than weekdays, or having higher temperatures in summer than in winter. Finally, another source of data variation is randomness. The data values might also vary simply due to random variations. Because of this randomness, it might be difficult to determine what is the expected baseline burger sales for the year's quarter. Hence, that's where exponential smoothing model will be helpful. 

Let's call `S_t` the expected baseline response for time period `t`. The expected summer temperature in Atlanta at hour `t` of the day, for example. Let's call `X_t` the observed response, the actual summer temperature in Atlanta measured at time `t`. If we want to figure out what the summer temperature actually is over time without all the random variations but the temperature today is different from yesterday's, what does that mean? Does that indicate an increase in the baseline or was it just due to randomness? 

There are 2 ways we might answer this question. 
1. We might think the observed temperature is a real indicator of the baseline. So, <br>
`S_t = X_t`

2. Or we might think there is no change to the baseline and the higher observed temperature today is just due to random luck. So, <br>
`S_t = S_t-1` 

(Which also means today's baseline is the same as yesterday's baseline)

The exponential smoothing method combines these 2 ideas.  <br>
`S_t = α*x_t + (1 - α)S_t-1` 
Where alpha, `α` is just a number between 0 and 1.

So if there is alot of randomness in the temperature system, then fluctuations are likely due to randomness and we should make alpha closer to 0. This is because yesterday's baseline temperature is probably a good indicator of today's baseline, even if we observed something different today. 

If there is not much randomness in the system, then we should make alpha close to 1. If we observed a fluctuation today, it likely means today's baseline is close to the observed data.

So, how do we start using the ES method? 
As the initial condition, we can choose `S_1 = X_1`

This method does not deal with trends (e.g. summer temperature increasing over the years) and cyclical variations yet. So let's dive into how to include the trends and cyclic variations into the ES model next.

### 2: Trends and Cyclic Effects

Let's call `T_t` the trend at time period `t`.
1. Our baseline `S_t = alpha*x_t + (1-alpha)(S_t-1 + T_t-1)`
2. With our previous estimate `S_t-1` now included a trend term `T_t-1` 
3. and we can estimate the new trend `T_t`, just like how we do for the baseline:

> `T_t = beta(S_t - S_t-1) + (1 - beta)(T_t-1)`

The initial condition, `T_1 = 0`

We can deal with cyclic patterns in the same way as trend, by making them an **additive** component of the formula (which is the right thing to do in some cases).
We can also deal with the cyclic patterns, which are also called seasonalities in a **multiplicative** way.

**Include both trend and seasonality:** <br>
`S_t = alpha*X_t / C_t-L  +  (1- alpha)(S_t-1 + T_t-1)`

`L` is the length of a cycle
`C_t` is the multiplicative seasonality factor for the time `t`. 
The seasonality factor will help us inflate or deflate the observation, based on the part of the cycle that time period `t` is in.

**For trend** <br>
The initial condition to find out what `C_t-L` is a the beginning, 
`T_1 = 0` (indicates no initial trend)

**For multiplicative seasonality** <br>
Multiplying by `1` shows no initial cylic effect and we need `L` of them, so the first `L` values of `C` are set to `1`

Depending on how many aspects like trend and seasonality is included, sometimes, this method is called single, double or triple exponential smoothing. 
Triple exponential smoothing with the base equation, plus trend an seasonality is also called Winter's Method, or Holt-Winters.

### 3. What does the name Exponential Smoothing mean
The exponential smoothing curve basically smooth out high peaks and valleys of a data set plotted as a graph. Every single past observation contributes to the current baseline estimate `S_t`. All the older data points are considered into the term `S_t-1`. <br>
Because `1 - alpha` is less than 1, newer obervations are weighted more than old observations. Exponential smoothing method accounts for all past observations, with the more recent observations being more important (with higher weights) to the current baseline estimate.
.
.
.
To be continued... ... (need to prepare for my mid-terms and will complete this post after that!)
