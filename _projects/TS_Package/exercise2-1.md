---
layout: single
title: "Exercise 2-1. Plotting Macroeconomic data of the US"
author_profile: true
permalink: /projects/TS_Package_MATLAB/exercise2-1/
collection: projects
---
<br>
**[Link to Code]:** <a href="https://github.com/hjchu95/Time_Series_Package/blob/main/Exercises/ex1_1_PlotData_US.m" target="_blank">ex1_1_PlotData_US.m</a>

In this exercise, we will plot several macroeconomic variables for the United States and use these plots to introduce time series data and key macroeconomic indicators. Specifically, we will cover the concept of seasonality in time series data, the identity relationship between real GDP, nominal GDP, and the implicit price deflator (GDP deflator), differences between various price indices, labor market indicators and Okun's law.

## Annualization
&emsp;Before diving into the details, it is important to note that the quarterly nominal and real GDP data (`GDP` and `GDPC1`) obtained from FRED are reported at annualized rates. This means that the quarterly values are multiplied by four to express what the total would be if the level of economic activity observed in that quarter were maintained for an entire year.

&emsp;The reason for annualization lies in both policy practicality and comparability. Specifically, annualized figures provide the intuitive sense of "What would the annual total be if this quarterly pace continued for a full year?" This makes it easier to understand the scale of a country's economy from an annual perspective. In fact, annualized values are commonly used in the United States, where economic reporting and policymaking often focus on annual growth trends. The use of annualized data allows analysts and decision makers to evaluate quarterly movements within a familiar yearly framework.

&emsp;However, when the goal is to compare multiple quarterly macroeconomic variables, it is necessary to convert annulized GDP values to its quarterly level. To do so, the seasonally adjusted nominal and real GDP figures are divided by 4.

&emsp;Also, we standardize the units of measurement by expressing all GDP values in billions of dollars. Specifically, nominal GDP figures that are not seasonally adjusted and reported in millions of dollars are converted to billions by dividing them by 1,000.

## Trend, Cycles, Seasonality and Transformation
&emsp;Following Persons (1919), time series data are said to consist of three main unobservable components: the trend, cyclical and seasonal components. The trend refers to long-run development, while the cyclical component captures fluctuations lasting more than one year. The seasonal component represents recurring movements within a year. When applying time series analysis, it is useful to visualize and detect those properties by examining the graphical representation of the series.

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure1.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 1. The nominal GDP level of the United States
  </div>
</div>

&emsp;**Figure 1** shows the seasonally adjusted and non-seasonally adjusted series of the Nominal GDP of the United States. Specifically, one can observe that the series of nominal GDP increases in the long run, i.e. has a positive trend. There are two notable shifts in the series, corresponding to the 2008 global financial crisis and the 2020 COVID-19 shock. In addition, the non-seasonally adjusted series, depicted by the blue line, shows an apparent “jagged” pattern within each year. These are referred to as “seasonal variations”. Typical examples include sharp increases in personal consumption expenditures (PCE) during the second or fourth quarters, which coincide with the summer vacation and end-of-year holiday seasons, as well as swings in construction investment, which tends to rise during the spring and summer months and decline in the winter.

&emsp;When the objective is to compare changes over time, it is desirable to eliminate seasonality prior to conducting the analysis. This is because such predictable seasonal patterns can distort the underlying relationship between quarters and make meaningful comparisons more difficult. Therefore, unless there is a specific reason, it is standard practice in macroeconomic analysis to use seasonally adjusted series, depicted in orange.

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure2.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 2. Quarterly changes of the nominal GDP level of the United States
  </div>
</div>

&emsp;Now we delve deeper into the details and discuss various transformation methods to remove the trend and seasonality, thereby allowing us to focus on the cyclical component, which captures the underlying economic fluctuations of interest. **Figure 2** above applies the quarter-on-quarter(QoQ) first-difference transformation $$( \Delta GDP_{t}=GDP_{t}-GDP_{t-1} )$$ to the not seasonally adjusted quarterly nominal GDP series of the United States. While this first-difference transformation effectively removes the trend component, seasonal variations remain evident in the data. Specifically, in most years, quarterly fluctuations occur around zero, with the nominal GDP consistently lower in the first quarter, sharply increasing in the second quarter, declining in the third quarter, and slightly increasing again in the fourth quarter. Furthermore, a structural change in seasonality can be observed over time, as the typical pattern where the fourth quarter exceeds the level of the second-quarter gradually disappears.

&emsp;However, transformation methods such as **Figure 2** have a limitation in that it does not account for the scale effect of the variable. Specifically, the amplitude of the series appears to increase over time, which is likely attributable to the expansion of the economy, i.e. the rising level of nominal GDP of the United States. To remove this scale effect, it is common to transform the series into quarterly growth rates. In this case, the growth rate is calculated as follows:

$$\begin{equation}
    qg_{gdp} = \frac{GDP_{t}-GDP_{t-1}}{GDP_{t-1}}\cdot 100 \notag
\end{equation}$$

The problem with this representation, however, is that it introduces asymmetry between positive and negative changes. For example, a positive change from 100 to 125 corresponds to a 25% increase, while a negative change from 125 to 100 amounts to a 20% decrease. As a result, when calculating the average growth rate for a highly volatile series, the average can be biased. In an extreme case, the average growth rate can be calculated in spite of a negative trend. To address this issue, the most commonly used method is to employ the *continuous growth rate*, which approximates the growth rate as follows:

$$\begin{equation}
    qg_{gdp}\approx (\ln{GDP_{t}}-\ln{GDP_{t-1}})\cdot 100 \notag
\end{equation}$$

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure3.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 3. Quarterly growth rate of the nominal GDP level of the United States
  </div>
</div>

&emsp;**Figure 3** above depicts the quarterly growth rate of U.S. nominal GDP, calculated as the log difference between consecutive quarters. Similar to **Figure 2**, the long-term trend is removed, while seasonal fluctuations remain. However, unlike the level-differenced series in **Figure 2**, the volatility of the series does not exhibit an increasing pattern over time. Rather, the series fluctuates around zero with a relatively stable amplitude. Interestingly, the volatility appears relatively larger prior to the 1980s, gradually decreasing thereafter, and shows a temporary spike around 2020 before stabilizing in the subsequent period.

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure4.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 4. Annual changes of the nominal GDP level of the United States
  </div>
</div>

&emsp;Until now, various transformation methods that eliminate the trend while retaining seasonality in the series have been introduced. If the objective is to remove both the trend and seasonality, it is necessary to apply year-on-year (YoY) difference transformation ($$\Delta_{4}GDP_{t} = GDP_{t} - GDP_{t-4}$$) rather than the previous quarterly-on-quarter differencing. **Figure 4** depicts the year-on-year differenced series of the U.S. quarterly nominal GDP. A key characteristic of this series is that both the trend and seasonal fluctuations are no longer visible. Furthermore, the annual changes are generally positive, turning negative only during periods of recession. Specifically, the series shows negative changes only during the 2008 financial crisis and the 2020 COVID-19 shock.

&emsp;Similar to the QoQ differencing, the YoY differenced series in **Figure 4** does not account for the scale of the variable. As a result, the amplitude of fluctuations tends to increase over time, reflecting the expansion of the nominal GDP level. To address this scale effect, it is common to transform the series into an approximate annual growth rate as follows:

$$\begin{equation}
    ag_{gdp} = \ln{GDP_{t}} - \ln{GDP_{t-4}}\cdot 100 \notag
\end{equation}$$

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure5.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 5. Annual growth rate of the nominal GDP level of the United States
  </div>
</div>

&emsp;**Figure 5** above illustrates the annual growth rate of U.S. nominal GDP. From the 1960s to 1980s, the U.S. exhibited a relatively high average nominal GDP growth rates, ranging between 2-15%, along with considerable volatility. This was largely driven by post-war industrialization, population growth, and external shocks such as the two oil crises in 1973 and 1979. Since the 1990s, however, the U.S. economy has experienced both lower growth rates and reduced volatility, commonly referred to as the Great Moderation, reflecting a combination of low inflation, slowing productivity growth, and demographic shifts. Two notable exceptions occurred in 2008 and 2020, during which volatility spiked and negative growth rates were observed. In particular, during the COVID-19 pandemic, year-on-year nominal GDP growth sharply turned negative, followed by a rapid recovery driven by expansionary fiscal spending, with growth rates reaching around 15%---levels comparable to those of the 1960s-1980s---before reverting to the recent trend levels.

## Nominal and Real GDP
&emsp;This section explains the definitions of nominal and real GDP, along with the implicit price index derived from them, known as the GDP deflator.

&emsp;**Nominal GDP** is defined as the current dollar value of all final goods and services that are produced within a country within a given period of time. Formally, if an economy produces $$n$$ final goods and services, and the quantity of good $$i$$ produced in year $$t$$ is denoted by $$y_{i,t}$$ with the corresponding market price $$p_{i,t}$$, then the nominal GDP in year $$t$$ is the sum of prices multiplied by quantities as follows:

$$\begin{equation}
    NGDP_{t} = p_{1,t}\cdot y_{1,t} + p_{2,t}\cdot y_{2,t} + \cdots + p_{n,t}\cdot y_{n,t} = \sum_{i=1}^{n}{p_{i,t}\cdot y_{i,t}} \notag
\end{equation}$$

Defined in this way, nominal GDP changes whenever prices or quantities change. In economic analysis, our focus is maximizing utility, and utility is primarily determined by the quantity of goods and services we consume. Therefore, what ultimately matters for well-being is the quantity rather than the price level. This is why it is necessary to measure real GDP, which captures the quantity of production without being influenced by price fluctuations.

&emsp;Real GDP, often referred to as **constant dollar GDP**, is defined by evaluating the total quantity of production at the prices of a specific *base year*, in order to ensure consistency across different time periods. Specifically, it multiplies the quantity of each goods and services produced each year by their corresponding prices in the chosen base year. If the base year is denoted as year $$t$$ and the economy produces $$N$$ goods and services, the real GDP for each year can be expressed as follows:

$$\begin{aligned}
    & Y_{t} = p_{1,t}\cdot y_{1,t} + p_{2,t}\cdot y_{2,t}+\cdots+p_{N,t}\cdot y_{N,t} \notag \\ 
    & Y_{t+1} = p_{1,t}\cdot y_{1,t+1} + p_{2,t}\cdot y_{2,t+1} + \cdots + p_{N,t}\cdot y_{N,t+1} \notag \\
    & \hspace{20ex}\vdots \notag \\
    & \Rightarrow Y_{t+h} = \sum_{i=1}^{N}{p_{i,t}\cdot y_{i,t+h}}\text{ for }h=0,1,2,\cdots \notag
\end{aligned}$$

&emsp;Based on nominal GDP and constant dollar GDP (real GDP), we can then define an **implicit price index** called as the **GDP deflator** as follows:

$$\begin{aligned}
    & P_{t} = \frac{NGDP_{t}}{RGDP_{t}} = \frac{p_{1,t}\cdot y_{1,t}+\cdots+p_{N,t}\cdot y_{N,t}}{p_{1,t}\cdot y_{1,t}+\cdots+p_{N,t}\cdot y_{N,t}} = 1 \notag \\
    & P_{t+1} = \frac{NGDP_{t+1}}{RGDP_{t+1}} = \frac{p_{1,t+1}\cdot y_{1,t+1}+\cdots+p_{N,t+1}\cdot y_{N,t+1}}{p_{1,t}\cdot y_{1,t+1}+\cdots+p_{N,t}\cdot y_{N,t+1}} \notag \\
    & \hspace{20ex}\vdots \notag \\
    & \Rightarrow P_{t+h} = \frac{\sum_{i=1}^{N}{p_{i,t+h}\cdot y_{i,t+h}}}{\sum_{i=1}^{N}{p_{i,t}\cdot y_{i,t+h}}}\text{ for }h=0,1,2,\cdots \notag 
\end{aligned}$$

From the definition of the GDP deflator, we can derive two important points. First, the price level is normalized to 1 in the base year. Second, we can establish the following identity that holds between nominal GDP, real GDP, and the price level:

$$\begin{equation}
    P_{t} = \frac{NGDP_{t}}{RGDP_{t}} \iff RGDP_{t} = \frac{NGDP_{t}}{P_{t}} \notag
\end{equation}$$

From this identity, we can derive an important implication: if the price level increases, nominal GDP must increase more rapidly than real GDP to maintain the equality.

<table style="width: 50%; margin: auto; border-collapse: collapse;">
  <thead>
    <tr>
      <th style="text-align: center">Variable</th>
      <th style="text-align: center;">Quarterly</th>
      <th style="text-align: center;">Annual</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">NGDP</td>
      <td style="text-align: center;">1.54</td>
      <td style="text-align: center;">6.17</td>
    </tr>
    <tr>
      <td style="text-align: center;">RGDP</td>
      <td style="text-align: center;">0.73</td>
      <td style="text-align: center;">2.92</td>
    </tr>
    <tr>
      <td style="text-align: center;">GDPDEF</td>
      <td style="text-align: center">0.81</td>
      <td style="text-align: center;">3.25</td>
    </tr>
  </tbody>
</table>
<div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 20px; margin-bottom: 20px;">
  Table 1. Quarterly and Annual Growth Rates of Nominal GDP, Real GDP and GDP Deflator
</div>

&emsp;By examining the actual US macroeconomic data, one can verify if the identity empirically holds. Specifically, the average quarter-on-quarter growth rate of the nominal GDP is 1.54%, corresponding to an annualized growth rate of 6.17%. Applying the same method to real GDP, we find that the average QoQ growth rate is significantly lower, at 0.73%, equivalent to an annualized growth rate of 2.92%. According to the identity above, the gap between nominal and real GDP growth rates (approximately 3.25 percentage points) should match the average annual growth rate of the GDP deflator. Indeed, the GDP deflator's average quarterly growth rate is 0.81%, corresponding to an annualized growth rate of 3.25%. Therefore, we can conclude that the identity holds true in actual data.

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure6.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 6. Logarithm of the Nominal and Real GDP of the United States
  </div>
</div>

&emsp;When comparing the historical data of the nominal and real GDP, a noticeable gap emerges between the two series. Below, I examine the underlying reasons for this difference. **Figure 6** depicts the nominal and real GDP, expressed in natural logarithms. The key advantage of this logarithm transformation is that the vertical distance between two points can be interpreted as the approximate growth rate over the corresponding period.

&emsp;The figure reveals three key takeaway points. First, the nominal GDP has increased relatively rapidly in the 1970s, but its growth rate slowed after the 1980s. Second, nominal GDP exhibits a steeper upward trend compared to the real GDP. According to the identity above, when the price level rise, the growth rate of nominal GDP must exceed that of real GDP. Indeed, as shown in **Figure 7** below, both the price level and inflation regarding the GDP deflator were high during the 1970s and 1980s. Therefore, the relatively rapid increase in nominal GDP and its steeper trend compared to real GDP during this period can be attributed to this mechanism.

<div style="display: flex; justify-content: center; gap: 10px;">
  <div style="text-align: center;">
    <div style="overflow: hidden; width: 360px; height: 225px; margin: 0 auto;">
      <iframe src="/projects/TS_Package/ex2-1/figure7a.html"
              style="zoom: 0.5; width: 725px; height: 475px; border: none;">
      </iframe>
    </div>
    <div style="font-size: 14px; font-weight: bold; margin-top: 0px;">Figure 7-(a) Price Level</div>
  </div>
  <div style="text-align: center;">
    <div style="overflow: hidden; width: 360px; height: 225px; margin: 0 auto;">
      <iframe src="/projects/TS_Package/ex2-1/figure7b.html"
              style="zoom: 0.5; width: 725px; height: 475px; border: none;">
      </iframe>
    </div>
    <div style="font-size: 14px; font-weight: bold; margin-top: 0px;">Figure 7-(b) Inflation</div>
  </div>
</div>
<div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 20px; margin-bottom: 20px">
  Figure 7. Price Level and Inflation Regarding the GDP Deflator of the United States
</div>

&emsp;Third, interestingly, the level of the real GDP prior to the base year of 2017 appears to be higher than that of the nominal GDP. This is somewhat counterintuitive at first glance, considering that nominal GDP reflects real GDP adjusted for the price level. This phenomenon arises from the use of the *chain-weighted method* for calculating real GDP. The chain-weighted method addresses the limitation of arbitrarily fixing a single base year, especially since relative price of goods and services change continuously over time. To circumvent this issue, chain-weighted GDP calculates real GDP by first deriving real GDP between adjacent periods and then adjusting it using the geometric average of the growth rates.

&emsp;Since past economies where characterized by relatively lower prices productivity, calculating real GDP using recent base-year prices tends to overestimate the level of real GDP for earlier periods. As a result, it is possible to observe a reversal in which real GDP exceeds nominal GDP prior to the base year---a phenomenon commonly seen in national statistics that apply recent base years. In this analysis, the real GDP series is calculated based on a chain-weighted method while using 2017 as the base year, which explains the observed gap between real and nominal GDP levels before and after that point.

## Price Indices


### Reference
- Gar$$\imath$$n, J., Lester, R., & Sims, E. (2018), "Intermediate macroeconomics," This Version, 3(0).
- Kirchgässner, G., Wolters, J., & Hassler, U. (2012), "Introduction to modern time series analysis," *Springer Science & Business Media*.
- Persons, W. M. (1919). "Indices of business conditions: an index of general business conditions," *Harvard University Press*.

[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})