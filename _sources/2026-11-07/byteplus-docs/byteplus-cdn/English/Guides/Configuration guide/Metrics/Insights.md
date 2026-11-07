---
title: "Insights"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/6a4Gqa"
---

The Insights feature in BytePlus CDN provides valuable analytics by calculating and analyzing user request metrics. With this feature, you can gain a deep understanding of your CDN usage and user behavior. This document introduces the three main components of the Insights page—Data Distribution, Client IPs, and Domain Rankings—and guides you on how to interpret various metrics to optimize your content delivery strategy.

BytePlus CDN gathers statistics and analyzes relevant metrics of user requests, displaying information valuable to your business. The [Insights](https://console.byteplus.com/cdn/cdn-bp/report/insights) page includes the following tabs:


* [Data Distribution](https://docs.byteplus.com/en/docs/18/22304#data-distribution)

* [Client IPs](https://docs.byteplus.com/en/docs/18/22304#client-ips)

* [Domain Rankings](https://docs.byteplus.com/en/docs/18/22304#domain-rankings)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you have just started using the <strong>Insights</strong> page, please be sure to read the following document first to help you understand the description in this document.</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1">Statistical Time Period</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4">Metrics Reference</a>. In this document, focus on the calculation methods for aggregate data of traffic, requests, and status codes.</div>


* <div data-tips="true" data-tips-type="tip">The metric data calculated at the cache node may change due to network jitter. In most cases, metric data stabilizes within 12 hours.</div>



<span id="data-unit"></span>
## Data Unit

CDN uses default units and bases to display metric data. You can specify other units and bases on the page. If you specify a different unit or base, the metric data will be updated accordingly.

The available units for each metric are as follows:


|**Metric** |**Base** |**Available Units** |**Default Unit** |
|---|---|---|---|
|Traffic |1,000 |KB, MB, GB, TB, and PB |GB |
|Bandwidth ||Kbps, Mbps, Gbps, and Tbps |Kbps |
|Requests |Not applicable |Thousands, Millions, Billions |Thousands |
|2xx Status Codes ||||
|3xx Status Codes ||||
|4xx Status Codes ||||
|5xx Status Codes ||||
|4xx Status Codes || ||
|5xx Status Codes || ||


<span id="data-distribution"></span>
## Data Distribution

<span id="introduction"></span>
### Introduction

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The data displayed on the page may have a delay of about 5 minutes.</div>


This tab shows the distribution of aggregate data for the following metrics across countries and regions:


* Data transfer from clients to CDN (traffic): The amount of data transferred from users to the CDN.

* Data transfer from CDN to clients (traffic): The amount of data transferred by CDN to users.

* Data transfer from clients to CDN (bandwidth): The peak bandwidth calculated based on the amount of data transferred by users to the CDN.

* Data transfer from CDN to clients (bandwidth): The peak bandwidth calculated based on the amount of data transferred by the CDN to users.

* Number of non\-GET and non\-HEAD requests: The number of dynamic requests received by CDN.

* Number of GET and HEAD requests: Indicates the number of static requests received by CDN.

* Total requests: Indicates the number of all user requests received by the CDN.


Metric data is aggregated by country and region and sorted from largest to smallest. For the definition and calculation method of each metric, see [Metrics Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

<span id="data-filtering"></span>
### Data Filtering

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f3d4b5a80cd0c05a093ead94012551b3.png) </span>


|**Filter type** |**Description** |
|---|---|
|Project |Collects metric data at the project level. If no project is specified, the metric data is collected at the domain name level.<br><br>&nbsp;<br><br>**Example**<br><br>Consider the following scenario:<br><br><br>* The specified statistical time period is from 8:00 to 10:00 on a certain day.<br><br>* Domain name X is transferred from another project to project A at 9:00. Domain name Y has always been in project A.<br><br><br>In this scenario,<br><br><br>* Suppose you specify both project A and domain names X and Y. In this case, you get the project\-level metric data, covering:<br><br>   * The metric data of domain name X from 9:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00.<br><br>* Suppose you do not specify project A but specify domain names X and Y. In this case, you get the domain name\-level metric data, covering:<br><br>   * The metric data of domain name X from 8:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00. |
|Domain Name |Indicates one or more domain names used to filter user requests. You can specify up to 50 domain names. Multiple domain names are separated by commas (,). If no domain name is specified, it indicates that this filter type is not used to filter requests.<br><br>&nbsp;<br><br>Please note:<br><br><br>* If a project is specified, you get the project\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of the project during the statistical time period, the metric data will be affected.<br><br>* If no project is specified, you get the domain name\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of any project during the statistical time period, the metric data will not be affected.<br><br><br>See the example in the "Project" description.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For IAM users, the domain name list includes the domain names they have permission to access.</div><br> |


<span id="time-granularity-and-statistical-time-period"></span>
### Time Granularity and Statistical Time Period

On the page, you also need to specify the time granularity and statistical period.


* Aggregate data is the sum of a series of data points. Time granularity determines the time interval between each data point.

* The options for statistical time period are **Today**, **Yesterday**, **Past 3 Days**, **Past 7 Days**, **Past 30 Days**, **This Month**, and **Last Month**. You can also specify an arbitrary time period within the past 92 days, down to the minute. The default is **Today**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At the top of the page, you can specify the time zone of the statistical time period. The default time zone is UTC+08:00.</div>


The time granularity you specify affects the time span of the statistical period.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The time granularity used by CDN to aggregate data is specified by CDN and cannot be adjusted by you.</div>


Details are shown in the table below:


|**Time granularity** |**Maximum time span of the statistical period** |
|---|---|
|1 minute |1 day |
|5 minutes |31 days |


In addition, time granularity also determines the actual statistical time period of metric data. See [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1).

<span id="metric-data"></span>
### Metric Data

After you set the filter conditions, time granularity and statistical time period, you can click **Query** to view the data of each metric.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5d13e9da6ea75b068eadb00566844b6c.png) </span>

<span id="data-unit"></span>
#### Data Unit

See [Data Unit](https://docs.byteplus.com/en/docs/18/22304#data-unit).

<span id="data-download"></span>
#### Data Download

You can click the download button on the upper right side of the data table to download the metric data in the table. When you click the download button, you need to select the file format to download. The file formats available are **xlsx** and **csv**.

For each metric, the naming convention of the downloaded file is as follows. In the file naming convention,  *<YYYYMMDDHHMMSS\>*  represents the download time of the file, and  *<AccountID\>*  represents the ID of the primary account.


|**Metric** |**Naming Convention for Downloaded Files** |
|---|---|
|Clients data transfer to CDN (traffic) |ByteplusCDN Data distribution_in_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|CDN data transfer to clients (traffic) |ByteplusCDN Data distribution_out_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|Clients data transfer to CDN (bandwidth) |ByteplusCDN Data distribution_in_bandwidth  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|CDN data transfer to clients (Bandwidth) |ByteplusCDN Data distribution_out_bandwidth  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|Number of non\-GET and non\-HEAD requests |ByteplusCDN Data distribution_dynamic_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|Number of GET and HEAD requests |ByteplusCDN Data distribution_static_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|Total requests |ByteplusCDN Data distribution_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |


<span id="client-ips"></span>
## Client IPs

<span id="introduction"></span>
### Introduction

This tab shows the trend in the number of unique client IP addresses during the statistical time period.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The number of unique client IP addresses is based on hourly granularity metric data. Therefore, the data statistics may have a delay of about 2 hours. For example, for the number of unique client IP addresses during the time period from 09:00 to 10:00, you can get the accurate results around 11:00.</div>


<span id="data-filtering"></span>
### Data Filtering

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d441ca34fb8a8cb04b09b66aed6086cb.png) </span>


|**Filter type** |**Description** |
|---|---|
|Project |Indicates a project used to collect metric data at the project level. If no project is specified, it indicates that the metric data is collected at the domain name level.<br><br>&nbsp;<br><br>**Example**<br><br>Consider the following scenario:<br><br><br>* The specified statistical time period is from 8:00 to 10:00 on a certain day.<br><br>* Domain name X is transferred from another project to project A at 9:00.<br><br><br>In this scenario,<br><br><br>* Suppose you specify both project A and domain names X. In this case, you get the project\-level metric data, covering the metric data of domain name X from 9:00 to 10:00.<br><br>* Suppose you do not specify project A but specify domain names X. In this case, you get the domain name\-level metric data, covering the metric data of domain name X from 8:00 to 10:00. |
|Domain Name |Indicates one domain name used to filter user requests. If no domain name is specified, it indicates that this filter type is not used to filter requests.<br><br>&nbsp;<br><br>Please note:<br><br><br>* If a project is specified, you get the project\-level metric data for the specified domain name. This means that if the domain name was transferred into or out of the project during the statistical time period, the metric data will be affected.<br><br>* If no project is specified, you get the domain name\-level metric data for the specified domain name. This means that if the domain name was transferred into or out of any project during the statistical time period, the metric data will not be affected.<br><br><br>See the example in the "Project" description.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For IAM users, the domain name list includes the domain names they have permission to access.</div><br> |
|Client Regions |Specify up to 10 Chinese provincial administrative regions or up to 30 countries and regions to filter requests by their origin. All countries and regions are included by default. |
|IP Version |Specify an IP protocol version to filter user requests. You can specify **IPv4** or **IPv6**. Versions of all IP protocols are included by default. |


<span id="time-granularity-and-statistical-time-period"></span>
### Time Granularity and Statistical Time Period

On the page, you also need to specify the time granularity and statistical period.


* The time granularity you can specify is **Hour** and **Day**.

* You can specify a statistical period that spans no more than 31 days.

* Aggregate data is the rollup of a series of breakdown data. Time granularity determines the time interval between each breakdown data. In addition, time granularity also determines the actual statistical time period. See [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1).

* The options for statistical time period are **Today**, **Yesterday**, **Past 3 Days**, **Past 7 Days**, **Past 30 Days**, **This Month**, and **Last Month**. You can also specify an arbitrary time period within the past 92 days, down to the minute. The default is **Today**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At the top of the page, you can specify the time zone of the statistical time period. The default time zone is UTC+08:00.</div>


<span id="metric-data"></span>
### Metric Data

After you set the filter conditions, time granularity and statistical time period, you can click **Query** to view the trend of the number of unique client IP addresses.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_077b14b7d89438810ea94e2543866b4f.png) </span>

<span id="timeline"></span>
#### Timeline

There is a time axis at the bottom of the data trend chart, which reflects the actual statistical time period. You can drag the start and end time points to see a breakdown of the metric over a smaller time range.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_540b4c7f65cdfe5c855499907caf65c0.png) </span>

<span id="data-unit"></span>
#### Data Unit

CDN uses default units and bases to display metric data. You can specify other units and bases on the page. If you specify a different unit or base, the metric data will be updated accordingly.

The available units for the number of unique client IP addresses are as follows:


|**Metric** |**Available Bases** |**Default Base** |
|---|---|---|
|Unique Client IP Addresses |Thousands, Millions, Billions |Thousands |


<span id="data-download"></span>
### Data Download

Click the download button in the upper\-right corner of the data table to download the metric data as an .xlsx or .csv file.

The naming convention for downloaded files is as follows:


* ByteplusCDN client\-ip\-analysis  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>* 


 *<YYYYMMDDHHMMSS\>*  represents the download time of the file, and  *<AccountID\>*  represents the ID of the primary account.

<span id="domain-rankings"></span>
## Domain Rankings

<span id="introduction"></span>
### Introduction

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The data displayed on the page may have a delay of about 5 minutes.</div>


Based on the user requests received by the CDN and the requests sent to the origins, this tab calculates and displays aggregate data of the following metrics by domain name:


|**Type** |**Metric** |
|---|---|
|User Requests Received by CDN |* Client data transfer to CDN (traffic): Indicates the amount of data transferred by users to the CDN.<br><br>* CDN data transfer to client (traffic): Indicates the amount of data transferred by CDN to users.<br><br>* Client data transfer to CDN (bandwidth): Indicates the peak bandwidth calculated based on the amount of data transferred by users to the CDN.<br><br>* CDN data transfer to client (bandwidth): Indicates the peak bandwidth calculated based on the amount of data transferred by the CDN to users.<br><br>* Non\-GET and non\-HEAD requests: Indicates the number of dynamic requests received by CDN.<br><br>* GET and HEAD requests: Indicates the number of static requests received by CDN.<br><br>* Total requests: Indicates the number of all user requests received by the CDN.<br><br>* 2xx: Indicates the number of 2xx status codes in the CDN's response to user requests.<br><br>* 3xx: Indicates the number of 3xx status codes.<br><br>* 4xx: Indicates the number of 4xx status codes.<br><br>* 5xx: Indicates the number of 5xx status codes. |
|Requests Sent by CDN to Origins |* Origin data transfer to CDN (traffic): Indicates the amount of data transferred from origins to the CDN.<br><br>* CDN data transfer to origins (traffic): Indicates the amount of data transferred by the CDN to origins.<br><br>* Origin data transfer to CDN (bandwidth): Indicates the peak bandwidth calculated based on the amount of data transferred from origins to the CDN.<br><br>* CDN data transfer to origins (bandwidth): Indicates the peak bandwidth calculated based on the amount of data transferred by the CDN to origins.<br><br>* Total requests: Indicates the number of requests sent by the CDN to origins.<br><br>* 2xx: Indicates the number of 2xx status codes in the origin response received by the CDN.<br><br>* 3xx: Indicates the number of 3xx status codes.<br><br>* 4xx: Indicates the number of 4xx status codes.<br><br>* 5xx: Indicates the number of 5xx status codes. |


Metric data is aggregated by domain name and sorted in descending order. For the definition and calculation method of each metric, see [Metrics Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

<span id="data-filtering"></span>
### Data Filtering

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fbf4e67d1113294b305ad589885a5322.png) </span>

Refer to the description of the filter types in [Data Distribution](https://docs.byteplus.com/en/docs/18/22304#data-distribution).

<span id="time-granularity-and-statistical-time-period"></span>
### Time Granularity and Statistical Time Period

On the page, you also need to specify the time granularity and statistical period.


* Aggregate data is the rollup of a series of breakdown data. Time granularity determines the time interval between each breakdown data.

* The options for statistical time period are **Today**, **Yesterday**, **Past 3 Days**, **Past 7 Days**, **Past 30 Days**, **This Month**, and **Last Month**. You can also specify an arbitrary time period within the past 92 days, down to the minute. The default is **Today**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At the top of the page, you can specify the time zone of the statistical time period. The default time zone is UTC+08:00.</div>


The time granularity you specify affects the following factor:


* The time span of the statistical period.


Details are shown in the table below:


|**Time granularity** |**Maximum time span of the statistical period** |
|---|---|
|1 minute |1 day |
|5 minutes |31 days |


In addition, time granularity also determines the actual statistical time period. See [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1).

<span id="metric-data"></span>
### Metric Data

After you set the filter conditions, time granularity and statistical time period, you can click **Query** to view the ranking of domain names.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_60090958ffa049b2af75c3a85a9cefd8.png) </span>

<span id="data-unit"></span>
#### Data Unit

See [Data Unit](https://docs.byteplus.com/en/docs/18/22304#data-unit).

<span id="data-download"></span>
### Data Download

You can click the download button on the upper right side of the data table to download the metric data in the table. When you click the download button, you need to select the file format to download. The file formats available are **xlsx** and **csv**.

In the file naming convention,  *<YYYYMMDDHHMMSS\>*  represents the download time of the file, and  *<AccountID\>*  represents the ID of the primary account.


|**Type** |**Metric** |**Naming Convention for Downloaded Files** |
|---|---|---|
|User Requests Received by CDN |Client data transfer to CDN (traffic) |ByteplusCDN Domain_Ranking_Edge_in_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||CDN data transfer to client (traffic) |ByteplusCDN Domain_Ranking_Edge_out_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Client data transfer to CDN (bandwidth) |ByteplusCDN Domain_Ranking_Edge_in_bandwidth  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||CDN data transfer to client (bandwidth) |ByteplusCDN Domain_Ranking_Edge_out_bandwidth  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Non\-GET and non\-HEAD requests |ByteplusCDN Domain_Ranking_Edge_dynamic_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||GET and HEAD requests |ByteplusCDN Domain_Ranking_Edge_static_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Total requests |ByteplusCDN Domain_Ranking_Edge_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||2xx |ByteplusCDN Domain_Ranking_Edge_status_2xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||3xx |ByteplusCDN Domain_Ranking_Edge_status_3xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||4xx |ByteplusCDN Domain_Ranking_Edge_status_4xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||5xx |ByteplusCDN Domain_Ranking_Edge_status_5xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|Requests Send by CDN to Origins |Origin data transfer to CDN (traffic) |ByteplusCDN Domain_Ranking_Origin_in_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||CDN data transfer to origins (traffic) |ByteplusCDN Domain_Ranking_Origin_out_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Origin data transfer to CDN (bandwidth) |ByteplusCDN Domain_Ranking_Origin_in_bandwidth  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||CDN data transfer to origins (bandwidth) |ByteplusCDN Domain_Ranking_Origin_out_bandwidth  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Total requests |ByteplusCDN Domain_Ranking_Origin_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||2xx |ByteplusCDN Domain_Ranking_Origin_status_2xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||3xx |ByteplusCDN Domain_Ranking_Origin_status_3xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||4xx |ByteplusCDN Domain_Ranking_Origin_status_4xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||5xx |ByteplusCDN Domain_Ranking_Origin_status_5xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
