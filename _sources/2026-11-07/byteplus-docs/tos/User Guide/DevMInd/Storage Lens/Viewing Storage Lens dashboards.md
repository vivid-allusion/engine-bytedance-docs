---
title: "Viewing Storage Lens dashboards"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Viewing-Storage-Lens-dashboards"
---

This topic explains how to view Storage Lens dashboard metrics.

<span id="61U711jl"></span>
## How data is aggregated

Storage Lens dashboards aggregate storage data from your account daily across five levels of granularity. These dashboards provide snapshots, metric details, and trend and distribution views to help you analyze metrics such as storage usage, object count, and storage type from multiple angles.


|Granularity |Description |
|---|---|
|Overview |Includes **Snapshot**, **Metric Details**, **Trends and Distribution**, and **Snapshot Top N** modules. You can view combined data for a specified date, trends and distributions of combined data within a certain time range, top N overview, and growth of top N prefixes. |
|Section |Includes **Trend, Distribution, Bubble Chart** and **Data Details** modules. You can view trends and distributions of data across regions over a specified time range, as well as combined data for each region on a given date. |
|Storage type |Includes **Trend, Distribution, Bubble Chart** and **Data Details** modules. You can view trends and distributions of data across storage types over a specified time range, as well as combined data for each storage type on a given date. |
|Bucket |Includes **Trend, Distribution, Bubble Chart** and **Data Details** modules. You can view trends and distributions of data across buckets over a specified time range, as well as combined data for each bucket on a given date. |
|Prefix |Includes **Trend, Distribution, Bubble Chart** and **Data Details** modules. You can view trends and distributions of data across prefixes over a specified time range, as well as combined data for each prefix on a given date.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This option is only available when <strong>advanced features</strong> is selected under <strong>Metric collection method</strong> and <strong>Prefix aggregation</strong> is enabled.</div><br> |


<span id="vU416Mso"></span>
## Dashboard modules


<Tabs>
<Tab zoneid="4DFhJ6be" title="Snapshot">
<TabTitle>Snapshot</TabTitle>

This module provides a static overview of your storage resources on a given date. It shows four core metrics: total storage, object count, average object size, and bucket count. This allows you to quickly assess the overall scale of your resources for that day.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bea477d6b4a2b96be9c96e90b286e91.png) </span>




</Tab>
<Tab zoneid="GCES4QzT" title="Metric Details">
<TabTitle>Metric Details</TabTitle>

The metric filter in this module allows you to quickly view detailed metric values for each category (Summary, Cost Optimization, and Data Protection) on the selected date. The details for each category are as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_48558e668da7196e49a69beb9e1131d2.png) </span>




</Tab>
<Tab zoneid="xiikD2Ns" title="Trends and Distribution">
<TabTitle>Trends and Distribution</TabTitle>

This module focuses on one or more specific metrics, combining a trend chart with distribution views by region and storage type. This allows you to track changes to the metrics over time and analyze the composition by region and storage type. You can also export detailed data on total storage, data uploaded, and data deleted. The module consists of the following sections:


|Section |**Time range** |**Content** |
|---|---|---|
|Trend |The date range selected in the Trends and Distribution section (default: 7 days) |A continuous daily trend of the selected metric(s), which helps you identify growth patterns, fluctuations, and anomalies. |
|Regions |The selected date |The proportional and absolute values of the selected metric(s) across regions. |
|Storage classes |The selected date |The proportion of the selected metric(s) across storage types such as Standard Storage, Infrequent Access Storage, and Archive. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de0e557175d0021b0f208d756c52290a.png) </span>




</Tab>
<Tab zoneid="mwpQ76p6" title="Snapshot Top N">
<TabTitle>Snapshot Top N</TabTitle>

This module displays the top N items for a specified metric on a given date, sorted by prefix, region, or bucket. It helps you quickly identify the objects that contributed the most to that day. The module consists of the following sections:


|**Section** |**Description** |
|---|---|
|Switch dimension |Sort the items by selecting **Prefix, Region, or Bucket**. Click the corresponding tab to change the view.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <strong>Prefix</strong> view is only available when <strong>advanced features</strong> is selected under <strong>Metric collection method</strong> and <strong>Prefix aggregation</strong> is enabled.</div><br> |
|Metric |Select the metric for which you want to see a ranking. You can choose from the following categories: summary, cost optimization, and data protection. |
|TopN |Specify the value for N. The larger the number, the more entries will be displayed. The current maximum is 100. |


<span id="UWvcUvhx"></span>
### <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_70149229caa852920c2424449961ebbd.png) </span>


</Tab>
<Tab zoneid="JAB0J2Tf" title="Bubble Chart">
<TabTitle>Bubble Chart</TabTitle>

To display the overall data distribution and aggregation for a selected date, configure the following: **X Axis**, **Y Axis**, and **Size**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9616a8a11d15ed7756bd304041bae418.png) </span>




</Tab>
<Tab zoneid="5rqUWSnd" title="Data Details">
<TabTitle>Data Details</TabTitle>

This module displays a table with the full set of metrics for the selected dimension (region, storage type, bucket, or prefix) and **metric category**, based on the chosen date.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6887fbc6c9bf8a4352532fadbd68628c.png) </span>




</Tab>
<Tab zoneid="WhunegcP" title="Top N Prefix Growth">
<TabTitle>Top N Prefix Growth</TabTitle>

This module displays the fastest\-growing prefixes (directories) on a specified base date and their month\-to\-month changes. This helps you quickly identify directories that are expanding rapidly for storage capacity attribution and management.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This module is only available when <strong>advanced features</strong> is selected under <strong>Metric collection method</strong> and <strong>Prefix aggregation</strong> is enabled.</div>



</Tab>
</Tabs>


<span id="r9UcSw7j"></span>
## 

&nbsp;
