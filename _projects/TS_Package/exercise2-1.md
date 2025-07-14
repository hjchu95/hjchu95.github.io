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

## Trend, Seasonality and Transformation
When applying time series analysis, it is useful to plot and detect those properties of the series by observing the graphical representation.

<iframe src="/projects/TS_Package/ex2-1/figure1a.html" width="725px" height="475px" style="border:none; display:block; margin:auto;"></iframe>
<div style="text-align: center; font-weight: bold; font-size: 16px; margin-top: -30px; margin-bottom: 20px">
  Figure 1. The nominal GDP level of the United States
</div>

Figure 1 shows the seasonally adjusted and non-seasonally adjusted series of the Nominal GDP of the United States. Specifically, one can observe that the series of nominal GDP increases in the long run, i.e. has a positive trend. There are two notable shifts in the series, corresponding to the 2008 global financial crisis and the 2020 COVID-19 shock. In addition, the non-seasonally adjusted series, depicted by the blue line, shows an apparent “jagged” pattern within each year. These are referred to as “seasonal variations”. Typical examples include sharp increases in personal consumption expenditures (PCE) during the second or fourth quarters, which coincide with the summer vacation and end-of-year holiday seasons, as well as swings in construction investment, which tends to rise during the spring and summer months and decline in the winter.

When the objective is to compare changes over time, it is desirable to eliminate seasonality prior to conducting the analysis. This is because such predictable seasonal patterns can distort the underlying relationship between quarters and make meaningful comparisons more difficult. Therefore, unless there is a specific reason, it is standard practice in macroeconomic analysis to use seasonally adjusted series, depicted in orange.


[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})