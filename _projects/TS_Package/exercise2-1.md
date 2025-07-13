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

## Seasonality
<!-- <iframe src="/projects/TS_Package/ex2-1/figure1a.html" width="725px" height="470px" style="border:none; display:block; margin:auto;"></iframe> -->
<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">

  <!-- Left plot -->
  <div style="transform: scale(0.85); transform-origin: top left; width: 820px; height: 550px; overflow: hidden;">
    <iframe src="/projects/TS_Package/ex2-1/figure1a.html"
            width="960" height="600"
            style="border: none;">
    </iframe>
  </div>

  <!-- Right plot -->
  <div style="transform: scale(0.85); transform-origin: top left; width: 820px; height: 550px; overflow: hidden;">
    <iframe src="/projects/TS_Package/ex2-1/figure1b.html"
            width="960" height="600"
            style="border: none;">
    </iframe>
  </div>

</div>
When plotting quarterly or monthly time series data, it is common to observe a recurring pattern in the series. 

[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})