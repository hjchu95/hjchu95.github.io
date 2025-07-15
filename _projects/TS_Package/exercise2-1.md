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
Before diving into the details, it is important to note that the quarterly nominal and real GDP data (`GDP` and `GDPC1`) obtained from FRED are reported at annualized rates. This means that the quarterly values are multiplied by four to express what the total would be if the level of economic activity observed in that quarter were maintained for an entire year.

The reason for annualization lies in both policy practicality and comparability. Specifically, annualized figures provide the intuitive sense of "What would the annual total be if this quarterly pace continued for a full year?" This makes it easier to understand the scale of a country's economy from an annual perspective. In fact, annualized values are commonly used in the United States, where economic reporting and policymaking often focus on annual growth trends. The use of annualized data allows analysts and decision makers to evaluate quarterly movements within a familiar yearly framework.

However, when the goal is to compare multiple quarterly macroeconomic variables, it is necessary to convert annulized GDP values to its quarterly level. To do so, the seasonally adjusted nominal and real GDP figures are divided by 4.

Also, we standardize the units of measurement by expressing all GDP values in billions of dollars. Specifically, nominal GDP figures that are not seasonally adjusted and reported in millions of dollars are converted to billions by dividing them by 1,000.

## Trend, Cycles, Seasonality and Transformation
Following Persons (1919), time series data are said to consist of three main unobservable components: the trend, cyclical and seasonal components. The trend refers to long-run development, while the cyclical component captures fluctuations lasting more than one year. The seasonal component represents recurring movements within a year. When applying time series analysis, it is useful to visualize and detect those properties by examining the graphical representation of the series.

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure1a.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 1. The nominal GDP level of the United States
  </div>
</div>

**Figure 1** shows the seasonally adjusted and non-seasonally adjusted series of the Nominal GDP of the United States. Specifically, one can observe that the series of nominal GDP increases in the long run, i.e. has a positive trend. There are two notable shifts in the series, corresponding to the 2008 global financial crisis and the 2020 COVID-19 shock. In addition, the non-seasonally adjusted series, depicted by the blue line, shows an apparent “jagged” pattern within each year. These are referred to as “seasonal variations”. Typical examples include sharp increases in personal consumption expenditures (PCE) during the second or fourth quarters, which coincide with the summer vacation and end-of-year holiday seasons, as well as swings in construction investment, which tends to rise during the spring and summer months and decline in the winter.

When the objective is to compare changes over time, it is desirable to eliminate seasonality prior to conducting the analysis. This is because such predictable seasonal patterns can distort the underlying relationship between quarters and make meaningful comparisons more difficult. Therefore, unless there is a specific reason, it is standard practice in macroeconomic analysis to use seasonally adjusted series, depicted in orange.

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure1c.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 2. Quarterly changes of the nominal GDP level of the United States
  </div>
</div>

Now we delve deeper into the details and discuss various transformation methods to remove the trend and seasonality, thereby allowing us to focus on the cyclical component, which captures the underlying economic fluctuations of interest. **Figure 2** above applies the quarter-on-quarter(QoQ) first-difference transformation $$( \Delta GDP_{t}=GDP_{t}-GDP_{t-1} )$$ to the not seasonally adjusted quarterly nominal GDP series of the United States. While this first-difference transformation effectively removes the trend component, seasonal variations remain evident in the data. Specifically, in most years, quarterly fluctuations occur around zero, with the nominal GDP consistently lower in the first quarter, sharply increasing in the second quarter, declining in the third quarter, and slightly increasing again in the fourth quarter. Furthermore, a structural change in seasonality can be observed over time, as the typical pattern where the fourth quarter exceeds the level of the second-quarter gradually disappears.

However, transformation methods such as **Figure 2** have a limitation in that it does not account for the scale effect of the variable. Specifically, the amplitude of the series appears to increase over time, which is likely attributable to the expansion of the economy, i.e. the rising level of nominal GDP of the United States. To remove this scale effect, it is common to transform the series into quarterly growth rates. In this case, the growth rate is calculated as follows:
\begin{equation}
    qg_{gdp} = \frac{GDP_{t}-GDP_{t-1}}{GDP_{t-1}}\cdot 100 \notag
\end{equation}
The problem with this representation, however, is that it introduces asymmetry between positive and negative changes. For example, a positive change from 100 to 125 corresponds to a 25% increase, while a negative change from 125 to 100 amounts to a 20% decrease. As a result, when calculating the average growth rate for a highly volatile series, the average can be biased. In an extreme case, the average growth rate can be calculated in spite of a negative trend. To address this issue, the most commonly used method is to employ the *continuous growth rate*, which approximates the growth rate as follows:
\begin{equation}
    qg_{gdp}\approx (\ln{GDP_{t}}-\ln{GDP_{t-1}})\cdot 100 \notag
\end{equation}
<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure1d.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 3. Quarterly growth rate of the nominal GDP level of the United States
  </div>
</div>

**Figure 3** above depicts the quarterly growth rate of U.S. nominal GDP, calculated as the log difference between consecutive quarters. Similar to **Figure 2**, the long-term trend is removed, while seasonal fluctuations remain. However, unlike the level-differenced series in **Figure 2**, the volatility of the series does not exhibit an increasing pattern over time. Rather, the series fluctuates around zero with a relatively stable amplitude. Interestingly, the volatility appears relatively larger prior to the 1980s, gradually decreasing thereafter, and shows a temporary spike around 2020 before stabilizing in the subsequent period.

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure1e.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 4. Annual changes of the nominal GDP level of the United States
  </div>
</div>

Until now, various transformation methods that eliminate the trend while retaining seasonality in the series have been introduced. If the objective is to remove both the trend and seasonality, it is necessary to apply year-on-year (YoY) difference transformation ($$\Delta_{4}GDP_{t} = GDP_{t} - GDP_{t-4}$$) rather than the previous quarterly-on-quarter differencing. **Figure 4** depicts the year-on-year differenced series of the U.S. quarterly nominal GDP. A key characteristic of this series is that both the trend and seasonal fluctuations are no longer visible. Furthermore, the annual changes are generally positive, turning negative only during periods of recession. Specifically, the series shows negative changes only during the 2008 financial crisis and the 2020 COVID-19 shock.

Similar to the QoQ differencing, the YoY differenced series in **Figure 4** does not account for the scale of the variable. As a result, the amplitude of fluctuations tends to increase over time, reflecting the expansion of the nominal GDP level. To address this scale effect, it is common to transform the series into an approximate annual growth rate as follows:
\begin{equation}
    ag_{gdp} = \ln{GDP_{t}} - \ln{GDP_{t-4}}\cdot 100 \notag
\end{equation}

<div style="position: relative; width: 100%; max-width: 725px; margin: auto;">
  <div style="position: relative; padding-bottom: 65%; height: 0;">
    <iframe src="/projects/TS_Package/ex2-1/figure1f.html"
            style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;">
    </iframe>
  </div>
  <div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: 0px; margin-bottom: 20px">
    Figure 5. Annual growth rate of the nominal GDP level of the United States
  </div>
</div>

**Figure 5** above illustrates the annual growth rate of U.S. nominal GDP. From the 1960s to 1980s, the U.S. exhibited a relatively high average nominal GDP growth rates, ranging between 2-15%, along with considerable volatility. This was largely driven by post-war industrialization, population growth, and external shocks such as the two oil crises in 1973 and 1979. Since the 1990s, however, the U.S. economy has experienced both lower growth rates and reduced volatility, commonly referred to as the Great Moderation, reflecting a combination of low inflation, slowing productivity growth, and demographic shifts. Two notable exceptions occurred in 2008 and 2020, during which volatility spiked and negative growth rates were observed. In particular, during the COVID-19 pandemic, year-on-year nominal GDP growth sharply turned negative, followed by a rapid recovery driven by expansionary fiscal spending, with growth rates reaching around 15%-levels comparable to those of the 1960s-1980s-before reverting to the recent trend levels.

## Nominal and Real GDP

### Reference
- Gar$$\imath$$n, J., Lester, R., & Sims, E. (2018), "Intermediate macroeconomics," This Version, 3(0).
- Kirchgässner, G., Wolters, J., & Hassler, U. (2012), "Introduction to modern time series analysis," *Springer Science & Business Media*.

[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})