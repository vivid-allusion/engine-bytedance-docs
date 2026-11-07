---
title: "Common FAQs for Visualization Queries"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Common_FAQs_for_Visualization_Queries"
---

<span id="_1-可视化查询"></span>
# 1. Visualization queries

<span id="_1-1-报错信息"></span>
## 1.1 Error messages

<span id="报错子查询涉及的数据集没有读取权限怎么办"></span>
### What should I do if the dataset involved in the subquery does not have read permission?

**Cause**

A subquery filter is used in the visualization query, and the chart for the subquery does not have permission.

**Solution**

Request permission to view the dataset corresponding to the subquery chart.

<span id="报错点数量超出限制怎么办"></span>
### What should I do if the number of data points exceeds the limit?

**Cause**

The number of data points rendered in the chart exceeds the rendering limit.

**Solution**

(1) Use a table to display the data.

(2) If the x\-axis of the chart is detailed time, click the time field in the dimension configuration bar to change the aggregation method. It is recommended to change the aggregation to hour, day, or month based on actual display requirements.

<span id="报错不支持的筛选值怎么办"></span>
### What should I do if the error indicates unsupported filter values?

**Cause**

There is an abnormal filter, which may be due to a mismatch between the filter field and the filter value type.

**Solution**

Check the filters in the filter bar. If you find an abnormal filter (for example, using a filter like "\>0" on a text\-type field), remove it and reconfigure the filter condition by dragging and dropping.

<span id="报错该图表使用的字段已删除怎么办"></span>
### What should I do if the error indicates that the field used by the chart has been deleted?

**Cause**

Some fields used by the chart have been deleted.

**Solution**

Contact the dataset owner to confirm whether there are replacement fields and reconfigure accordingly.

<span id="配置地图时报错该图表使用的维度字段必须设置地理角色"></span>
### When configuring a map, what should I do if the error indicates that the dimension field used by the chart must be set to a geographic role?

**Cause**

The dimension field used is not a geographic role field and needs to be matched to a geographic role.

**Solution**

Match the dimension field to a geographic role (you must have edit permission for the dataset being queried). For details on the operation: see [3.1 Edit geographic roles](https://docs.byteplus.com/docs/DataWind/Map#_3-1-%E7%BC%96%E8%BE%91%E5%9C%B0%E7%90%86%E8%A7%92%E8%89%B2).

<span id="配置同环比时报错时间设置范围为不限，不支持同环比设置"></span>
### When configuring year\-over\-year or month\-over\-month comparison, what should I do if the error indicates that the time range is set to unlimited and comparison is not supported?

**Cause**

The comparison is based on the date in the filter bar, and if the start or end time is set to "unlimited", comparison calculation cannot be performed in this case.

**Solution**

In the filter bar, modify the time range for period\-over\-period comparison based on the date, and set the start and end time (can be dynamic, but cannot be unlimited).

<span id="配置同环比时报错-datetime-类型非聚合时，不支持环比设置"></span>
### Error when configuring period\-over\-period comparison: when the datetime type is not aggregated, period\-over\-period comparison settings are not supported.

**Cause**

Period\-over\-period comparison is based on the date in the dimension bar, and the date in the dimension bar is detailed, unaggregated time. In this case, period\-over\-period comparison calculation cannot be performed.

**Solution**

Click the dimension in the dimension bar and select a method for date aggregation. It is recommended to aggregate by hour, day, or month as appropriate.

<span id="可视化查询报错-timeout-exceeded"></span>
### Visualization query error: Timeout exceeded

**Possible cause**

The query timed out, possibly due to cluster status or excessive data volume.

**Solution**

(1) Try querying again first.

(2) Shorten the query date range to reduce data volume.

Add filter conditions to reduce data volume.

<span id="可视化查询报错-too-many-simultaneous-queries"></span>
### Visualization query error: Too many simultaneous queries

**Possible cause**

Engine concurrency is too high.

**Solution**

(1) Try querying again.

(2) Contact the DataWind project manager to resolve the issue.

<span id="可视化查询报错-memory-limit-for-query-exceeded"></span>
### Visualization query error: Memory limit (for query) exceeded

**Possible cause**

The query data volume exceeds the limit, or the cardinality of group by / count distinct is too large, causing the query to fail.

**Solution**

(1) Shorten the query date range to reduce data volume.

(2) Add filter conditions to reduce data volume.

<span id="可视化查询报错-memory-limit-for-user-exceeded"></span>
### Visualization query error: Memory limit (for user) exceeded

Similar issue: Visualization query error: Memory limit (total) exceeded

**Possible cause**

(1) Heavy load, memory exceeded.

(2) The current query requires too much memory.

**Solution**

(1) Try querying again first.

(2) Shorten the query date range to reduce data volume.

Contact the DataWind project manager to resolve the issue.

<span id="可视化查询报错-unknown-identifier-字段名"></span>
### Visualization query error: Unknown identifier: field name

**Possible cause**

(1) The field in the error does not exist.

(2) The table is missing columns.

**Solution**

(1) Check whether the dimension or metric fields referenced in the visualization query refer to model fields that do not exist.

(2) Contact the DataWind project manager to resolve the issue.

<span id="可视化查询报错-table……doesn-t-exist"></span>
### Visualization query error: Table……doesn't exist

**Possible cause**

The table does not exist on the cluster. Possible situations:

(1) The table has been deleted.

(2) The table exists, but some cluster nodes are missing, resulting in abnormal errors.

**Solution**

(1) Check whether the underlying data table exists. If it does not exist, switch to another dataset for the query.

(2) If the table exists, contact the DataWind project manager to resolve the issue.

<span id="可视化查询报错-exceeded-max-value-of-hash-function"></span>
### Visualization query error: exceeded max value of hash function

**Possible cause**

There are too many dimension values in the dimension field. For example, uid

**Solution**

(1) Reduce the number of dimensions in the query.

(2) Shorten the query date range to reduce the amount of data queried.

(3) Add filter conditions to reduce the amount of data queried.

<span id="可视化查询报错-limit-for-bytes"></span>
### Visualization query error: Limit for bytes

**Possible cause**

The amount of data read by the query is too large.

**Solution**

(1) Shorten the query date range to reduce the amount of data queried.

(2) Add filter conditions to reduce the amount of data queried.

<span id="可视化查询报错-frequency-reaches-the-upper-limit"></span>
### Visualization query error: frequency reaches the upper limit

**Possible cause**

There are too many complex queries. To ensure stability, the concurrency limit is triggered.

**Solution**

(1) Shorten the query date range to reduce the amount of data queried.

(2) Add filter conditions to reduce the amount of data queried.

(3) Contact the product project manager to resolve the issue.

<span id="可视化查询报错-could-not-find-enough-connections-to-up-to-date-replicas"></span>
### Visualization query error: Could not find enough connections to up\-to\-date replicas

**Possible cause**

Cluster primary\-secondary synchronization exception, indicating an abnormal situation in the cluster.

**Solution**

Contact the product project manager to resolve the issue.

<span id="可视化查询报错-query-size-is-too-big"></span>
### Visualization query error: query size is too big

**Possible cause**

The SQL statement assembled by the visualization query is too long, possibly due to an overly long query field expression, such as an excessively long case when expression or other similar expressions.

**Solution**

Check and adjust the field expressions.

<span id="_1-2-筛选器常见问题"></span>
## 1.2 Common issues with filters

<span id="可视化查询结果日期和筛选选定的日期不匹配"></span>
### The date of the visualization query result does not match the date selected in the filter.

**Similar issues:** 

> Date option does not take effect

> The time selected in the filter is inconsistent with the time of the displayed or downloaded data.


**Possible cause:** 

The dimension date field displayed is not the same as the date field used as the filter. That is, the date field used for filtering and the date field used in the chart are not the same field.

**Solution:** 

Use the relevant business date field as the filter to select the data that actually meets the criteria.

<span id="可视化查询对单个字段筛选多个值"></span>
### Visualization query: filter multiple values for a single field

**Similar issues:** 

> How to use the IN and arrayhas functions

> How to filter multiple selections in visual query

> How to batch upload data for filtering


When filtering, you can use IN (one value per line) or upload a file (one value per line);

For fields in array format, use arrayhas (separate different values with commas)

<span id="_1-3-图表分析常见问题"></span>
## 1.3 Common issues in chart analysis

<span id="可视化查询如何取排序后的前n条结果"></span>
### How to retrieve the top N sorted results in visual query

Use visual analysis [Top N](https://docs.byteplus.com/docs/DataWind/Top_N).

<span id="可视化查询如何修改展示的数据格式"></span>
### How to modify the data format displayed in visual query

Click the configuration capsule for the corresponding dimension or indicator, click the triangle arrow on the capsule, and select Set Data Format

<span id="可视化查询对坐标轴起始值灵活配置"></span>
### Flexible configuration of starting values for coordinate axes in visual query

Select the configuration panel below the chart selection bar, click the corresponding coordinate axis, and configure the axis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb55e588e9f64e37a1067e87966805fc~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f56adb8b96040f8a88ad15495d073bd~tplv-goo7wpa0wc-image.image) </span>

<span id="如何增加临时的自定义维度和指标"></span>
### How to add temporary custom dimensions and indicators

**Similar issues:** 

> Fields added in visualizations are not visible to other users

> Fields newly added in visual query are not visible to other users

> How to view data for multiple indicators divided, added, calculated, or aggregated

> How to configure multiple indicators for division, addition, calculation, or aggregation


In the visual query interface, click the ⋮ next to the dataset name, select Add Field, choose to add an indicator or dimension, define the display name, expression, and description to add the corresponding field. Supports aggregate operations, arithmetic operations, and other common SQL functions.

**Fields added in the visualization interface are temporary fields and are only visible to you. To add permanent fields, dataset editing permissions are required. You can choose "Save to Dataset"** 

or add them in dataset editing, refer to [Field Configuration](https://docs.byteplus.com/docs/DataWind/Fields_Configuration).

<span id="如何在一个图表中，让不同指标展示不同的图表类型"></span>
### How to display different chart types for different indicators in a single chart

**Similar issues:** 

> How to display different line types for different indicators in a single chart


You can use a dual\-axis chart to achieve the effect of displaying different chart types in the same chart. How to use [Dual-Axis Chart](https://docs.byteplus.com/docs/DataWind/Dual-Axis_Chart).

In the chart area, select dual\-axis chart and configure the display method for the primary and secondary axes separately. You can also configure charts of the same type but with different line styles for the primary and secondary axes.

<span id="折线图中数据格式与在指标胶囊中设置的不一致"></span>
### The data format in the line chart is inconsistent with the format set in the metric capsule.

**Similar issues:** 

> The data format in the chart is inconsistent with the format set in the metric capsule.

> The data format in the bar chart is inconsistent with the format set in the metric capsule.

> The data format in the column chart is inconsistent with the format set in the metric capsule.


Please go to the chart configuration area, select the corresponding axis, and click Data Format to configure the settings.

<span id="坐标轴或图表中的数据格式如何调整"></span>
### How to adjust the data format in the axis or chart

**Similar issues:** 

> How to adjust the data scale in the axis or chart


You can click the dimension or metric capsule corresponding to the value and set the data format to adjust the value format in the field; you can also select the corresponding axis (X\-axis or Y\-axis) at the bottom of the chart selection area and click Data Format to adjust the axis coordinate format.

For details on field format and chart format configuration, see [Field Configuration](https://docs.byteplus.com/docs/DataWind/Fields_Configuration).

<span id="_1-4-查询慢"></span>
## 1.4 Slow query

<span id="可视化查询缓慢，转很久无法查询出结果"></span>
### Visualization queries are slow, and results cannot be retrieved after a long time.

Dashboard loading is slow

Refer to [How to Optimize Query Performance?](https://docs.byteplus.com/docs/DataWind/How_to_Optimize_Query_Performance) to adjust the query.

<span id="_1-5-图表下载常见问题"></span>
## 1.5 Common issues with chart downloads

<span id="下载可视化查询数据无反应无报错"></span>
### No response or error when downloading visualization query data

**Similar issues:** 

> Download failed

> Failed to download data, timeout prompt

> Export failed


**Possible causes:** 

(1) Not connected to the intranet environment;

(2) Large data volume, resulting in slow download

(3) Actual data volume is small, but the number of rows set for download is too large, resulting in slow download

(4) Visualization data download requires re\-querying the data; if the data volume is large or the current query resources are highly concurrent, this can also cause slow downloads

**Solutions:** 

(1) Check whether you are connected to the intranet;

(2) Wait patiently for 1 minute; if the data volume is large, it may take 1–2 minutes to initiate the download;

(3) Limit the number of rows to download based on the actual query volume. When the number of rows is too large, it will extend the query and download time;

(4) If the current chart's query speed is also slow, downloading data may be slower as well. Please wait patiently for the download to complete.

<span id="下载可视化查询数据行数小于设定行数"></span>
### The number of rows downloaded from the visualization query is less than the specified number of rows

(1) Check the actual amount of data to see if it is less than the number of rows to be downloaded.

(2) Check whether the top N feature is used. Disable top N before downloading.

(3) Check whether the number of rows entered during download is less than the specified number. If the data exceeds 100,000 rows, it is recommended to download a CSV file.

<span id="如何设置下载权限？如何控制单个图表的下载权限？"></span>
### How to set download permissions? How to control download permissions for a single chart?

 **(1) Global permission settings**

Users can control download permissions for all charts within the project in the project center. This operation requires administrator permissions, and the configuration takes effect globally.

 **(2) Single chart permission settings**

Users can configure whether a chart can be downloaded from the dashboard in the download settings of the chart's visualization query page. This operation only applies to the individual chart. If the download function for a chart is disabled, no one is allowed to download data from that chart.

<span id="_1-6-其他常见问题"></span>
## 1.6 Other common issues

<span id="可视化查询和-sql-查询结果不一致"></span>
### Inconsistent results between visualization queries and SQL queries

**Possible causes:** 

(1) The query logic of the visualization query and the SQL query is inconsistent.

(2) The maximum number of rows that can be downloaded from a visualization query table is 1,000,000. Incomplete data downloads may cause inconsistencies in comparison, but the actual data is consistent.

(3) Visualization query data anomalies

**Solutions:** 

(1) Click the query history icon in the upper left corner of the visualization query page to view the SQL details corresponding to the visualization. Compare them with the SQL query statement to confirm that the base table, field expressions, and filter conditions are all consistent.

(2) Limit the query range and download data in segments for comparison to ensure accuracy.

(3) If the query logic is consistent but the comparison results are indeed inconsistent, contact us for troubleshooting.

<span id="如何查看可视化查询的查询sql逻辑"></span>
### How to view the SQL logic of a visualization query

Click the query history icon in the upper left corner of the visualization query page to view the SQL statements of historical queries.

<span id="可视化查询如何将时间戳或文本类型的字段转换为时间格式"></span>
### How to convert timestamp or text\-type fields to time format in visualized queries

Click the ┇ icon in the upper right corner of the module on the left side of the visualization page, select Batch Edit Fields, and set the field type of the corresponding field to Date or DateTime

<span id="可视化查询中最近有数一天比数据集实际最近有数日期早"></span>
### The most recent data date in the visualized query is one day earlier than the actual most recent data date in the dataset

**Possible causes:** 

(1) The page has not been refreshed

(2) The synchronization success request was lost

**Solutions:** 

(1) Refresh the page

(2) Try to resynchronize the dataset

<span id="底层表更新后可视化查询没数据"></span>
### No data in visualized queries after the underlying table is updated

After new fields are added to the underlying table, you need to update the selected fields in the dataset model configuration; after updating, resynchronize the dataset so that the new fields will have data; once the new fields for the corresponding date have data, perform the corresponding visualized query.

<span id="可视化查询去掉某个维度后，查询界面无数据展示"></span>
### No data is displayed in the query interface after removing a dimension from the visualized query

Possible cause: Before deleting the dimension, sorting or other analysis functions were configured for that dimension. After deletion, the analysis fails, resulting in no display.

Solution: Click the Analysis tab next to the chart type selection area, find the error analysis module with a red exclamation mark in the upper right corner, delete the abnormal analysis module, and apply the changes.

<span id="看板保存成功，保存到哪里了"></span>
### Where is the dashboard saved after it is saved successfully?

Similar questions:

How to view and manage visualized charts after saving

You can go to Project Center \- Chart Management to view and centrally manage your saved charts; if they have been saved to a dashboard, you can also view them on the corresponding dashboard.

<span id="可视化图表使用问题"></span>
### Issues with using visualized charts

**Similar questions:** 

> How to calculate the total sum for a metric

> How to display data proportions

> How to display year\-over\-year and month\-over\-month data

> How to use the comparison analysis feature

> How to use funnel charts

> How to use histograms


Please refer to the help documentation for the corresponding [Table](https://docs.byteplus.com/docs/DataWind/Table) and [Sorting](https://docs.byteplus.com/docs/DataWind/Sorting) features

<span id="归因分析需要有什么使用条件"></span>
### What are the requirements for using attribution analysis

(1) The dimension must be in date format;

(2) The chart types are bar chart, column chart, line chart, or area chart. See [Intelligent Attribution](https://docs.byteplus.com/docs/DataWind/Intelligent_Attribution).

<span id="可视化查询时只看到最近一天的数据"></span>
### Only the most recent day's data is visible when performing a visualization query.

Please filter the query date by using the p_date field in the 'Filter' section or by selecting another date field. By default, the most recent day's data for p_date is selected when creating a visualization.

<span id="日期字段格式无法动态筛选"></span>
### The date field format cannot be dynamically filtered.

**Similar issues:** 

> After importing the date field into the system, it is not in date format. How to modify or filter it?


The field needs to be processed and converted to date format (dataset editing permissions are required. If you do not have permission, it is recommended to contact the dataset owner to perform this operation).

**Method 1:**  Click the upper right corner of the left sidebar in the visualization, select batch edit fields, locate the corresponding field, change the type to "Date" or "Datetime", and confirm.

**Method 2:**  Hover the mouse over the corresponding field and select Edit Expression.

Use functions such as toDate to convert the field to date or time type. Different formats of date/time may require different functions. Refer to [3. Date functions](https://docs.byteplus.com/docs/DataWind/Introduction_to_Commonly_Used_Functions#_3-%E6%97%A5%E6%9C%9F%E5%87%BD%E6%95%B0).

<span id="同环比衍生字段的数据为空"></span>
### The derived fields for period\-over\-period and year\-over\-year comparisons have empty data.

**Possible causes**:

(1) The business data for the comparison period is missing. Example: For order date "2020\-01\-20", the period\-over\-period data for one day earlier is "2020\-01\-19", but the data for order date = "2020\-01\-19" is empty.

(2) The comparison period is missing data for the same dimension. Example: The filter condition is [Order Date] = "2020\-01\-20", the dimension is "City", and the metric is "Sales amount". The period\-over\-period data for one day earlier is "2020\-01\-19". There is data for City = "Shanghai" on "2020\-01\-20", but there is no data for City = "Shanghai" on "2020\-01\-19", so the period\-over\-period calculation for "Shanghai" is empty.

**Solution**:

Self\-check: On the period\-over\-period configuration page, use "View calculation rules" to check the comparison period, change the date filter condition to the corresponding date, and verify whether the business data is complete or whether the corresponding dimension items exist. Take appropriate actions based on actual data needs, such as adjusting the comparison period or correcting the data.

Self\-check example:

(1) The period\-over\-period calculation for 1 day earlier is empty. Reason: Dataset synchronization failed one day ago, making it impossible to retrieve the corresponding period's data.

(2) The dimensions are "shop id and shop name", and the metric is "sales revenue". After performing the period\-over\-period comparison, the data was found to be empty. Reason: The "shop id" for the comparison period did not change, but the "shop name" changed, resulting in inconsistent conditions for the period\-over\-period comparison.
