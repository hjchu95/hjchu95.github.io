---
layout: single
title: "Exercise 1. Downloading data from ECOS and FRED"
author_profile: true
permalink: /projects/TS_Package_MATLAB/exercise1/
collection: projects
---
<br>
**[Link to Code]:** <a href="https://github.com/hjchu95/Time_Series_Package/blob/main/Exercises/ex0_openAPI.m" target="_blank">ex0_openAPI.m</a>

This exercise will show how to download macroeconomic data for South Korea and the United States using Open API, which will be used throughout this time series package. These data can be obtained from the Economic Statistics System (ECOS) of the Bank of Korea (BOK) and the Federal Reserve Economic Data (FRED) provided by the Federal Reserve Bank of St. Louis.

A convenient way to download multiple datasets at once is by using an Open API. The basic principle of using an Open API is that a specific URL, constructed with a combination of 'request parameters', returns data in text format based on those parameters. This text-based data can then be retrieved using web crawling techniques.

Before diving into the details, you must first obtain an API key to use the Open API. This key functions like a password that grants access to the API and can be obtained by the following websites:  
- <a href="https://ecos.bok.or.kr/api/#/ServiceIntroduction" target="_blank">ECOS Open API Website</a>
- <a href="https://fred.stlouisfed.org/docs/api/api_key.html" target="_blank">FRED OPEN API Website</a>

Since this API key is essential for running the code below, make sure to define it in advance.  

Now the type of 'request parameters' that consist the URL link will be explained in detail for each ECOS and FRED Open API.

### (1) ECOS
The baseline URL for the ECOS Open API is as follows:
<pre><code>https://ecos.bok.or.kr/api/StatisticSearch/key/format/lang/start_page/end_page/main_code/data_frequency/start_date/end_date/sub_code1/sub_code2/sub_code3/sub_code4</code></pre>

Here, `key`, refers to value entered above, and the following box explains each request parameter in detail.

> 1. `format` (file format)  
>   : file format of the result. Can choose either `xml` or `json`.  
> 2. `lang` (language)  
>   : language of the result value. Can choose either `kr` for Korean or `en` for English.  
> 3. `start_page` & `end_page` (start and end number of requests)  
>   : start and end numbers within the full set of results. The start page should always be set to 1, and the end page can be an arbitrarily large number depending on the expected data volume.  
> 4. `main_code`