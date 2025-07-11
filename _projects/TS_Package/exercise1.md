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

## Request Parameters
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
> 4. `main_code` (statistic table)  
>   : code that specifies the statistic table, the highest-level category of the variable.  
> 5. `data_frequency` (frequency)  
>   : frequency of the data to be used, must be entered in the following format: annual (`A`), semi-annual (`S`), quarterly (`Q`), monthly (`M`), or daily (`D`)  
> 6. `start_date` & `end_date` (start and end date of the data)  
>   : start and end dates for the search that must be entered in the required format depending on the frequency of the data as follows:  
>   - Annual (A): `'2025'`
>   - Quarterly (Q): `'2025Q1'`
>   - Monthly (M): `'202501'`
>   - Daily (D): `'20250101'`
> 7. `sub_code1`  
>   : code corresponding to a specific account within a higher-level category, such account items or industry classifications.
> 8. `sub_code2`  
>   : code for a subcategory within a specific account, such as measurement items or sub-industries.
> 9. `sub_code3` & `sub_code4`  
>   : a more detailed sub-classification code; enter `'?'` if not applicable.

* Note that explanations about the request parameters can also be found in the following url:
<a href="https://ecos.bok.or.kr/api/#/DevGuide/DevSpeciflcation" target="_blank">ECOS Query Parameter Setup</a>

One can search for the specific query codes for each ECOS data in the following url:  
<a href="https://ecos.bok.or.kr/api/#/DevGuide/StatisticalCodeSearch" target="_blank">Statistic Code of ECOS Open API</a>

### (2) FRED
The baseline for the FRED Open API is as follows:
<pre><code>https://api.stlouisfed.org/fred/series/observations?series_id=main_code&api_key=key&observation_start=start_date&observation_end=end_date</code></pre>

Again, the parameter named `key` refers to value entered above, and the following box explains each request parameter in detail.

> 1. `main_code` (series_id)  
>   : ID code of the selected series
> 2. `start_date` & `end_date` (start and end date of the data)  
>   : start and end dates for the search that must be entered in the following required format; `start_date='2025-01-01'`
> 3. `frequency` (frequency)  
>   : frequency of the data to be used, must be entered in the following format: annual (`a`), semi-annual (`s`), quarterly (`q`), monthly (`m`), weekly (`w`), or daily (`d`)

The specific series ID codes for FRED variables can be found by searching for the relevant variables on the following FRED website:
<a href="https://fred.stlouisfed.org/" target="_blank">FRED Website</a>

In detail, the series ID codes is identical to the abbreviation of each variable, which can be found in parentheses next to the variable name. Note that this ID code differs depending on whether the data is seasonally adjusted and on the frequency of the data.

For example, when searching the Gross Domestic Product (GDP) in the search bar, the top result is `Gross Domestic Product`. Under this entry, one can see the link labeled `6 other formats` and clicking this link reveals various versions of the GDP variable. In detail, the series ID code of the seasonally adjusted quarterly Nominal GDP is `GDP`, while the seasonally not adjusted quarterly Nominal GDP is `GDPA`.

## Constructing the Code Dictionary and Using Functions
For convenience, a dictionary will be created to manage the statistical codes. In the `ex0_openAPI.m` file, all request parameter sets for the desired variables will be stored in a objective named `code_dictionary`.

Using the obtained API key, the code dictionary, and options containing information such as start and end dates, one can download and construct a table variable by using the `ecos_api` and `fred_api` functions for the ECOS and FRED cases, respectively.

Each function is consisted of the following input variables:
> <p style="font-size:25px"><code>KOR_df = ecos_api(code_dictionary, key, options)</code></p>
><p style="font-size:15px">Downloading economic data of South Korea using ECOS Open API</p>  
> - **Inputs**:  
>   `code_dictionary`: Dictionary containing request parameters for each variable  
>   `key`: API key (registered from "https://ecos.bok.or.kr/api/#/")  
>   `options`: start date, end date, start page, end page options  
> - **Outputs**:  
>   `KOR_df`: Table of variables

><p style="font-size:25px"><code>US_df = fred_api(code_dictionary, key, options)</code></p>
><p style="font-size:15px">Downloading economic data of the United States using FRED Open API</p> 
> - **Inputs**:  
>   `code_dictionary`: Dictionary containing request parameters for each variable  
>   `key`: API key (registered from "https://fred.stlouisfed.org/docs/api/api_key.html")  
>   `options`: start date, end date options  
> - **Outputs**:  
>   `US_df`: Table of variables

## Cleaning the US Data
One important note when using the FRED Open API is that the data retrieved may have different reporting frequencies. For example, variables such as GDP and PCE are reported on a quarterly basis, whereas the Federal Funds Rate and the 10-year Treasury Yield are available monthly. When downloading these series together, the merged dataset will follow the monthly frequency. As a result, the monthly data will have values for every month, while the quarterly data will only have values for January, April, July, and October of each year.

Therefore, it is necessary to clean the data appropriately depending on its frequency. Specifically, for quarterly data, the rows corresponding to non-quarter-end months should be discarded. For monthly data, the values should be aggregated to quarterly frequency-by computing the average of the three monthly values within each quarter.

These cleaning steps are stated in the fourth section of the `ex0_openAPI.m` code.

## Saving the Data
Finally, the downloaded data will be saved in a single Excel file. The name of the Excel file is controlled by an object called `filename`, and the data for each country are stored in separate sheets within that file.

[[Back to Previous Page]]({{ "/projects/TS_Package_MATLAB" | relative_url }})