---
layout: single
title: "Exercise 3-2. Autoregressive Models with Order P"
author_profile: true
permalink: /projects/TS_Package_MATLAB/exercise3-2/
collection: projects
---
<br>
**[Link to Code]:** <a href="https://github.com/hjchu95/Time_Series_Package/blob/main/Exercises/ex3_2_AR.m" target="_blank">ex3_2_AR.m</a>  
<!-- **[Link to Lecture Note]:** <a href="https://github.com/hjchu95/Time_Series_Package/blob/main/Exercises/ex1_1_PlotData_US.m" target="_blank">3. ACF and ARMA.pdf</a>   -->

## Autoregressive Model of Order (p)
### The AR(p) Process
One of the most commonly used models for a univariate time series is the autoregressive model of order (p), denoted by AR(p). In an autoregressive model, the current value of a stochastic process is explained by its own autoregressive terms of lag p.

Formally, an AR(p) process $$y_{t}$$ is defined as

$$\begin{equation}\label{eq1}
    y_{t} = v+\alpha_{1}y_{t-1} + \cdots + \alpha_{p}y_{t-p}+e_{t}\qquad e_{t}\sim WN(0,\sigma^{2}) \tag{1}
\end{equation}$$

where $$v$$ is an intercept, $$(\alpha_{1},\cdots,\alpha_{p})$$ are the autoregressive coefficients, and $$e_{t}$$ is a white noise innovation.

The model can also be expressed using the lag operator such as

$$\begin{equation*}
    \alpha(L)y_{t} = v+e_{t}
\end{equation*}$$

where $$\alpha(L)=(1-\alpha_{1}L-\cdots-\alpha_{L}L^{p})$$.

The AR(p) model has the following characteristics:
* Causal-stationarity

    An AR(p) process is causal and covariance stationary when all roots of the characteristic equation

    $$\begin{equation*}
        1-\alpha_{1}z-\cdots-\alpha_{p}z^{p}=0
    \end{equation*}$$

    lie outside the unit circle. In other words, every root $$(z_{j})$$ must satisfy

    $$\begin{equation*}
        |z_{j}|>1
    \end{equation*}$$

    Under this condition, the AR(p) process can be represented as an infinite moving-average process:

    $$\begin{equation*}
        \sum_{j=0}^{\infty}{\psi_{j}e_{t-j}}
    \end{equation*}$$

    where the coefficients $$(\psi_{j})$$ decay as $$j$$ increases.

* Intercept and Unconditional Mean

    The intercept term $$v$$ implies a nonzero unconditional mean. This can be shown as follows. Taking the expectations on both sides of equation $$\eqref{eq1}$$ gives

    $$\begin{align*}
        & \mathbb{E}[y_{t}] = v+\alpha_{1}\mathbb{E}[y_{t-1}] + \cdots + \alpha_{p}\mathbb{E}[y_{t-p}] + \mathbb{E}[e_{t}] \\
        & \Rightarrow (1-\alpha_{1}-\cdots-\alpha_{p})\mathbb{E}[y_{t}] = v
    \end{align*}$$

    where the last equality holds since $$y_{t}$$ is covariance stationary so that $$\mathbb{E}[y_{t}]=\cdots=\mathbb{E}[y_{t-p}]$$ and $$\mathbb{E}[e_{t}]=0$$ since $$e_{t}$$ is $$WN(0,\sigma^{2})$$.
    An alternative approach is to remove the sample mean from the data before estimating the model. In that case, the demeaned process is modeled without an intercept such as

    $$\begin{equation*}
        (y_{t}-\bar{y})= \alpha_{1}(y_{t}-\bar{y}) + \cdots + \alpha_{p}(y_{t}-\bar{y}) + e_{t}
    \end{equation*}$$

The `OLS_ARp` function uses this alternative approach. It automatically demeans the input variable `y` before estimating the AR(p) model. When forecasts are constructed, the sample mean removed during the demeaning procedure is added back to the predicted values.

### Estimation of AR(p) Process
When estimating the AR(p) process, there are two ways: using the (1) OLS method and (2) MLE method.
### (1) Ordinary Least Squares (OLS)
For observations $$(t=p+1,\ldots,T)$$, the AR((p)) model can be written as

$$\begin{equation*}
Y=X\beta+u,
\end{equation*}$$

where

$$\begin{equation*}
Y=\begin{bmatrix}
y_{p+1}\\
y_{p+2}\\
\vdots\\
y_T
\end{bmatrix},\qquad X=\begin{bmatrix}
1 & y_p & y_{p-1} & \cdots & y_1\\
1 & y_{p+1} & y_p & \cdots & y_2\\
\vdots & \vdots & \vdots & \ddots & \vdots\\
1 & y_{T-1} & y_{T-2} & \cdots & y_{T-p}
\end{bmatrix},\qquad\beta=\begin{bmatrix}
v & \alpha_1 & \alpha_2 & \cdots & \alpha_p
\end{bmatrix}^{\prime}.
\end{equation*}$$

Thus, the OLS estimator is

$$\begin{equation*}
\hat{\beta}=(X^{\prime}X)^{-1}X^{\prime}Y.
\end{equation*}$$

When the series is demeaned before the estimation, the intercept column is omitted from $$X$$, and only the autoregressive coefficients are estimated.

### (2) Maximum Likelihood Estimation (MLE)
Assume that the innovations are independently and normally distributions such that

$$\begin{equation*}
    e_{t}\sim \text{iid}\mathcal{N}(0,\sigma^{2})
\end{equation*}$$

Conditional on the first $$p$$ observations, the residual at period $$t$$ is

The `OLS_ARp` function estimates an AR(p) model by the OLS method.

> <p style="font-size:25px"><code>`phi_hat, sig2_hat, F, Y0, Y_lag, y_hat, u_hat, Y_predm = OLS_ARp(y, p, h)</code></p>
><p style="font-size:15px">Estimation of the AR(p) Model using OLS</p>  
> - **Inputs**:  
>   `y`: Objective of estimation (univariate)  
>   `p`: Lag of AR(p) Model  
>   `H`: Maximum forecasting horizon, does not forecast if None  
> - **Outputs**:  
>   `phi_hat`: OLS estimator  
>   `sig2_hat`: Variance-covariance matrix estimator  
>   `F`: Companion form of OLS estimators  
>   `Y0`: Response variable used in estimation  
>   `Y_lag`: Explanatory variables used in estimation  
>   `y_hat`: Fitted values of OLS  
>   `u_hat`: Residuals of OLS  
>   `Y_predm`: Predicted value  




[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})