---
title: "Page List"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Page_List"
---

The page list provides data on page errors, performance, requests, and more, organized by page, allowing you to perform targeted analysis based on the data for specific pages.

<span id=".5Yqf6IO95o-P6L-w"></span>
## description


* Provides comprehensive site page information and supports page pinning.

* Provides page\-level data within the site and supports custom metrics and metric sorting.

* Provide an overview of the data

* Supports navigating to page details and viewing detailed page data

   * JS overview: including Long Task, error trends, and error list

   * Performance overview: Includes trends, distribution, and bounce rate for various performance metrics


<span id=".5pWw5o2u5qaC6KeI"></span>
## Data overview


* The page overview displays the total number of pages for the current site, the page with the highest number of visits, the page with the most JS errors, and the page with the worst First Paint (FP) performance.

* Supports click on the page URL to navigate to the page details.


<span id=".6aG16Z2i5YiX6KGo"></span>
## Page list


* Display specific data at the page level. You can click pid to go to the page details for further analysis.

* Click the checkbox to pin the page to the top.

* Supports keyword search and custom columns. The custom columns currently include the following types of metrics:

   * User analyses

   * JS error

   * Static resources

   * Performance

   * Request data

* Click the download button to download the first 1,000 entries. In Excel, you can view custom columns and all content obtained from the page list request based on the filter dimensions.


<span id=".5oyH5qCH6K-05piO"></span>
## Indicator descriptions

The calculation methods for each metric in the overview data of the page list are as follows:


|**Overview of data indicators** |**Methods for calculating overview data** |
|---|---|
|PV |Directly sum the page views of all pages. |
|UV |Sum the UV counts from all pages, then deduplicate by user_id. |
|JS error count |Directly sum JS errors from all pages. |
|JS error rate |PV that has experienced errors / PV in overview data |
|Number of users affected by JS errors |The number of users affected by JS errors across all pages is summed and then deduplicated by user_id. |
|JS errors affect user retention rate | |
|Number of static resource errors |Directly sum the number of static resource errors for all pages. |
|Static resource errors affect the number of users |The total number of users affected by static resource errors across all pages, deduplicated by user_id. |
|FP |Calculate the average FP value for all pages |
|LCP |Calculate the average LCP of all pages |
|FCP |Calculate the average FCP for all pages |
|TTI |Take the average TTI of all pages |
|CLS |Calculate the average CLS of all pages |
|Load |Get the average load of all pages |
|DomReady |Calculate the average DomReady value for all pages |
|Page performance scores |Weighted average of FCP, LCP, TTI, and CLS (the weights of each metric can be modified in the settings) |
|Slow page occurrences |The slow page counts from all pages are added together directly. |
|Request error count |Directly sum the number of request errors for all pages. |
|Request error rate |Sum of request errors for all pages divided by the total number of requests |
|Number of users affected by request errors |The total number of users affected by request errors across all pages, deduplicated by user_id. |
|Request errors affect user retention rate |Number of users affected by overview data request errors / unique visitors of overview data |
|Number of successful requests |Directly sum the number of successful requests for all pages. |
|Request success rate |The direct sum of the number of successful requests for all pages divided by the total number of requests |
|Request duration (average) |Average request duration for all pages |


<span id=".6aG16Z2i6K-m5oOF"></span>
## Page details

Page details support analysis of the page from both JS and performance perspectives.

<span id=".SlPmgLvop4g="></span>
### JS overview

<span id=".SlPplJnor6_otovlir8="></span>
#### JS error trends


* On the error trend chart, you can observe the trends of error count and rate, and affected user count and rate within the selected time period. The chart supports selecting and viewing multiple data series of the same type simultaneously.

* If a new version is released during the selected time period, version release information will be displayed in the trend chart. For version configuration, refer to [SDK release configuration](https://docs.byteplus.com/en/docs/apmplus/Use_the_SDK_to_call_an_API).


<span id=".6ZSZ6K-v5YiX6KGo"></span>
#### Error list


* The error list enumerates JavaScript errors that occurred within the selected time period, including error details, start and end times, trends in the number of errors and the number of affected users, as well as the responsible person and status.

* Click the error message to access JS error details.

* Support updating the status of multiple selected issues


<span id=".5oCn6IO95oC76KeI"></span>
### Performance overview


* The performance overview provides the description of all performance metrics on this page, current metric values, metric trends, distribution, and bounce rate status.

* Supports comparing current and expected values within indicator values and trend charts. When setting expected values, you can refer to the [indicator baseline](https://docs.byteplus.com/en/docs/apmplus/project_setting#.5oCn6IO95oyH5qCH5Z-65YeG57q_), and customize the indicator baseline according to the project situation.
