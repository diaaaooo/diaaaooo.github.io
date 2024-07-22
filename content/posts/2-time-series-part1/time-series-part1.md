---
title: "Time Series Part 1"
date: 2024-07-22T00:00:00+00:00
# weight: 1
# aliases: ["/first"]
tags: ["tag"]
author: 🐶
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: true
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: true
UseHugoToc: true
math: mathjax
# menu:
#   main:
#     identifier: "posts"
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

Looking into time series lately and accumulated some notes to put down. 

## Time Series Types
There are two types of time series[1]:
- **Univirate time series:** focusing on a single time series. Most of time series analysis and models only handle univirate time series, like ARIMA. 
- **Multivariate time series:** focusing on relationships and interactions between two or more time series. Some models can handle such relationships, such as DeepAR.

## Time Series Models (subject to change)
The content in this section is subject to change. The following categories are only based on my current limited understanding of time series models. 

In general, time series models can be grouped into the following categories[1,2]:
### Statistical models
- **Classic models:** This group of models rely on using past values and past errors/residuals to predict present value. ARIMA models belong to this group. They cannot handle trends, seasonalities or cycles and usually assume and require time series values to be stationary. 
- **Regression-based models:** This group of models use time values as x variable and time series values as y variable. They usually can handle linear trends and assume linear trend within the time series.
- **Exponential smoothing models:** This group of models use weighted averages of past values to smoothe or reduce the noise of time series, and the weights decay exponentiallu as the values get older in time. 
- **Prophect:** This open-sourced model family is developed by Facebook. They have built-in support for trend, seasonality, cycle and holiday effects. 

### Machine learning models
- **LSTM**
- **DeepAR**

## Time Series Patterns

When looking at time series data, here are what we are trying to find[1]:
- Is there a **trend**, meaning that, on average, the values tend to increase or decrease over time?
- Is there a **seasonality**, meaning that there is a regular repeating pattern of hights and lows related to calendar time such as seasons, qyarters, months, days of the week, and so on? 
- Is there a long-run **cycle** or period unrelated to seasonality factors? 
- Is there **constant variance** over time, or is the variance non-constant?
- Are there **outliers**? In regression, outliers are far away from your line. While time series data, your outliers are far away from your other data.
- Are there any **abrupt changes** to either the level (mean) of the series or the variance? 

## Autoregressive (AR)
When talking about **Autoregresstive** term, you are talking about lags (or **order** in statistical terms). 

Let's look at an example for **AR(1)**. 1 means the 1st order of autoregressive, which means take the value as lag of 1. 

| Time (t) | Temperature Today (\\(x_t\\)) | Temperature Yesterday (\\(x_{t-1}\\)) |
|----------|-----------------------------|-------------------------------------|
| 1        | 15                          | 14                                  |
| 2        | 14                          | 15                                  |
| 3        | 16                          | 14                                  |
| 4        | 17                          | 16                                  |
| 5        | 18                          | 17                                  |

The **AR(1)** model states that today's temperature can be predicted using yesterday's temperature plus some random variation. 

Theoretically, an **AR(1)** is written like this:
$$
\ x_t = \alpha + \beta x_{t-1} + \epsilon_t \
$$
where:
- \\( x_t \\) is the temperature today.
- \\( \alpha \\) is the constant or intercept or bias.
- \\( \beta \\) is the slop or coefficient that determines the influence of yesterday's temperature.
- \\( \epsilon_t \\) is the error term.

AR(p) models have some assumptions:
- The error term \\( \epsilon_t \\) assums that the errors are independtly distributed with a normal distribution that has mean 0 and constant variance. (Todo: add a residual plot as to show an example)
- Errors are independent of observations \\( x \\). 

Back to the **AR(1)** example. Looking at the formula, you can see **AR(1)** actually represents a basic linear regression line. An AR model is basically a linear regression of time sereis \\( x \\) against past values. The only difference is:
- Regression assumes \\( x \\) values are independent.
- **AR(1)** accounts for the temporal dependence between \\( x_t \\) and \\( x_{t-1} \\).


## Moving Average (MA)
When talking about **Moving Average**, you are talking about moving average on past errors/residuals.

Let's look at an example of **MA(1)**. 1 means taking moving average against 1 past error. The errors are not the difference between observed values. They are calculated as \\[ \epsilon_t = \mu + \theta \epsilon_{t-1} \\].

| Time (t) | Temperature Today (\\(x_t\\)) | Error Today (\\(\epsilon_t\\)) | Error Yesterday (\\(\epsilon_{t-1}\\)) |
|----------|-----------------------------|------------------------------|-------------------------------------|
| 1        | 15                          | 0                            | 0                                   |
| 2        | 16                          | 1                            | 0                                   |
| 3        | 15                          | -0.6                         | 1                                   |
| 4        | 17                          | 2.36                         | -0.6                                |
| 5        | 14                          | -2.416                       | 2.36                                |

The **MA(1)** model states that today's value can be predicted using the mean of the series plus the random error term from today and the previous day's error term. 

Theoratically, an **MA(1)** model is written as:

\\[ x_t = \mu + \epsilon_t + \theta \epsilon_{t-1} \\]

where:
- \\( x_t \\) is the value at time \\( t \\).
- \\( \mu \\) is the mean of the series.
- \\( \epsilon_t \\) is the error term at time \\( t \\).
- \\( \theta \\) is a coefficient that determines the influence of the previous error term \\( \epsilon_{t-1} \\).

And the formula for **MA(2)** is:

\\[ x_t = \mu + \epsilon_t + \theta_1 \epsilon_{t-1} + \theta_2 \epsilon_{t-2} \\]

In a way, **MA(q)** models can be seen as a linear regression of time sereis \\( x_t \\) against past error terms. In an **MA(q)** model, the current value of the time series is expressed as a linear combination of the mean, the current error term, and q previous error terms.

## Takeaway

- **AR(p)** models can be seen as a linear regression of time series \\( x_t \\) against past values.
- **MA(q)** models can be seen as a linear regression of time sereis \\( x_t \\) against past error terms where the intercept is \\( \mu \\) the mean of the series. 


## References

[1] PennState. “[STAT510 Applied Time Series Analysis](https://online.stat.psu.edu/stat510/lesson/1)" 
[2] Weights & Biases. “[A Gentle Introduction To Time Series Analysis & Forecasting](https://wandb.ai/site/articles/a-gentle-introduction-to-time-series-analysis-forecasting)" 



