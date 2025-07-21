---
layout: single
title: "Exercise 3. Autocovariance Functions (ACF) and Autoregressive Moving Average (ARMA) Models"
author_profile: true
permalink: /projects/TS_Package_MATLAB/exercise3/
collection: projects
---
<br>
**[Link to Code]:** <a href="https://github.com/hjchu95/Time_Series_Package/blob/main/Exercises/ex1_1_PlotData_US.m" target="_blank">ex2_ACF_AR.m</a>

## Linear Model and Stationarity
Recall that a *linear regression model*, the most widely used framework in econometrics, is expressed as follows:[^1]

$$\begin{equation}\label{eq1}
    y_{t} = \beta_{0} + \beta_{1}x_{1t} + \beta_{2}x_{2t} + \cdots + \beta_{k}x_{kt} + u_{t}\text{, }u_{t}\sim iid(0,\sigma^{2}) \tag{1}
\end{equation}$$

**Time series data** is defined as a set of quantitative observations arranged in chronological order, where time is assumed to be discrete. Formally, time series data are referred to as a **stochastic process**, which is a sequence of random variables defined as follows.

> **Definition 1. Stochastic Process**  
> Suppose $$t\in \mathcal{T}$$ is a element in the time index set and $$\omega\in\Omega$$ is a element in the sample space. A **stochastic process** is a family (collection) of random variables $$\{X_{t}(\omega),t\in\mathcal{T}\text{, }\omega\in\Omega\}$$ defined in a probability space $$(\Omega,\mathcal{F},P)$$.

In this sense, a stochastic process is a function of two arguments: an element of the time index space and an element of the sample space. Put differently, *a stochastic process is simply a collection of random variables indexed by time*. Because a stochastic process is realized in time order, the ordering of observations plays a crucial role in time series analysis, which distinguishes it from randomly sampled cross-sectional data. Due to this time ordering, observations in time series data are inherently connected, meaning that the random variables exhibit correlation over time. This phenomenon is referred to as **serial correlation** or **time dependence**. Consequently, this lead to the need of a simple but flexible model that can effectively capture the time dependence among random variables.

One crucial assumption violated in equation (1) is that the error term is independently and identically distributed (i.i.d.). Formally, independence and identical distribution are each defined as follows:

> **Definition 2. Independence**  
> Let random variables $$X$$ and $$Y$$ follow a joint probability distribution $$f_{XY}(x,y)$$. Then $$X$$ and $$Y$$ are said to be **independent** if and only if
>
>$$\begin{equation}
    f_{XY}(x,y) = f_{X}(x)\cdot f_{Y}(y)
\end{equation}$$
>
>where $$f_{X}(x)$$ and $$f_{Y}(y)$$ denote the marginal probability density functions of $$X$$ and $$Y$$, respectively.

> **Definition 3. Identically Distributed**  
> Random variables $$X$$ and $$Y$$ are said to be **identically distributed** if their probability density functions, $$f_{X}(x)$$ and $$f_{Y}(y)$$, are identical. In other words, they share the same probability distribution.

In time series analysis, each variable is heavily time dependent since each observation is related to one another (recall that the chronological ordering is important). s


## White Noise Process

## Estimation of the Autocovariance Function

## Autoregressive Moving Average Process

[^1]: Note that the subscript $$t$$ can be changed to $$i$$. Generally, the subscript $$t$$ is used in cases related to "time series" where the sample size is denoted as $$T$$, while the subscript $$i$$ is used in cases using "cross-sectional" data where the sample size is denoted as $$N$$.

[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})