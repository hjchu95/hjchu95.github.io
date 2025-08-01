---
layout: single
title: "Exercise 3-1. Autocovariance Functions (ACF) and White Noise Test"
author_profile: true
permalink: /projects/TS_Package_MATLAB/exercise3-1/
collection: projects
---
<br>
**[Link to Code]:** <a href="https://github.com/hjchu95/Time_Series_Package/blob/main/Exercises/ex3_1_ACF.m" target="_blank">ex3_1_ACF.m</a>

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

## Estimation of the Autocovariance and Autocorrelation Function
Mostly in economics, we mainly focus up to the second moment including the cross moment. Specifically, in time series, the covariance of the random variable's own history is called **autocovariance** which is formally defined as follows:

> **Definition 2. Autocovariance Function (ACF)**  
> If $$\{X_{t}:t\in\mathbb{Z}\}$$ is a process such that $$Var(X_{t})<\infty$$ for each $$t\in\mathbb{Z}$$, then the **autocovariance function** $$R_{X}(r,s)$$ of $$\{X_{t}\}$$ is defined as
> 
> $$\begin{equation}
>     R_{X}(r,s) = Cov(X_{r},X_{s})\text{ where }r\text{, }s\in\mathbb{Z}
> \end{equation}$$
>
> In other words, the autocovariance function implies the covariance of two members (observations) in a process.

Note that if one chooses another pair of members, say $$(r^{\prime},s^{\prime})$$, then the autocovariance will differ from that of $$(r,s)$$. Also, the restriction that $$Var(X_{t})<\infty$$ implies that the random variables for which the autocovariance function is defined must have finite second moments. This is because one cannot compare the autocovariance if random variables have infinite second moments, which is not the interest of time series.[^1]

Recall that the limit of covariance is that we cannot know the magnitude of the direction since it depends on the unit of measurement. As autocovariance suffers from a similar limitation, the definition of *autocorrelation*, which is a normalization of the autocovariance function, is introduced.

> **Definition 3. Autocorrelation Function**  
> The **autocorrelation function** of a random variable $$X$$ is defined as
>
> $$\begin{equation}
>   \rho_{X}(h) = \frac{R_{X}(h)}{R_{X}(0)}
> \end{equation}$$
>
> where $$R_{X}(0)$$ implies the variance of that variable.

Since one important assumption was that the error term (or shock process) is a *white noise process*, it is sometimes useful to estimate the autocovariance or autocorrelation function of a stochastic process and check whether it is a white noise process. Once data is given, it turns out that as the cross-sectional data case, we use sample moments as estimators. Two most popular estimators of the autocovariance function is as follows.

$$\begin{gather}
    \hat{R}(\tau) = \frac{1}{T}\sum_{t=1}^{T-|\tau|}{(X_{t}-\bar{X})(X_{t+|\tau|}-\bar{X})} \label{eq1} \tag{1} \\
    \hat{R}^{*}(\tau) = \frac{1}{T-|\tau|}\sum_{t=1}^{T-|\tau|}{(X_{t}-\bar{X})(X_{t+|\tau|}-\bar{X})} \label{eq2} \tag{2}
\end{gather}$$

Note that although (\ref{eq1}) and (\ref{eq2}) are both biased since $$\bar{X}$$, which is the sample mean, can be biased under a small sample size. Moreover, the bias will be bigger for (\ref{eq1}) although the bias is asymptotically negligible for both of them because if $$\tau$$ is small, $$1/(T-\tau)\approx 1/T$$ holds.

Using the estimators above, the estimator for the autocorrelation function is given as

$$\begin{equation}\label{eq3}
    \hat{\rho}(\tau) = \frac{\hat{R}(\tau)}{\hat{R}(0)} \tag{3}
\end{equation}$$

By collecting these autocorrelation functions for $$\tau=1,\cdots,h$$ periods, one finally obtains the autocorrelation function estimator for $$h$$ periods as follows:

$$\begin{equation}\label{eq4}
    \rho_{h} = \begin{pmatrix}
        \rho(1) \\
        \vdots \\
        \rho(h)
    \end{pmatrix} \tag{4}
\end{equation}$$

## White Noise Tests
### Simple White Noise Tests
Using the fact that a white noise process has $$\rho_{h}=0$$, i.e. no autocorrelation, one can derive the test statistic of the sample ACF and check whether a process is white noise. Since $$\rho_{h}=0$$, the asymptotic distribution of the sample ACF is as follows.

$$\begin{align*}
    & \sqrt{T}\cdot(\hat{\rho}_{h} - \rho_{h})\to^{d}\mathcal{N}(0,I_{h}) \\
    & \Rightarrow \hat{\rho}_{h} \to^{d}\mathcal{N}(0,\frac{1}{T}\cdot I_{h})
\end{align*}$$

Then the null and alternative hypothesis will be as follows.

$$\begin{align*}
    & H_{0}\text{: }\rho_{h}=0\text{; the process is white noise} \\
    & H_{1}\text{: }\rho_{h}\neq 0\text{; the process is not a white noise}
\end{align*}$$

Moreover, referring to Box et. al. (2015), the asymptotic standard error of the sample ACF is as follows.

$$\begin{equation}\label{eq5}
    se(\hat{\rho}_{h}) = \frac{1}{\sqrt{T}} \tag{5}
\end{equation}$$

Therefore, the confidence interval for the sample autocorrelation function is given by the two standard error bounds as follows:

$$\begin{equation}
    [-2\cdot\frac{1}{\sqrt{T}},+2\cdot\frac{1}{\sqrt{T}}] \tag{6}
\end{equation}$$

The simple white noise test, which checks whether the sample autocorrelation function falls within the two standard error bounds, is implemented in the following function that estimates the sample autocorrelation function.

> <p style="font-size:25px"><code>corr, bound = autocor(X, taumax=None,is_plot=None)</code></p>
><p style="font-size:15px">Estimating the Autocorrelation function (ACF) of a univariate process and testing a single hypothesis for a White-noise test.</p>  
> - **Inputs**:  
>   `X`: Objective of estimation (univariate)  
>   `taumax`: Maximum time lag (default = 20)  
>   `is_plot`: Option to control for the figure  
>    - 0 = omit figure  
>    - 1 = plot figure  
> - **Outputs**:  
>   `corr`: Estimated autocorrelation function, $$(\text{taumax}+1) \times 1$$  
>   `bound`: 2 standard error limits, Box et. al. (2015) pp. 33.

---

The `autocov` function, which is used within the `autocor` function above, is defined follows:

> <p style="font-size:25px"><code>cov = autocov(X, taumax=None)</code></p>
><p style="font-size:15px">Estimating the Autocovariance function (ACF) of a univariate process</p>  
> - **Inputs**:  
>   `X`: Objective of estimation (univariate)  
>   `taumax`: Maximum time lag (default = 20)  
> - **Outputs**:  
>   `cov`: Estimated autocovariance function, $$(\text{taumax}+1) \times 1$$  

### Example
<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex3/figure1.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: -20px; margin-bottom: 20px">
    Figure 1. Sample Autocorrelation Function of the CPI Inflation Rate of the United States
  </div>
</div>

Using the CPI inflation rate of the United States where $$T=260$$ (from 1960 Q2 to 2025 Q1), one can obtain **Figure 1** above. Note that the red dots in the stem plot is the ACF from 0 to 20, i.e. the default lag is 20 periods. One can observe that $$\hat{\rho}(0)$$ is one, which is in line with the definition of the sample autocorrelation function. The blue line is the confidence interval of the sample autocorrelation function under a 2 standard error limit. Using equation (\ref{eq5}) for the standard error, critical value as 2, and the confidence interval equation, the estimated confidence interval is as follows:

$$\begin{align}
    & [-c.v\cdot se(\hat{\rho}_{h}),+c.v\cdot se(\hat{\rho}_{h})] \\
    & \Rightarrow [-2\cdot\frac{1}{\sqrt{T}},+2\cdot\frac{1}{\sqrt{T}}] \\
    & \Rightarrow [-0.1240,+0.1240]
\end{align}$$

Interpreting the result of **Figure 1** above, one can say that the null hypothesis is rejected such that the CPI inflation rate of the United States is not a white noise process since all the ACFs are outside the confidence interval bound.

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex3/figure2.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: -20px; margin-bottom: 20px">
    Figure 2. Sample Autocorrelation Function of the Real GDP Growth Rate of the United States
  </div>
</div>

Can one then conclude that a process is white noise if all the sample autocorrelations (ACFs) fall within the confidence bounds? For example, consider **Figure 2**, which shows the estimated ACF and the corresponding confidence bounds for the real GDP growth rate of the United States. One can observe that all ACFs from lag 1 to lag 20 fall within the confidence bounds. Should we then conclude that the US real GDP growth rate follows a white noise process? 

In fact, this is not necessarily true. This is because the confidence bounds are derived from a single hypothesis test conducted at each individual lag. Even under the 2 standard error interval (equivalent to a 5 percent significance level), applying the test repeatedly across multiple lags does not imply that the null hypothesis for the entire process holds. This is due to the fact that each individual tests carries the risk of a Type 1 error (false rejection). Therefore, an alternative approach is to conduct a joint hypothesis test as follows.

### Joint White Noise Tests (Box-Pierce and Ljung-Box Test)
When conducting a joint hypothesis test to check whether the process is a white noise process, the null and alternative hypothesis is as follows.

$$\begin{align}
    H_{0}\text{: }\rho(1)=\rho(2)=\cdots=\rho(h) = 0 \\
    H_{1}\text{: }\rho(s)\neq 0\text{ for some }1\leq s\leq h
\end{align}$$

Then, the central limit theorem (CLT) leads to

$$\begin{equation}\label{eq7}
    \sqrt{T}\cdot(\hat{\rho}_{h} - \rho_{h})\to^{d}\mathcal{N}(0,I_{h}) \tag{7}
\end{equation}$$

Based on equation (\ref{eq7}) above, the test statistic for the joint hypothesis under the null hypothesis is given by

$$\begin{align}
    (\sqrt{T}\hat{\rho}_{h})^{\prime}(\sqrt{T}\hat{\rho}_{h}) & = T\cdot(\hat{\rho}_{x}(1)^{2} + \cdots + \hat{\rho}_{x}(h)^{2}) \\
    & \to^{d} \chi_{h}^{2}
\end{align}$$

since the sum of squared asymptotically standard normal random variables converges in distribution to a chi-squared distribution. Note that this is also called as the **Box-Pierce statistic**, which can be formally expressed as

$$\begin{equation}\label{eq8}
    Q = T\cdot\sum_{\tau=1}^{h}\hat{\rho}^{2}(\tau) \tag{8}
\end{equation}$$

where $$T$$ acts as the penalty term due to the number of information. However, as suggested by Davies (1979), some simulation studies have shown a poor performance of the Box-Pierce statistic. Therefore, an alternative is the **Ljung-Box statistic** which is as

$$\begin{equation}\label{eq9}
    Q = T\cdot(T+2)\cdot\sum_{\tau=1}^{h}{(T-\tau)^{-1}\cdot\hat{\rho}^{2}(\tau)} \tag{9}
\end{equation}$$

### Example
<table style="width: 50%; margin: auto; border-collapse: collapse;">
  <thead>
    <tr>
      <th style="text-align: center"></th>
      <th style="text-align: center;">Box-Pierce Test</th>
      <th style="text-align: center;">Ljung-Box Test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">Test Statistic</td>
      <td style="text-align: center;">914.91</td>
      <td style="text-align: center;">947.39</td>
    </tr>
    <tr>
      <td style="text-align: center;">p-value</td>
      <td style="text-align: center;">0.00</td>
      <td style="text-align: center;">0.00</td>
    </tr>
  </tbody>
</table>
<div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 20px; margin-bottom: 20px;">
  Table 1. Test Statistics of the BP and LB Q-test for the CPI Inflation Rate of the United States
</div>

Again, one can check whether the stochastic process is a white noise process using the Box-Pierce (BP) or Ljung-Box (LB) Q-test. For the CPI inflation rate of the United States, where $$T=260$$, the test statistics are reported in **Table 1** above. One can see that both the BP and LB Q-test reject the null hypothesis even at the conservative 1% significance level. This implies that the CPI inflation rate is not a white noise process.

<table style="width: 50%; margin: auto; border-collapse: collapse;">
  <thead>
    <tr>
      <th style="text-align: center"></th>
      <th style="text-align: center;">Box-Pierce Test</th>
      <th style="text-align: center;">Ljung-Box Test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">Test Statistic</td>
      <td style="text-align: center;">7.3017</td>
      <td style="text-align: center;">7.5961</td>
    </tr>
    <tr>
      <td style="text-align: center;">p-value</td>
      <td style="text-align: center;">0.9956</td>
      <td style="text-align: center;">0.9942</td>
    </tr>
  </tbody>
</table>
<div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 20px; margin-bottom: 20px;">
  Table 2. Test Statistics of the BP and LB Q-test for the Real GDP Growth Rate of the United States
</div>

On the other hand, the test statistics obtained from the BP and LB Q-tests for the real GDP growth rate of the United States are shown in **Table 2**. Now, both the BP and LB tests fail to reject the null hypothesis, even at the lenient 10% significance level. Thus, this can be interpreted as evidence that the real GDP growth rate of the United States behaves like a white noise process.

### Reference
- Box, G. E., Jenkins, G. M., Reinsel, G. C., & Ljung, G. M. (2015). "Time series analysis: forecasting and control". *John Wiley & Sons*.
- Davies, N. and Newbold, P. (1979). "Some power studies of a portmanteau test of time series model specification". *Biometrika*, 66(1), pp. 153–155.

[^1]: Indeed the definition of $$\infty$$ is that no matter what number you pick, it is strictly greater than that number, i.e. not comparable.

[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})