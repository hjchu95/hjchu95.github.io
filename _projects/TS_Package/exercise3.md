---
layout: single
title: "Exercise 3. Autocovariance Functions (ACF) and Autoregressive Moving Average (ARMA) Models"
author_profile: true
permalink: /projects/TS_Package_MATLAB/exercise3/
collection: projects
---
<br>
**[Link to Code]:** <a href="https://github.com/hjchu95/Time_Series_Package/blob/main/Exercises/ex2_ACF_AR.m" target="_blank">ex2_ACF_AR.m</a>  
**[Link to Lecture Note]:** <a href="https://github.com/hjchu95/Time_Series_Package/blob/main/Exercises/ex1_1_PlotData_US.m" target="_blank">3. ACF and ARMA.pdf</a>  

## White Noise Process
In time series analysis, observations are typically dependent across time, violating the usual assumption in linear regression models that the error terms are independently and identically distributed (i.i.d). To address this issue, time series models commonly assume that the error terms follow a **white noise process**, which is slightly more lenient assumption than i.i.d. The formal definition of a white noise process is as follows:

> **Definition 1. White Noise Process**
> A sequence of random variables $$\{X_{t}\}$$ is a **white noise process** if its mean is zero and has a autocovariance function such that
>
> $$\begin{equation}
>     R_{X}(h) = \begin{cases}
>        \sigma^{2} & \text{if }h=0 \\
>        0 & \text{otherwise}
>     \end{cases}
> \end{equation}$$
>
> This is denoted as
>
> $$\begin{equation}
>   \{X_{t}\}\sim WN(0,\sigma^{2})
> \end{equation}$$
>
> In words, a white noise process is simply a process with no time dependence, i.e. we do not care about the distribution but only care about the correlation (or covariance). Therefore, a process that is not i.i.d but has the same autocovariance as the i.i.d process is called the white noise process.

## Estimation of the Autocovariance Function


## Autoregressive Moving Average Process

[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})