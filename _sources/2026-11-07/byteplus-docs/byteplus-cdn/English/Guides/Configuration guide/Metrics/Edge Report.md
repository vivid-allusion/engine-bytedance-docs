---
title: "Edge Report"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/bWlzDn"
---

BytePlus CDN collects statistics on relevant metrics for user requests. You can view these metric data on the **Edge Report** page.

When you query metric data, you need to specify a statistical time period. You can query data for up to the past 92 days, but the time span of a single query cannot exceed 31 days. At the same time, you can specify filtering conditions to filter requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you have just started using the <strong>Edge Report</strong> page, please be sure to read the following document first to help you understand the description in this document.</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1">Statistical Time Period</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4">Metrics Reference</a></div>


* <div data-tips="true" data-tips-type="tip">The metric data calculated at the cache node may change due to network jitter. In most cases, metric data stabilizes within 12 hours. Therefore, the metrics on this page are for reference only and might not match your final bill. For official usage data, refer to your invoice.</div>


* <div data-tips="true" data-tips-type="tip">The data displayed on the page may have a delay of about 5 minutes.</div>



<span id="introduction"></span>
## Introduction

The **Edge Report** page provides comprehensive statistics on user request metrics collected by BytePlus CDN. On this page, you can query, filter, and visualize key data to monitor service performance and analyze usage patterns. This document explains how to use various filters, set time periods, and interpret metrics like bandwidth, traffic, and status codes.

For user requests that meet the filter criteria, this page displays aggregate data and data trends for the following metrics:


* Bandwidth, traffic, requests, QPS, status codes, response time, average speed


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Average speed refers to the average data transfer rate of the CDN in response to user requests.</div>


* <div data-tips="true" data-tips-type="tip">For status codes, this page displays the number of status codes for 2xx, 3xx, 4xx, and 5xx categories, including:</div>


   * <div data-tips="true" data-tips-type="tip">Number of status codes per category.</div>


   * <div data-tips="true" data-tips-type="tip">Trend in the number of status codes per category.</div>


   * <div data-tips="true" data-tips-type="tip">Trend in the number of individual status codes under each category.</div>



**Screenshot of traffic**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_442bfaae6ab9fc2278e4540da0ecfa6d.png) </span>

**Screenshot of status codes**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e1338f0369bac584b48fac9e140aae7d.png) </span>

<span id="data-filtering"></span>
## Data Filtering

You can specify the following filtering types to filter user requests.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b8a0ebc60abfad52f94395634dae1beb.png) </span>


|**Filter type** |**Description** |
|---|---|
|Project |Collects metric data at the project level. If no project is specified, the metric data is collected at the domain name level.<br><br>**Example**<br><br>Consider the following scenario:<br><br><br>* The specified statistical time period is from 8:00 to 10:00 on a specific day.<br><br>* Domain name X is transferred from another project to project A at 9:00. Domain name Y has always been in project A.<br><br><br>In this scenario,<br><br><br>* Suppose you specify both project A and domain names X and Y. In this case, you get the project\-level metric data, covering:<br><br>   * The metric data of domain name X from 9:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00.<br><br>* Suppose you do not specify project A but specify domain names X and Y. In this case, you get the domain name\-level metric data, covering:<br><br>   * The metric data of domain name X from 8:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00. |
|Domain Name |Indicates one or more domain names used to filter user requests. You can specify up to 50 domain names. Multiple domain names are separated by commas (,). If no domain name is specified, it indicates that this filter type is not used to filter requests.<br><br>Please note:<br><br><br>* If a project is specified, you get the project\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of the project during the statistical time period, the metric data will be affected.<br><br>* If no project is specified, you get the domain name\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of any project during the statistical time period, the metric data will not be affected.<br><br><br>See the example in the "Project" description.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For IAM users, the domain name list includes the domain names they have permission to access.</div><br> |
|Request Protocol |Specify an application layer protocol to filter user requests to obtain requests using this protocol. This configuration has the following options:<br><br><br>* HTTP: Indicates the HTTP protocol.<br><br>* HTTPS: Indicates the HTTPS protocol.<br><br>* QUIC: Indicates the QUIC protocol. For a description of the QUIC protocol, see [QUIC Protocol](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-quic_1).<br><br>* WebSocket: Indicates the WebSocket protocol.<br><br>* Non\-WebSocket: Indicates the HTTP, HTTPS and QUIC protocols.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you are viewing data for response time or average speed, please specify <strong>Request Protocol</strong> to filter out WebSocket requests. This is because the data for these two metrics is inaccurate for WebSocket requests.</div><br> |
|Client Regions |Specify up to 10 Chinese provincial administrative regions or up to 30 countries and regions to filter user requests for requests originating from those regions. All countries and regions are included by default. |
|Chinese ISPs |Specify up to 5 Chinese network operators to filter user requests for requests using these operators.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This filter type is only available when <strong>Client Regions</strong> is <strong>China/xx</strong>.</div><br> |
|IP Version |Specify an IP protocol version to filter user requests to obtain requests that use this protocol version. You can specify **IPv4** or **IPv6**. Versions of all IP protocols are included by default. |


<span id="time-granularity-and-statistical-time-period"></span>
## Time Granularity and Statistical Time Period

On the page, you also need to specify the time granularity and statistical period.


* Time granularity determines the data point interval in the trend chart and affects how summary and breakdown data are calculated and displayed. For more information, see [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1).

* The options for statistical time period are **Today**, **Yesterday**, **Past 3 Days**, **Past 7 Days**, **Past 30 Days**, **This Month**, and **Last Month**. You can also specify an arbitrary time period within the past 92 days, down to the minute. The default is **Today**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At the top of the page, you can specify the time zone of the statistical time period. The default time zone is UTC+08:00.</div>


The available time granularities depend on the selected time span:


* If time span <= 1 day, you can specify a time granularity of **1 Minute**, **5 Minutes**, or **1 Hour**.

* If 1 day < time span <= 3 days, you can specify a time granularity of **5 Minutes**, **1 Hour**, or **1 Day**.

* If 3 days < time span <= 31 days, you can specify a time granularity of **1 Hour** or **1 Day**.


The calculation method for the summary data of metrics can vary with different time granularities. For more information, see [Metrics Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

To the right of the statistical time period, there is a **Compare** button. When you click **Compare**, you can specify another statistical period for comparison. CDN will calculate and display the breakdown data and aggregate data of each metric for these two statistical time periods respectively.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d9785c263888c9efe4379af71d008868.png) </span>

<span id="metric-data"></span>
## Metric Data

After setting the filters, time granularity, and statistical period, click **Query** to view the metric data.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ec50fc34730a3fc1a8cf29e78a04a7cb.png) </span>

Metric data includes aggregate data and breakdown data within the statistical time period. Breakdown data is presented in a line chart with time on the horizontal axis, allowing you to understand the trend in the data.

The page displays data for the following metrics:


|**Metric** |**Breakdown Data** |**Aggregate Data** |
|---|---|---|
|Traffic |Displays the data volume trend within the actual statistical time period, including:<br><br><br>* Trend in the amount of data users transfer to the CDN.<br><br>* Trend in the amount of data transferred by CDNs to users. |Displays the total data volume within the actual statistical time period, including:<br><br><br>* The amount of data the user transfers to the CDN.<br><br>* The amount of data the CDN transfers to users. |
|Bandwidth |Displays the bandwidth trend within the actual statistical time period, including:<br><br><br>* Bandwidth trend based on the amount of data users transfer to the CDN.<br><br>* Bandwidth trend based on the amount of data the CDN transfers to users. |Displays the peak bandwidth within the actual statistical time period, including:<br><br><br>* Peak bandwidth calculated based on the amount of data users transferred to the CDN.<br><br>* Peak bandwidth calculated based on the amount of data the CDN transfers to users. |
|Requests |Displays the trend of the number of requests during the actual statistical period, including:<br><br><br>* Trend in the number of all user requests.<br><br>* Trend in the number of dynamic user requests.<br><br>* Trend in the number of static user requests. |Displays the total number of requests within the actual statistical period.<br><br><br>* Number of all user requests.<br><br>* Number of dynamic user requests.<br><br>* Number of static user requests. |
|QPS |Displays the trend of request QPS during the actual statistical time period. |Displays the peak request QPS during the actual statistical period. |
|Status Codes |Displays the trend in the number of CDN response status codes during the actual statistical time period, including:<br><br><br>* Trends in the number of 2xx status codes and each status code starting with the number 2.<br><br>* Trends in the number of 3xx status codes and each status code starting with the number 3.<br><br>* Trends in the number of 4xx status codes and each status code starting with the number 4.<br><br>* Trends in the number of 5xx status codes and each status code starting with the number 5. |Displays the number of CDN response status codes during the actual statistical time period, including:<br><br><br>* Number of 2xx status codes.<br><br>* Number of 3xx status codes.<br><br>* Number of 4xx status codes.<br><br>* Number of 5xx status codes. |
|Response Time |Displays the trend of the average time it takes for CDN to respond to user requests during the actual statistical time period. |Displays the average time it takes for CDN to respond to user requests during the actual statistical time period. |
|Average Speed |Displays the average speed trend when CDN transfers data to users during the actual statistical time period. |Displays the average speed when the CDN transfers data to users during the actual statistical time period. |


For the definition and calculation method of each metric, see [Metrics Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

<span id="timeline"></span>
## Timeline

A timeline at the bottom of the data trend chart shows the selected statistical period. You can drag the start and end time points to see a breakdown of the metric over a smaller time range.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4a23869f3068db793b898912af7e03d7.png) </span>

<span id="data-unit"></span>
## Data Unit

CDN uses default units and bases to display metric data. You can specify other units and bases on the page. If you specify a different unit or base, the metric data will be updated accordingly.

The available units for each metric are as follows:


|**Metric** |**Base** |**Available Units** |**Default Unit** |
|---|---|---|---|
|Traffic |1,000 |KB, MB, GB, TB, and PB |GB |
|Bandwidth ||Kbps, Mbps, Gbps, and Tbps |Mbps |
|Requests |Not applicable |Thousands, Millions, Billions |Millions |
|QPS ||Thousands QPS, Millions QPS, Billions QPS |Thousands QPS |
|Status Codes ||Thousands, Millions, Billions |Millions |
|Response Time ||Milliseconds, Seconds, Minutes |Milliseconds |
|Average Speed |1,000 |bps, Kbps, Mbps, Gbps, and Tbps |Kbps |


<span id="data-download"></span>
## Data Download

To the right of the time granularity selector, you can download a breakdown of the metric in the trend chart. When you click the download button, you need to select the file format to download. The file formats available are **xlsx** and **csv**.

For each metric, the naming convention of the downloaded file is as follows. In the file naming convention, `<YYYYMMDDHHMMSS>` represents the download time of the file, and `<AccountID>` represents the ID of the primary account.


|**Metric** |**Naming Convention for Downloaded Files** |
|---|---|
|Traffic |`ByteplusCDN traffic <AccountID>_<YYYYMMDDHHMMSS>` |
|Bandwidth |`ByteplusCDN bandwidth <AccountID>_<YYYYMMDDHHMMSS>` |
|Requests |`ByteplusCDN requests <AccountID>_<YYYYMMDDHHMMSS>` |
|QPS |`ByteplusCDN qps <AccountID>_<YYYYMMDDHHMMSS>` |
|Status Codes |`ByteplusCDN status_all <AccountID>_<YYYYMMDDHHMMSS>` |
|Response Time |`ByteplusCDN response_time <AccountID>_<YYYYMMDDHHMMSS>` |
|Average Speed |`ByteplusCDN avg_speed <AccountID>_<YYYYMMDDHHMMSS>` |
