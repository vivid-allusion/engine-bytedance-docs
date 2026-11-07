---
title: "Configure storage lens dashboard"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Configure-pivot-dashboard"
---

This section describes the details of the Storage Lens dashboard for CloudLens for TOS in TLS.

The CloudLens for TOS Storage Lens dashboard allows you to configure the scope of bucket metric collection as needed, aggregates storage and access metrics by day, and supports quick view, trend, distribution, and TopN analysis. With the pivot dashboard, you can track storage capacity growth trends and identify the fastest\-growing buckets and prefixes. This helps you to determine whether storage growth aligns with expectations and optimize storage costs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>



* <div data-tips="true" data-tips-type="default"><strong>CloudLens for TOS Storage Lens</strong> is in closed beta. To request access for business needs, contact your account manager to add you to the allowlist.</div>


* <div data-tips="true" data-tips-type="default">The <strong>Prefix aggregation</strong> feature within the <strong>Advanced features</strong> functions is not currently supported.</div>



<span id="8a1a9451"></span>
## Notice


* A maximum of 50 dashboards can be created per account.

* For newly created storage lens dashboards, it may take up to 48 hours to view the corresponding data metrics. Subsequent data will be updated daily, displaying statistics from the previous day.

* Prefix metric data requires using the advanced metric collection method and enabling the prefix aggregation feature.

* When the storage lens dashboard resource meets the following conditions, the corresponding log topic/table topic will be deleted:

   
   |Resources |Deletion criteria |
   |---|---|
   |Log topic (`tos-lens-topic`) |All storage lens tasks in this storage region have been deleted. |
   |Table topic (named after the bucket) |The object storage bucket corresponding to this table topic is not associated with any storage lens task that has prefix aggregation enabled. |
   


<span id="d5bcf618"></span>
## Dashboard configuration steps


1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. Refer to [Integrate TOS log application](https://docs.byteplus.com/docs/tls/Integrate-TOS-log-application) to integrate the CloudLens for TOS log application.

3. In the left navigation bar, click **Common functions** \> **Log application**.

4. On the **My app** page, click the name of the integrated CloudLens for TOS log application.

5. On the **Storage Lens** page, click **Create dashboard** to enter the dashboard creation page.

6. Confirm the following information as prompted on the interface, then click **Create dashboard**.

   
   |Parameters |Description |
   |---|---|
   |Dashboard name |The name of the storage lens dashboard. Cannot be modified after creation.<br><br><br>* Can only contain numbers, letters a\-Z, and a hyphen `-`.<br><br>* Value range: 1 to 65 characters. |
   |Region |Used to store exported dashboard metrics. Cannot be modified after creation. |
   |Metric collection method |Select the metric collection method.<br><br><br>* Free metrics: Collects basic metrics and supports all regions and buckets.<br><br>* Advanced features: In addition to free metrics, supports activity metrics and prefix aggregation. Only available for specified regions and buckets. Metrics are stored for 15 months. |
   |Filter metrics |View the filtered collected metrics. The metric categories are as follows.<br><br><br>* Activity metrics (only for the **Advanced features** collection method): Includes uploaded bytes and deleted bytes.<br><br>* Summary metrics: Includes total storage and total object count.<br><br>* Cost optimization metrics: Includes historical version bytes, historical version object count, and unmerged multipart upload bytes.<br><br>* Data protection metrics: Includes current version bytes and current version object count. |
   |Prefix aggregation |<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <strong>Prefix aggregation</strong> feature within the <strong>Advanced features</strong> functions is not currently supported.</div><br><br><br>When the **Metric collection method** is set to **Advanced features**, prefix aggregation can be configured.<br><br>Supports aggregating storage metrics by prefix dimension, which can be used to analyze the storage usage distribution of each prefix. After enabling it, configure the prefix range as follows.<br><br><br>* Prefix threshold (%):<br><br>   * Prefix threshold: Set the minimum prefix threshold size. For example, a prefix threshold of 5% means aggregating prefixes that account for 5% or more of the total storage size of the bucket. The supported range is an integer from 1 to 100.<br><br>   * Prefix depth: The maximum number of levels for a prefix. The supported range is an integer from 1 to 10.<br><br>   * Prefix separator: Supports selecting `/` or custom. When custom is selected, only a single character can be entered.<br><br>* Specify prefix:<br><br>   * The prefix is effective at the bucket level. When entering, do not include the bucket name.<br><br>      For example, to specify the prefix `test` in the bucket named `abc`, only enter `test` in the add prefix field, rather than `abc/test` or `/test`.<br><br>   * Up to 50 specified prefixes can be added. |
   |Region and bucket |Select the region and bucket where the TOS bucket for the storage lens dashboard to be created is located, or exclude specified regions and buckets.<br><br><br>* You can select all regions, all buckets, or specified buckets in specified regions.<br><br>* After enabling prefix aggregation, excluding regions and buckets is not supported. |
   |Export metrics |You can configure the data in this dashboard to be exported once per day and sent to the target TOS bucket for use in your chosen analytics tool. After enabling, you need to configure the relevant output information:<br><br><br>* Output format: Supports CSV and Parquet.<br><br>* Target bucket: Set the target bucket. If the target bucket is set to public read (write), there is a risk of metric file leakage.<br><br>* Metric prefix: After setting the metric prefix, metrics will be delivered to the `target bucket/specified prefix/` ** **  path. Please go to this path to view them.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">Complete the following authorizations as prompted:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Authorize the TOS Object Storage Service to read and write files in your bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Authorize the TOS Object Storage Service to access your KMS service.</div><br> |
   

7. After successful creation, on the **Access management** tab of the storage lens dashboard, click the dashboard name to view the storage lens dashboard. For dashboard details, refer to [Storage lens metric analysis](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#68ed3195).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Notice   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">On the <strong>target storage topic</strong> tab, you can view information such as the project name, topic name, region, topic type, and creation time for storage lens data storage.   </div>
   

<span id="68ed3195"></span>
## Storage Lens metric analysis

The monitoring charts in the storage lens dashboard of the CloudLens for TOS log application are categorized into types such as overview, region, storage type, storage bucket, and prefix. Details of each metric type are as follows.


|Category |Description |
|---|---|
|[Overview](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#84bab49a) |Display metric snapshots, metric details, trends and distribution, TopN snapshots, and incremental TopN prefix. |
|[Region](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#9f87f946) |Display the trends, distribution, bubble diagram, and data details of the corresponding metrics within the specified area. |
|[Storage types](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#1f805bf2) |Display the corresponding metrics trends, distributions, bubble chart, and detailed data for the specified storage type. |
|[Bucket](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#1fb4b120) |Display trends, distributions, bubble charts, and detailed data for corresponding metrics in the specified bucket. |
|[Prefix](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard#f0cdb26f) |Displays the trends, distributions, bubble charts, and detailed data for the specified metrics under the given prefix.<br><br>The advanced feature metric collection method must be used, and prefix aggregation must be enabled. |


The functions and related limitations of each metric chart are described as follows:


* Snapshot

   Snapshot charts can only be viewed in the overview.

   Display snapshot information for the specified date, including total storage, object count, average object size, and bucket count.

* Trend (line chart)

   The line chart supports setting the **date range** and will show the trend of metric data over a specified period. Hovering the mouse over the line allows you to view specific metric data.

   The supported date range and time interval unit for the line chart are affected by the following conditions. Please refer to the actual chart display.

   
   |Impact type |Description |
   |---|---|
   |Date range |* Advanced features enabled:<br><br>   The maximum supported **date range** is **the last 15 months**, which means you can view up to 15 months of metric data.<br><br>* Advanced features not enabled:<br><br>   The maximum supported **date range** is **the last 14 days**, which means you can view up to 14 days of metric data. |
   |**Time interval unit** between data points on the line chart |* Date range ≤ last 45 days: The time interval unit is **day**.<br><br>* Date range is the last 90 days: The time interval unit is **week**.<br><br>* Date range ≥ last 120 days: The time interval unit is **month**. |
   

* Distribution (bar chart)

   The bar chart visually displays the total metric data for the specified date, making it easier to identify data change characteristics.

   Hovering the mouse over a data bar allows you to view the total metric data for the specified date.

* Bubble chart

   Set the **X axis**, **Y axis**, and **size** to display the distribution and aggregation of total metric data for the specified date.

   Hovering the mouse over a dot allows you to view specific metric data for the specified date.

* Data details

   Display detailed data information for the specified metric category in table format.

* Snapshot top N

   Snapshot top N charts can only be viewed in the overview.

   Display the top N metric data and percentage of the total from the perspectives of prefix (advanced features must be enabled), region, and bucket.

   The prefix dashboard displays prefixes in the format bucket name/prefix. For example, if the dashboard displays the prefix as test/aaa, it means the prefix is aaa and the bucket name containing the prefix is test.

* Increment of top N prefixes

   The increment chart for top N prefixes can only be viewed in the overview.

   In the **increment of top N prefixes** area, set the **reference date** and **top N** to view the storage growth of **top N prefixes** and analyze the trend changes. The explanations for each metric are as follows:

   
   |Metric |Description |
   |---|---|
   |Directory |TOP N prefixes, with the prefix format as bucket name/prefix. |
   |Current capacity |The prefix storage amount for the current date, which can be set at the top of the dashboard details page. |
   |Incremental change |Incremental change = Prefix storage amount on the current date \- Prefix storage amount on the baseline date<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can set the current date at the top of the dashboard details page.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can set the baseline date in the <strong>Increment of TOP N Prefixes</strong> dashboard.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The TOP N prefixes for the current date and the TOP N prefixes for the baseline date may differ. If a TOP N prefix for the current date does not exist in the TOP N prefixes for the baseline date, the storage lens dashboard will display a period\-over\-period increment of 0 for that prefix.</div><br><br><br>   <div data-tips="true" data-tips-type="default">For example, if the current date is 2025\-05\-16 and the TOP 3 prefixes are aaa, bbb, and ccc, and the baseline date is 2025\-03\-15 with TOP 3 prefixes aaa, bbb, and ddd, since the ccc prefix does not exist in the TOP 3 prefixes of the baseline date, the period\-over\-period increment for the ccc prefix is displayed as 0.   </div><br>    |
   |Rate of incremental change |Rate of incremental change = (Prefix storage amount on the current date \- Prefix storage amount on the baseline date) / Prefix storage amount on the baseline date |
   


<span id="700bb109"></span>
## Storage Lens chart summary

<span id="84bab49a"></span>
### Overview

Display snapshot, metric details, trend, and other information for each metric. It supports filtering by region, storage type, bucket, prefix, and specified date, and displays the following charts.


<Tabs>
<Tab zoneid="ZBosao1KaS" title="Snapshot">
<TabTitle>Snapshot</TabTitle>

Display the snapshot information for the specified date, including total storage, object count, average object size, and bucket count.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/462e70c2f9bd49b4be06680ae22630bb) </span>


</Tab>
<Tab zoneid="wuR598smrV" title="Metric details">
<TabTitle>Metric details</TabTitle>

Select a metric category to display detailed information for the metric on the specified date:


* Metric categories: summary metrics, cost optimization metrics, and data protection metrics

* Metric name:

   * Total storage, total object count, current version bytes, and current version object count

   * Historical version bytes, historical version object count,

   * Unmerged multipart upload bytes, unmerged multipart upload object count


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a30a1bafceee4b7983ad497fadc9d2e2) </span>


</Tab>
<Tab zoneid="xrLD9d5bhQ" title="Trend and distribution">
<TabTitle>Trend and distribution</TabTitle>

The trend distribution includes line charts and bar charts. Select a specified metric and date range (such as the last 7 days or the last 14 days) to display the trends of the metric, region, and storage type data.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/805aafcbf4204334a426223a6b19be45) </span>


</Tab>
<Tab zoneid="CUXvmRFT2T" title="Snapshot TopN">
<TabTitle>Snapshot TopN</TabTitle>

Select a specified metric and TopN quantity to view the TopN snapshot information of the metric's prefix, region, and bucket.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/88e969a957cc4452a01eab7ffe44a853) </span>


</Tab>
<Tab zoneid="HP14XBmVx4" title="Increment of TOPN prefixes">
<TabTitle>Increment of TOPN prefixes</TabTitle>

Select a baseline date, specified metric, and TopN quantity (N is 1–100) to view the TopN incremental information of the metric's prefix based on the baseline date.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/dcb9a76d4a1843be92bb017b17292e72) </span>


</Tab>
</Tabs>


<span id="9f87f946"></span>
### Region

Display top N charts (N is 1–50) for the specified metric by region. Chart details are as follows:


<Tabs>
<Tab zoneid="EjyLOthLRT" title="Trends">
<TabTitle>Trends</TabTitle>

Select a date range to display the trends of the metric within that date range, such as the last 7 days or the last 14 days.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/96fcfbaceffd48ebaa426b28f3f53f5a) </span>


</Tab>
<Tab zoneid="K1KFUpiF9I" title="Distribution">
<TabTitle>Distribution</TabTitle>

Display the distribution of the metric on the specified date.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c4a975c223e24a558f7831e30c47820a) </span>


</Tab>
<Tab zoneid="MM6mq6RKzZ" title="Bubble charts">
<TabTitle>Bubble charts</TabTitle>

Select the X\-axis, Y\-axis, and size of the metric bubble chart to display the regional distribution bubble chart of the corresponding metric on the specified date.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/69e843f4cd0e471fbae274397c738e72) </span>


</Tab>
<Tab zoneid="mP8YbxeEAH" title="Data details">
<TabTitle>Data details</TabTitle>

Select the metric category to display the detailed data information of that category in the region.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a572a6c7fabe4265a61f7137ec0f40ec) </span>


</Tab>
</Tabs>


<span id="1f805bf2"></span>
### Storage class

Display Top N charts (N is 1\-50) for the specified metrics by storage class. Chart details are as follows:


<Tabs>
<Tab zoneid="gK44JlCyg8" title="Trends">
<TabTitle>Trends</TabTitle>

Select a date range to display the trends of the metric within that date range, such as the last 7 days or the last 14 days. 

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/920057ab55b5492e80b0c61e90015c1e) </span>


</Tab>
<Tab zoneid="DYtnJ7I3uz" title="Distribution">
<TabTitle>Distribution</TabTitle>

Display the distribution of the metric on the specified date.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/00c72246efb548d5980881da34ec4f28) </span>


</Tab>
<Tab zoneid="Hj3YMMT4EJ" title="Bubble charts">
<TabTitle>Bubble charts</TabTitle>

Select the X\-axis, Y\-axis, and size of the metric bubble chart to display the storage type bubble chart of the corresponding metric on the specified date.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9cf2b1015cd94d2a99a4bb1b6902242e) </span>


</Tab>
<Tab zoneid="ycA56SsGk2" title="Data details">
<TabTitle>Data details</TabTitle>

Select the metric category to display the detailed data information of that category across different storage types.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bc79104663584f62a82dd4e27a5986ec) </span>


</Tab>
</Tabs>


<span id="1fb4b120"></span>
### Bucket

Display Top N charts (N is 1\-50) for the specified metrics by bucket. Chart details are as follows:


<Tabs>
<Tab zoneid="Uf4ihWIyGG" title="Trends">
<TabTitle>Trends</TabTitle>

Select a date range to display the trends of the metric within that date range, such as the last 7 days or the last 14 days. 

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0e173d4d1ada4216831e0e49eb8231ea) </span>


</Tab>
<Tab zoneid="cJfa6vBxBU" title="Distribution">
<TabTitle>Distribution</TabTitle>

Display the distribution of the metric on the specified date.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bca6507f2cbe4eb584395e6e408f2d23) </span>


</Tab>
<Tab zoneid="wprT0uVKv8" title="Bubble charts">
<TabTitle>Bubble charts</TabTitle>

Specify the X\-axis, Y\-axis, and size of the bubble chart as the specified metric to view the bucket bubble chart of the metric on the specified date.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b040ce0f2ea94b5e863548463004ac29) </span>


</Tab>
<Tab zoneid="GURjhyYoUh" title="Data details">
<TabTitle>Data details</TabTitle>

Select the metric category to display the detailed data information of that category across different buckets.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/eb6bcf37ccdf45589ba4c322466e6c89) </span>


</Tab>
</Tabs>


<span id="f0cdb26f"></span>
### Prefix

Display Top N charts (N is 1\-50) for the specified metrics by prefix. Chart details are as follows:


<Tabs>
<Tab zoneid="EsymauQZAS" title="Trends">
<TabTitle>Trends</TabTitle>

Select a date range to display the trends of the metric within that date range. For example, the last 7 days or the last 14 days.


</Tab>
<Tab zoneid="ZzSPPFPWpI" title="Distribution">
<TabTitle>Distribution</TabTitle>

Display the prefix distribution of the metric on the specified date.


</Tab>
<Tab zoneid="foOjUnpzVy" title="Bubble charts">
<TabTitle>Bubble charts</TabTitle>

Specify the X\-axis, Y\-axis, and size of the bubble chart as the specified metric to view the prefix bubble chart of the metric on the specified date.


</Tab>
<Tab zoneid="XDnNnn1g3R" title="Data details">
<TabTitle>Data details</TabTitle>

Select a metric category to display detailed data information for different prefixes of that category.


</Tab>
</Tabs>
