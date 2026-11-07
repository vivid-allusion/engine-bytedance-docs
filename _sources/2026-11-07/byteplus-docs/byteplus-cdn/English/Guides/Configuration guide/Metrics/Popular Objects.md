---
title: "Popular Objects"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/og-CdZ"
---

The **Popular Objects** page in BytePlus CDN provides ranked analytics to help you identify your most requested content and understand user traffic patterns. You can view top\-ranked URLs, referers, user agents (such as devices, browsers, and operating systems), and client IP addresses based on metrics like traffic volume and request counts. This document explains how to query and filter this data, understand the ranking logic, and download reports to gain deeper insights into your content's performance and audience engagement.

When you query metric data, you need to specify a statistical time period. You can query data for up to the past 92 days, but the time span of a single query cannot exceed 31 days. You can also specify conditions to filter requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you are new to the Popular Objects page, we recommend reading the following documents to better understand the concepts described here.</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1">Statistical Time Period</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4">Metrics Reference</a>. In this document, focus on the calculation methods for aggregate data of traffic, requests, and status codes.</div>


* <div data-tips="true" data-tips-type="tip">The metric data calculated at the cache node may change due to network jitter. In most cases, metric data stabilizes within 12 hours.</div>


* <div data-tips="true" data-tips-type="tip">The popular objects are based on hourly granularity metric data. Therefore, the data statistics may have a delay of about 2 hours. For example, data for the 09:00 to 10:00 period will be accurate around 11:00.</div>



<span id="introduction"></span>
## Introduction

On the **Popular Objects** page, you can obtain the popular objects analyzed by CDN based on user requests and the metric data of these objects.


* Popular URLs under the domain name

* Popular Referer domains

* Popular access devices

* Popular operating systems

* Popular browsers

* Top client IP addresses

* Popular regions


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9971d06be3d3e542ae5f06e19250a8dc.png) </span>

<span id="ranking-logic-of-popular-objects"></span>
## Ranking Logic of Popular Objects

This page displays the top 1,000 popular objects. The CDN does not simply aggregate data for each object over a specified time period to obtain the top 1,000 popular objects. Instead, it follows these steps:


1. The CDN calculates the top 1,000 popular objects for each 5\-minute interval.

2. The CDN then calculates the aggregate data for each object identified in step 1, using the data from each 5\-minute interval.

3. Using this aggregate data, the CDN determines the final top 1,000 popular objects.


<span id="data-filtering"></span>
## Data Filtering

You can specify the following filtering types to filter user requests.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7e3db9eae982c1c34e9338e82029bf88.png) </span>


|**Filter type** |**Description** |
|---|---|
|Project |Collects metric data at the project level. If no project is specified, the metric data is collected at the domain name level.<br><br>&nbsp;<br><br>**Example**<br><br>Consider the following scenario:<br><br><br>* The specified statistical time period is from 8:00 to 10:00 on a certain day.<br><br>* Domain name X is transferred from another project to project A at 9:00. Domain name Y has always been in project A.<br><br><br>In this scenario,<br><br><br>* Suppose you specify both project A and domain names X and Y. In this case, you get the project\-level metric data, covering:<br><br>   * The metric data of domain name X from 9:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00.<br><br>* Suppose you do not specify project A but specify domain names X and Y. In this case, you get the domain name\-level metric data, covering:<br><br>   * The metric data of domain name X from 8:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00. |
|Domain Name |Indicates one or more domain names used to filter user requests. You can specify up to 50 domain names, separated by commas. If you do not specify a domain name, this filter is not applied.<br><br>&nbsp;<br><br>Please note:<br><br><br>* If a project is specified, you get the project\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of the project during the statistical time period, the metric data will be affected.<br><br>* If no project is specified, you get the domain name\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of any project during the statistical time period, the metric data will not be affected.<br><br><br>See the example in the "Project" description.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For IAM users, the domain name list includes the domain names they have permission to access.</div><br> |
|Area Type |**Area Type** only appears when you are on the **Top Regions** tab, and is used to get the distribution of the client IP addresses within that type of area. This configuration has the following options:<br><br><br>* Global: Indicates countries and regions around the world.<br><br>* China: Indicates provincial administrative regions in China. |


<span id="popular-object-types"></span>
## Popular Object Types

For user requests that match the filter criteria, the CDN displays the following types of popular objects. For each type, the CDN displays up to 1,000 popular objects.


|**Popular Object Type** |**Description** |
|---|---|
|Top URLs |Request URLs are sorted based on aggregate data for traffic, requests, and status codes respectively.<br><br><br>* Traffic: Indicates ranking of request URLs based on the amount of data transferred by the CDN to users.<br><br>* Requests: Indicates that request URLs are sorted based on the number of user requests received by the CDN.<br><br>* Status Codes: Indicates that request URLs are sorted based on the number of CDN response status codes of the specified category. The status code categories you can specify are 2xx, 3xx, 4xx, and 5xx. |
|Top Referers |Display popular Referers based on aggregate data of traffic and requests respectively.<br><br><br>* Traffic: Indicates that the Referers in requests are sorted based on the amount of data transferred by the CDN to users.<br><br>* Requests: Indicates that the Referers in requests are sorted based on the number of user requests received by the CDN. |
|User\-Agent |This category ranks objects based on information from the User\-Agent header. You can choose to rank by device, browser, or operating system, sorted by either traffic or number of requests.<br><br>&nbsp;<br><br>For example, if you select device:<br><br><br>* Traffic: Ranks client device types by the amount of data the CDN transfers to users.<br><br>* Requests: Ranks client device types by the number of user requests received by the CDN.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Device types include COMPUTER, MOBILE, TABLET, DMR, GAME_CONSOLE, etc.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Browsers include BOT, CHROME, IE, MOZILLA, SAFARI, DOWNLOAD, etc. DOWNLOAD corresponds to those requests sent via scripts (wget, cURL, etc.).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Operating systems include Windows, Android, macOS, Linux, IOS, etc.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If an object's device type, browser, or operating system is not recognized, the object's type will be UNKNOWN.</div><br> |
|Top Client IP Addresses |Client IP addresses are sorted by aggregate data of traffic and requests respectively.<br><br><br>* Traffic: Indicates the ranking of client IP addresses based on the amount of data the CDN transfers to users.<br><br>* Requests: Indicates the ordering of client IP addresses based on the number of user requests received by the CDN. |
|Top Regions |Indicates that countries and regions, as well as provincial administrative regions in China are sorted based on the number of client IP addresses. |


<span id="time-granularity-and-statistical-time-period"></span>
## Time Granularity and Statistical Time Period

On the page, you also need to specify the time granularity and statistical time period.


* Time granularity determines the time interval between data points.

* The options for statistical time period are **Today**, **Yesterday**, **Past 3 Days**, **Past 7 Days**, **Past 30 Days**, **This Month**, and **Last Month**. You can also specify an arbitrary time period within the past 92 days, down to the minute. The default is **Today**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At the top of the page, you can specify the time zone of the statistical time period. The default time zone is UTC+08:00.</div>


When calculating metric data, the time granularity used by CDN is 5 minutes. The selected time granularity affects the available time range.

<span id="metric-data"></span>
## Metric Data

After you set the filter conditions and the statistical time period, you can click **Query** to view popular objects of various types.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_929270ad6ce7061ccc98833586f6f9b2.png) </span>

<span id="data-unit"></span>
## Data Unit

CDN uses default units and bases to display metric data. You can specify other units and bases on the page. If you specify a different unit or base, the metric data will be updated accordingly.

The available units for each metric are as follows:


|**Metric** |**Base** |**Available Units** |**Default Unit** |
|---|---|---|---|
|Traffic |1,000 |KB, MB, GB, TB, and PB |GB |
|Requests |Not applicable |Thousands, Millions, Billions |Millions |
|2xx Status Codes ||||
|3xx Status Codes ||||
|4xx Status Codes ||||
|5xx Status Codes ||||
|Client IP Addresses |||Thousands |


<span id="data-download"></span>
## Data Download

Click the download button in the upper\-right corner of the list to download the displayed popular objects and their metric data. When you click the download button, you need to select the file format to download. The file formats available are **xlsx** and **csv**.

For each popular object type, the naming convention of the downloaded file is as follows. In the file naming convention,  *<YYYYMMDDHHMMSS\>*  represents the download time of the file, and  *<AccountID\>*  represents the ID of the primary account.


|**Popular Object Type** |**Metric** |**Naming Convention for Downloaded Files** |
|---|---|---|
|Top URLs |Traffic |ByteplusCDN statistical_ranking_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Requests |ByteplusCDN statistical_ranking_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||2xx Status Codes |ByteplusCDN statistical_ranking_status_2xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||3xx Status Codes |ByteplusCDN statistical_ranking_status_3xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||4xx Status Codes |ByteplusCDN statistical_ranking_status_4xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||5xx Status Codes |ByteplusCDN statistical_ranking_status_5xx  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|Top Referer |Traffic |ByteplusCDN statistical_ranking_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Requests |ByteplusCDN statistical_ranking_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|User\-Agent |Traffic |ByteplusCDN statistical_ranking_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Requests |ByteplusCDN statistical_ranking_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|Top Client IP Addresses |Traffic |ByteplusCDN statistical_ranking_traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
||Requests |ByteplusCDN statistical_ranking_requests  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
|Top Regions |Client IP Addresses |ByteplusCDN statistical_ranking_clientip  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
