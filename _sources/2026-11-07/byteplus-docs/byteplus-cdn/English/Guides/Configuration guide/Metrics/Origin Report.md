---
title: "Origin Report"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/xdlhZY"
---

BytePlus CDN calculates relevant metric data for origin requests. You can view these metric data on the **Origin Report** page.

When you query metric data, you need to specify a statistical time period. You can query data for up to the past 92 days, but the time span of a single query cannot exceed 31 days. You can also specify filter conditions to narrow down the requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you have just started using the <strong>Origin Report</strong> page, please be sure to read the following document first to help you understand the description in this document.</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1">Statistical Time Period</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4">Metrics Reference</a></div>


* <div data-tips="true" data-tips-type="tip">The metric data calculated at the cache node may change due to network jitter. In most cases, metric data stabilizes within 12 hours. Therefore, the metrics on this page are for reference only and might not match your bill. For actual usage charges, refer to your bill.</div>


* <div data-tips="true" data-tips-type="tip">The data displayed on the page may have a delay of about 5 minutes.</div>



<span id="introduction"></span>
## Introduction

The **Origin Report** in BytePlus CDN is a monitoring tool that provides detailed metric data about requests sent from CDN edge nodes to your origin server. You can use this report to analyze origin performance, monitor traffic and bandwidth load, and identify request patterns or potential issues. This document explains the available metrics, such as traffic, bandwidth, and status codes, and guides you on how to filter data, set time periods, and download reports for further analysis.

For origin requests that meet the filter criteria, this page displays aggregate data and data trends for the following metrics:


* Bandwidth, traffic, requests, QPS, status codes, response time


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For status codes, this page displays the number of status codes for 2xx, 3xx, 4xx, and 5xx categories, including:</div>


   * <div data-tips="true" data-tips-type="tip">Number of status codes per category.</div>


   * <div data-tips="true" data-tips-type="tip">Trend in the number of status codes per category.</div>


   * <div data-tips="true" data-tips-type="tip">Trend in the number of individual status codes under each category.</div>



**Screenshot for traffic**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_88e0661e8b1c96b3bd94b906de35e21a.png) </span>

**Screenshot for requests**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cd56261a2ab551e11e005b2312c13353.png) </span>

<span id="data-filtering"></span>
## Data Filtering

You can use the following filters for origin requests.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d967108fffa2bffefa56b2d86b9d8e3b.png) </span>


|**Filter type** |**Description** |
|---|---|
|Project |Collects metric data at the project level. If no project is specified, the metric data is collected at the domain name level.<br><br>**Example**<br><br>Consider the following scenario:<br><br><br>* The specified statistical time period is from 8:00 to 10:00 on a given day.<br><br>* Domain name X is transferred from another project to project A at 9:00. Domain name Y has always been in project A.<br><br><br>In this scenario,<br><br><br>* Suppose you specify both project A and domain names X and Y. In this case, you get the project\-level metric data, covering:<br><br>   * The metric data of domain name X from 9:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00.<br><br>* Suppose you do not specify project A but specify domain names X and Y. In this case, you get the domain name\-level metric data, covering:<br><br>   * The metric data of domain name X from 8:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00. |
|Domain Name |Indicates one or more domain names used to filter origin requests. You can specify up to 50 domain names. Multiple domain names are separated by commas (,). If no domain name is specified, this filter is not applied.<br><br>Please note:<br><br><br>* If a project is specified, you get the project\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of the project during the statistical time period, the metric data will be affected.<br><br>* If no project is specified, you get the domain name\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of any project during the statistical time period, the metric data will not be affected.<br><br><br>See the example in the "Project" description.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For IAM users, the domain name list includes the domain names they have permission to access.</div><br> |


<span id="time-granularity-and-statistical-time-period"></span>
## Time Granularity and Statistical Time Period

On the page, you also need to specify the time granularity and statistical period.


* Time granularity determines the interval between data points in the breakdown data. This setting affects how both summary and breakdown data are calculated and displayed. For more information, see [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1).

* The options for statistical time period are **Today**, **Yesterday**, **Past 3 Days**, **Past 7 Days**, **Past 30 Days**, **This Month**, and **Last Month**. You can also specify an arbitrary time period within the past 92 days, down to the minute. The default is **Today**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At the top of the page, you can specify the time zone of the statistical time period. The default time zone is UTC+08:00.</div>


The time granularities you can specify vary depending on the time span of the selected statistical period. The details are as follows:


* If time span <= 1 day, you can specify a time granularity of **1 Minute**, **5 Minutes**, or **1 Hour**.

* If 1 day < time span <= 3 days, you can specify a time granularity of **5 Minutes**, **1 Hour**, or **1 Day**.

* If 3 days < time span <= 31 days, you can specify a time granularity of **1 Hour** or **1 Day**.


The calculation method for the summary data of metrics can vary with different time granularities. For more information, see [Metrics Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

To the right of the statistical time period, there is a **Compare** button. When you click **Compare**, you can specify another statistical period for comparison. CDN will calculate and display the breakdown and aggregate data for each metric for both time periods.

<span id="metric-data"></span>
## Metric Data

After you set the filter conditions, time granularity and statistical time period, you can click **Query** to view the data of each metric.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ad0c593d5243883630e5fac06addbd52.png) </span>

Metric data includes aggregate data and breakdown data within the statistical time period. Breakdown data is presented in a line chart with time on the horizontal axis, allowing you to understand trend in the data.

The page displays data for the following metrics:


|**Metric** |**Breakdown Data** |**Aggregate Data** |
|---|---|---|
|Traffic |Displays the data volume trend within the actual statistical time period, including:<br><br><br>* Trend in the amount of data the CDN transfers to origins.<br><br>* Trend in the amount of data transferred by origins to the CDN. |Displays the total data volume within the actual statistical time period, including:<br><br><br>* The amount of data the CDN transfers to origins.<br><br>* The amount of data transferred by origins to the CDN. |
|Bandwidth |Displays the bandwidth trend within the actual statistical time period, including:<br><br><br>* Bandwidth trend based on the amount of data the CDN transfers to origins.<br><br>* Bandwidth trend based on the amount of data transferred by origins to the CDN. |Displays the peak bandwidth within the actual statistical time period, including:<br><br><br>* Peak bandwidth calculated based on the amount of data the CDN transfers to origins.<br><br>* Peak bandwidth calculated based on the amount of data transferred by origins to the CDN. |
|Requests |Displays the trend of the number of origin requests during the actual statistical period. |Displays the total number of origin requests within the actual statistical period. |
|QPS |Displays the QPS trend over the actual statistical time period. |Displays the peak request QPS during the actual statistical period. |
|Status Codes |Displays the trend in the number of response status codes from origins during the actual statistical time period, including:<br><br><br>* Trends for the 2xx status code category and for each individual status code within that category (e.g., 200, 201).<br><br>* Trends for the 3xx status code category and for each individual status code within that category.<br><br>* Trends for the 4xx status code category and for each individual status code within that category.<br><br>* Trends for the 5xx status code category and for each individual status code within that category. |Displays the number of response status codes from origins during the actual statistical time period, including:<br><br><br>* Number of 2xx status codes.<br><br>* Number of 3xx status codes.<br><br>* Number of 4xx status codes.<br><br>* Number of 5xx status codes. |
|Response Time |Displays the trend of the average time it takes for CDN to receive origin responses during the actual statistical time period. |Displays the average time it takes for CDN to receive origin responses during the actual statistical time period. |


For the definition and calculation method of each metric, see [Metrics Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

<span id="timeline"></span>
## Timeline

The time axis at the bottom of the data trend chart represents the selected statistical period. You can drag the start and end time points to see a breakdown of the metric over a smaller time range.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_144d51d408b3465c132a6e814e663661.png) </span>

<span id="data-unit"></span>
## Data Unit

CDN uses default units and bases to display metric data. You can specify different units for each metric. For some metrics, you can also change the base for calculation. If you specify a different unit or base, the metric data will be updated accordingly.

The available units for each metric are as follows:


|**Metric** |**Base** |**Available Units** |**Default Unit** |
|---|---|---|---|
|Traffic |1,000 |KB, MB, GB, TB, and PB |GB |
|Bandwidth ||Kbps, Mbps, Gbps, and Tbps |Mbps |
|Requests |Not applicable |Thousands, Millions, Billions |Millions |
|QPS ||Thousands QPS, Millions QPS, Billions QPS |Thousands QPS |
|Status Codes ||Thousands, Millions, Billions |Millions |
|Response Time ||Milliseconds, Seconds, Minutes |Milliseconds |


<span id="data-download"></span>
## Data Download

You can download the breakdown data shown in the trend chart by using the download button to the right of the time granularity selector. When you click the download button, you need to select the file format to download. The available file formats are  **.xlsx** and  **.csv**.

For each metric, the naming convention of the downloaded file is as follows. In the file naming convention, `<YYYYMMDDHHMMSS>` represents the download time of the file, and `<AccountID>` represents the ID of the primary account.


|**Metric** |**Naming Convention for Downloaded Files** |
|---|---|
|Traffic |`ByteplusCDN traffic <AccountID>_<YYYYMMDDHHMMSS>` |
|Bandwidth |`ByteplusCDN bandwidth <AccountID>_<YYYYMMDDHHMMSS>` |
|Requests |`ByteplusCDN requests <AccountID>_<YYYYMMDDHHMMSS>` |
|QPS |`ByteplusCDN qps <AccountID>_<YYYYMMDDHHMMSS>` |
|Status Codes |`ByteplusCDN status_all <AccountID>_<YYYYMMDDHHMMSS>` |
|Response Time |`ByteplusCDN response_time <AccountID>_<YYYYMMDDHHMMSS>` |
