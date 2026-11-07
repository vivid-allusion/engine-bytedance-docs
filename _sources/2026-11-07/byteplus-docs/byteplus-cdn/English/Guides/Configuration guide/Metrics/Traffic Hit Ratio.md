---
title: "Traffic Hit Ratio"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/17GTty"
---

To understand and optimize your content delivery performance, you can use the **Traffic Hit Ratio** page in the BytePlus CDN console. This guide explains how to query, visualize, and analyze your traffic hit ratio data.

You will learn to apply filters such as project and domain name, set specific time granularities, and compare data across different periods to gain insights into your cache efficiency.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you are new to the <strong>Traffic Hit Ratio</strong> page, we recommend reading the following documents first to understand the concepts and terminology used in this article.</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1">Statistical Time Period</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4">Metrics Reference</a></div>


* <div data-tips="true" data-tips-type="tip">The metric data calculated at the cache node may change due to network jitter. In most cases, metric data stabilizes within 12 hours.</div>


* <div data-tips="true" data-tips-type="tip">The data displayed on the page may have a delay of about 5 minutes.</div>



<span id="introduction"></span>
## Introduction

On the **Traffic Hit Ratio** page, you can query the traffic hit ratio data for user requests. You can specify filter conditions to filter user requests.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b9e9b5716b11e8a4f5962c1abf990efa.png) </span>

<span id="data-filtering"></span>
## Data Filtering

You can filter user requests by the following types.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a94b7b260d777f24914f72ce47d5da6b.png) </span>


|**Filter type** |**Description** |
|---|---|
|Project |Collects metric data at the project level. If no project is specified, the metric data is collected at the domain name level.<br><br>&nbsp;<br><br>**Example**<br><br>Consider the following scenario:<br><br><br>* The specified statistical time period is from 8:00 to 10:00 on a certain day.<br><br>* Domain name X is transferred from another project to project A at 9:00. Domain name Y has always been in project A.<br><br><br>In this scenario,<br><br><br>* Suppose you specify both project A and domain names X and Y. In this case, the query returns project\-level metric data, covering:<br><br>   * The metric data of domain name X from 9:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00.<br><br>* Suppose you do not specify project A but specify domain names X and Y. In this case, the query returns domain name\-level metric data, covering:<br><br>   * The metric data of domain name X from 8:00 to 10:00.<br><br>   * The metric data of domain name Y from 8:00 to 10:00. |
|Domain Name |Indicates one or more domain names used to filter user requests. You can specify up to 50 domain names. Multiple domain names are separated by commas (,). If no domain name is specified, it indicates that this filter type is not used to filter requests.<br><br>&nbsp;<br><br>Please note:<br><br><br>* If a project is specified, you get the project\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of the project during the statistical time period, the metric data will be affected.<br><br>* If no project is specified, you get the domain name\-level metric data for the specified domain names. This means that if these domain names are transferred into or out of any project during the statistical time period, the metric data will not be affected.<br><br><br>See the example in the "Project" description.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For IAM users, the domain name list includes the domain names they have permission to access.</div><br> |
|Billing Region |Specify a billing region to filter user requests to get requests from those regions. All billing regions are included by default. |


<span id="time-granularity-and-statistical-time-period"></span>
## Time Granularity and Statistical Time Period

On the page, you also need to specify the time granularity and statistical time period.


* Time granularity determines the time interval between each breakdown data.

* The options for statistical time period are **Today**, **Yesterday**, **Past 3 Days**, **Past 7 Days**, **Past 30 Days**, **This Month**, and **Last Month**. You can also specify an arbitrary time period within the past 92 days, down to the minute. The default is **Today**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At the top of the page, you can specify the time zone of the statistical time period. The default time zone is UTC+08:00.</div>


The time granularity you specify affects the following factors:


* The time span of the statistical period.

* The time granularity used by CDN when aggregating data.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN specifies the time granularity for data aggregation; you cannot adjust this setting.</div>


Details are shown in the table below:


|**Time granularity** |**Maximum time span of the statistical period** |**Data Aggregation Granularity** |
|---|---|---|
|1 minute |1 day |1 minute |
|5 minutes |3 days |5 minutes |
|1 hour |31 days ||
|1 day |||


In addition, time granularity also determines the actual statistical time period of metric data. See [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1).

To the right of the statistical time period, there is a **Compare** button. When you click **Compare**, you can specify another statistical period for comparison. CDN will calculate and display the breakdown data and aggregate data of traffic hit ratio for these two statistical time periods respectively.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fb18a965f9837dc5283d893ac1db2e30.png) </span>

<span id="metric-data"></span>
## Metric Data

After you set the filter conditions, time granularity and statistical time period, you can click **Query** to view the data of traffic hit ratio.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0f1bdcde6d066eaca1ed222d3c1182b7.png) </span>

Traffic hit ratio data includes aggregate and breakdown data within the statistical time period. Breakdown data is presented in a line chart with time on the horizontal axis, allowing you to understand trends in the data.

The page displays data for the following metrics:


|**Metric** |**Breakdown Data** |**Aggregate Data** |
|---|---|---|
|Traffic Hit Ratio |Displays the trend of traffic hit ratio within the actual statistical time period. |Displays the average traffic hit ratio within the actual statistical period. |


For the definitions and calculation methods of each metric, see [Metrics Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4).

<span id="timeline"></span>
## Timeline

There is a time axis at the bottom of the data trend chart, which reflects the actual statistical time period. You can drag the start and end time points to see a breakdown of the metric over a smaller time range.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a2aad733c4047b93d030555ef2449db6.png) </span>

<span id="data-download"></span>
## Data Download

To the right of the time granularity selector, you can download a breakdown of the metric in the trend chart. When you click the download button, you need to select the file format to download. The file formats available are **xlsx** and **csv**.

For traffic hit ratio, the naming convention of the downloaded file is as follows. In the file naming convention,  *<YYYYMMDDHHMMSS\>*  represents the download time of the file, and  *<AccountID\>*  represents the ID of the primary account.


|**Metric** |**Naming Convention for Downloaded Files** |
|---|---|
|Traffic Hit Ratio |ByteplusCDN traffic  *<AccountID\>* _ *<YYYYMMDDHHMMSS\>*  |
