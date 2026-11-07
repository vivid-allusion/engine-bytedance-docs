---
title: "Visual Query Configuration for Datasets"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Visual_Query_Configuration_for_Datasets"
---

<span id="_1-概述"></span>
# 1. Overview

In the dataset list, the actions for each individual dataset include the visual query configuration for the dataset. Intelligent Data Insight supports configuring certain properties of datasets in a visual manner when participating in frontend query analysis. This feature module is mainly related to query performance when there are a large number of datasets. It is generally recommended to enable it when query speed is too slow, and dataset administrators or data\-related personnel are advised to make this determination.

<span id="_2-快速入门"></span>
# 2. Quick start

(1) Enter your project.

(2) Click Datasets.

(3) Click the configuration option for the corresponding dataset in the dataset list (as shown in the figure).

(4) Click "Visual Query Configuration".

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In version V2.40 and earlier, this feature was called "Visualization Feature Switch".</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/142588b5be394b278330bf741f4e45c3~tplv-goo7wpa0wc-image.image) </span>

(5) As shown in the figure below, you can configure push control, query control, and more settings as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b7b4e0de3794f86a2cb011367df6132~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In version V2.40 and earlier, this feature only included three features: automatic query, dataset subscription/subscription, and creating a new monitor.</div>


<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-推送控制"></span>
## 3.1 Push control

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef289a8efb064379bcfb5551fcc55de3~tplv-goo7wpa0wc-image.image" width="613px" /></div>


<span id="_3-1-1-数据集订阅"></span>
### 3.1.1 Dataset subscription


* Datasets are generally allowed to be subscribed to in analysis queries. When the data itself consists of a large volume of detailed records, it is recommended to disable this feature (that is, select Not Allowed).

* Once Not Allowed is selected, the dataset will not participate in subscription queries, and the chart data created from it will not be displayed in dashboard subscription screenshots. However, it will still display normally when the dashboard is actually opened. As shown in the figure below, the dataset for the chart on the left has subscription set to [Not Allowed], while the dataset for the chart on the right is set to the default [Allowed].

* Selecting [Not Allowed] for subscription does not affect the use of the dataset in visual queries or viewing specific data normally in the dashboard.


<span id="_3-1-2-新建监控"></span>
### 3.1.2 Create monitoring task


* Datasets are generally allowed to be monitored in analysis queries. However, when the data itself consists of a large volume of detailed records, it is recommended to disable this feature (that is, select Not Allowed).

* Once "Not allowed" is selected, the dataset will not participate in creating new monitoring, and the [Create Monitoring] feature for charts created from this dataset will be unavailable. As shown in the figure below, the left chart dataset has "Create Monitoring" set to "Not allowed", while the right chart dataset defaults to "Allowed".

* Selecting "Not allowed" for creating monitoring does not affect usage in visual queries or normal viewing of specific data in dashboards.


<span id="_3-2-查询控制"></span>
## 3.2 Query control

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/449cef62d903439988a06ffb1953a9f2~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-2-1-自动查询"></span>
### 3.2.1 Auto query


* The [Auto Query] feature for visual queries corresponding to the dataset is enabled by default. If the data itself consists of a large volume of detailed records, it is recommended to disable this feature by selecting "Not allowed".

* After selecting "Not allowed", auto query will be disabled by default during visual queries. Data will only be queried from the dataset after manually clicking the Query button.

* Disabling auto query does not affect dashboard presentation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1369c32e061c4558b6f3a1b8d56a5811~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-筛选搜索优化"></span>
### 3.2.2 Filter search optimization


* This feature affects [Dimension Filter](https://docs.byteplus.com/docs/DataWind/Dimension_Filtering) and [Filtering](https://docs.byteplus.com/docs/DataWind/Filtering).

* When set to "Allowed", the filter will prioritize using frontend cache when searching for data items in the exact search list, resulting in higher filtering efficiency.

* When set to "Not allowed", searching for data items in the list will query all backend data from the past 30 days to ensure data integrity. If the partition does not cover 30 days, the actual number of days will be used.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the datasets in the filter come from multiple datasets, and some are set to allow filter search optimization while others are not, all will be treated as not allowing filter search optimization.</div>


<span id="_3-2-3-查询天数限制"></span>
### 3.2.3 Query day limit

Users can set a query day limit for the dataset. After the limit is set, dataset users can only query data within the restricted number of days.

**Note:**  If the dataset in use has already been configured with a "maximum query days" restriction for visual queries, then when performing queries and configuring filters based on this dataset in visual queries, the filter will also be applied. When the maximum query days set for the dataset is less than or equal to the "Show only sampled data from the last N days" setting, only sampled data from the last N days will be displayed.

<span id="_3-2-4-明细字段"></span>
### 3.2.4 Detail fields

Supports setting fields in the dataset as detail fields. When no metrics are added to the query, these fields can only be used for detail queries.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/646509973136442fb6fbbace9c8b6785~tplv-goo7wpa0wc-image.image" width="610px" /></div>


You can click to switch to the detail table to perform a detail query.

<span id="_3-3-更多"></span>
## 3.3 More


* Default visualization query


Supports setting a default visualization query link for the current dataset. After configuring the default visualization query link, when users open the visualization query for the dataset, they will automatically enter the configured default query.

<span id="_3-4-超时节点"></span>
## 3.4 Timeout nodes


* When querying a very large amount of data, the data return time can be long. If data accuracy is not strictly required in this case (for example, if the aggregated statistical result is 100, it is acceptable to return a result of 99.98), you can allow discarding timeout nodes.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please use this feature with caution</div>



* After enabling discarding, you need to set the timeout duration and error ratio.

   * Timeout duration: The time taken for each data query node to return data. The default value is 100 ms and can be adjusted as needed. If the query time for a node exceeds this duration, the data result from that node will not be returned.

   * Error ratio: For example, if it is set to 0.100, and the number of nodes exceeding the above duration divided by the total number of query nodes is greater than or equal to 10 percent, the dataset query will report an error and no data will be returned. If the number of nodes exceeding the above duration divided by the total number of query nodes is less than 10 percent, the dataset query will return data normally. Note: The precision of this ratio is to three decimal places.

* By default, timeout nodes are not discarded, and this will not affect data results in visualization queries and dashboards.


<span id="_3-5-对历史存量资源的影响"></span>
## 3.5 Impact on historical data resources


|**Resource description** |**Automatic query** |**Subscription / dataset subscription** |**Create monitoring** |**Filter search optimization** |**Timeout node** |
|---|---|---|---|---|---|
|Dataset |No impact, allowed by default |No impact, allowed by default |No impact, allowed by default |No impact, allowed by default |No impact, not allowed by default |
|Visual query chart |No impact, allowed by default |No impact, allowed by default |No impact, allowed by default |No impact, allowed by default |No impact, not allowed by default |
|Dashboard |No impact, allowed by default |No impact, allowed by default |No impact, allowed by default |No impact, allowed by default |No impact, not allowed by default |


<span id="_3-6-长周期查询配置"></span>
## 3.6 Long\-period query configuration


* When querying data over a long time period, it supports using the Presto engine to query Hive tables.


<span id="_3-7-null-join"></span>
## 3.7 Null join


* When there are doubts about the visualization query results, if the current query includes LOD, visualization join, period\-over\-period, or comparison functions, a null value prompt will be displayed. Click "Go to enable" to close the current troubleshooting pop\-up and open "Query configuration".

* In the "Query configuration" window, you can configure caching, sampling, and join options.

* Null join explanation:

   * When the current query uses visual join, period\-over\-period comparison, comparison, or when a field involved in charting is an lod field, Null join configuration is supported.

      * Null join configuration only supports extract\-type datasets.

      * The configuration corresponding to "join" is displayed, and it is not selected by default.

      * If the above conditions are no longer met, this option is grayed out and cannot be selected.


<span id="_4-faq"></span>
# 4. FAQ


* Why restrict whether users are allowed to enable the basic functions of "subscription" and "create monitoring" on datasets?


\-\-Because some users' datasets are extremely large and have poor query performance; at the same time, since subscriptions and monitoring periodically scan all data, they have a significant impact on the data storage and computing engine. For example, some full advertising detail list data is used in subscriptions or monitoring, and such scenarios are not recommended for use in subscriptions and monitoring. Therefore, for such large\-scale detail list data, switches are provided to control whether subscription and monitoring are allowed, so that users can adjust according to actual needs.
