---
title: "Page list"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/page_list_minipro"
---

The page list provides data by page, such as page error, performance, request, and other metrics, enabling targeted analysis based on the data of specific pages.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Overly fragmented PIDs are detrimental to exception localization and data analysis. We recommend aggregating pages such as /a/:id under a single PID rather than reporting them separately, so that you can maximize the use of the platform’s capabilities. PID aggregation can be accomplished by setting [extractPid] in the SDK. For details, refer to [the Configuration Plugin](https://docs.byteplus.com/en/docs/apmplus/Configure_plugins).

<span id=".5pWw5o2u5qaC6KeI"></span>
### Data overview

The data overview displays the total number of pages for the current site, the page with the highest number of visits, the page with the highest JavaScript error count, the page with the longest first screen load time, and the page with the longest page transition load time. The overview supports clicking the PID to jump to the specific feature page.

<span id=".6aG16Z2i5YiX6KGo"></span>
### page list

The page list displays specific data at the page level.


* Click the checkbox to pin the page to the top.

* Supports keyword search and customizable columns. The customizable columns currently include the following types of metrics:

   * User analysis

   * JavaScript error

   * Start performance

   * pageload performance

   * Runtime Performance

   * Request data

      Clicking a metric of the corresponding type will navigate to the relevant feature page. For example, clicking the JavaScript error count will carry the PID and navigate to **JavaScript overview**.

* The calculation methods for each metric in the overview data of the page list are as follows:

   
   |**Metric** |**Calculation method** |
   |---|---|
   |PV |Directly add up the page view counts of all pages. |
   |UV |Sum the UVs from all pages and then deduplicate by user_id. |
   |page time on site |Average page time on site for all pages |
   |JavaScript error |Direct sum of all JavaScript errors across pages |
   |JavaScript error rate |PVs with errors / PVs of overview data |
   |Impacted user (JavaScript error) |The impacted user count from JavaScript errors on all pages is summed and then deduplicated by user_id. |
   |JavaScript error affects affected user rate |User count impacted by JavaScript errors in overview data / unique visitors in overview data |
   |total launch count |The total number of starts across all pages |
   |cold\-start count |Sum the cold\-start counts of all pages |
   |Cold start total time |Calculate the average value of the total Cold Start time for all pages |
   |mini program load time |Get the average mini program load time for all pages |
   |download time |Get the average download time for all pages |
   |JS injection time |Average JS injection time for all pages |
   |first screen load time |Obtain the average first screen load time for all pages |
   |first screen build time |Average first screen build time for all pages |
   |first screen render time |Obtain the average first screen render time for all pages |
   |first screen total load time |Obtain the average value of the first screen total load time for all pages. |
   |open rate |Calculate the average open rate of all pages |
   |churn rate |Calculate the average churn rate of all pages |
   |Slow start count |Sum of slow starts across all pages |
   |route change time |Obtain the average route change time for all pages |
   |page build time |Calculate the average page build time for all pages. |
   |page render time |Get the average page render time for all pages |
   |total page navigation time |Obtain the average of the total page navigation time for all pages |
   |first render time |Obtain the average first render time for all pages. |
   |First paint duration |Obtain the average First Paint duration for all pages |
   |Time to first contentful paint on the page |Calculate the average First Contentful Paint duration for all pages |
   |Largest Contentful Paint duration |Obtain the average Largest Contentful Paint time across all pages |
   |slow\-pageload count |Sum the slow\-pageload count for all pages |
   |setData Call Count |Total setData call count across all pages |
   |The setData frequency |Obtain the average setData frequency for all pages |
   |setData Time |Get the average setData Time for all pages. |
   |setData Size |Calculate the average setData Size of all pages |
   |request error |Total request error count across all pages |
   |request error rate |Take the average request error rate across all pages. |
   |request error affected user |The request error affected user counts from all pages are summed and then deduplicated by user_id. |
   |request error user impact rate |Overview data request error affected user count / overview data unique visitors |
   |successful request count |Sum of successful request counts across all pages |
   |Request success rate |Get the average page request success rate for all page requests |
   |request time |Get the average request time for all page requests |
