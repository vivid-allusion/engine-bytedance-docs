---
title: "Visual Query Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Visual_Query_Overview"
---

<span id="_1-概述"></span>
# Overview

The data visualization feature in DataWind is called **visual query**, which is an important step from data to decision\-making.

Users can perform self\-service visual analysis based on the connected data without needing to know SQL syntax. By clicking or dragging, users can generate visual charts and gain data insights. This module supports a variety of chart and analysis settings, flexible filtering based on dimensions, dates, metrics, and dynamic dimensions/dynamic metrics, interactive analysis such as drill\-up, drill\-down, chart linkage, as well as intelligent analysis operations like attribution analysis, helping with data\-driven decision\-making and business growth.

<span id="_2-界面概览"></span>
# Interface overview

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9faae6724edf4afe9798cb9ae196d40e~tplv-goo7wpa0wc-image.image) </span>

As shown in the figure above, the visual query editing interface provides users with simple operation functions. The interface sections are introduced as follows:


1. Field list area: Displays the list of fields in the dataset used by the current visual query. The field list includes dataset fields and personal fields. Users can switch datasets in this area.

2. Chart and analysis configuration area:

* Chart configuration area: Provides configuration functions for each chart, such as color settings, X\-axis settings, Y\-axis settings, and more.

* Analysis configuration area: Provides analysis functions such as sorting, Top N, total, percentage, comparison, year\-over\-year, month\-over\-month, reference lines, and table calculations.

3. Field configuration area: Field types include dimensions and metrics. Dragging a field into this area allows further configuration for a specific field to complete the query.

4. Filter configuration area: Provides filtering capabilities for dimension and metric fields.

5. Chart display area: Displays the chart style according to the various query conditions configured by the user, providing a what\-you\-see\-is\-what\-you\-get effect.

6. Overall configuration area (top toolbar): In this top toolbar area, users can undo or redo operation steps, and options are provided for viewing query history, downloading, monitoring and alerts, as well as query configuration. The following provides instructions for the specific operations in the overall configuration area:

   
   |Names of operation items in the overall configuration area |Description |
   |---|---|
   |Undo |Return to the previous operation and cancel the most recent configuration change. |
   |Redo |Restore the undone operation, suitable for restoring after an incorrect undo. |
   |Reset |Restore the current query or configuration to its initial state and clear all temporary changes. |
   |Query history |Click the query history button to view the historical query records of the current dataset, making it easy to trace or reuse previous queries. |
   |Download |Click Download to open the dropdown menu, then select Download Data, Download Image, or Configure Download. After configuring the download as needed, click the Download button to download the relevant content. |
   |Monitor |Click the monitoring chart to create a new monitor or open the monitor list.<br><br>Caution: After setting Pivot Table \- Tree View to incremental fetching, monitoring is not supported; existing monitors will not be pushed. |
   |Query configuration |Click the Query Configuration button to configure the query in detail. Select whether to enable caching. If enabled, select the cache validity period; use the dropdown to select cluster query parameters. After completing the configuration, click the Apply button to finish the configuration. |
   |Rename |Change the name of the current chart. |
   |Chart list |Click the Chart List button to navigate to the Project Center's Chart Management and view the chart list. |
   |Save as |Save the current configuration as a new copy. |
   |Save |Save the current configuration or changes to the system, overwriting the previous version. |
   


<span id="_3-快速入门"></span>
# Quick start

<span id="_3-1-设置维度、指标条件"></span>
## **Set dimension and metric conditions**

For example, select province and year\-month as dimensions, and select GMV as the metric. You can drag fields from the field list on the left to the data panel to select them, or click the desired field so that it appears in the dimension or metric row of the data panel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f00201600c804f2b829fa0f3833a1bc8~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-选择图表类型"></span>
## **Select chart type**

To use more diverse chart types, such as a bar chart, click the bar chart icon in the chart panel to select a bar chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6b3de526bec482f8109f320389d4126~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-设置排序"></span>
## **Set sorting**

To sort, click Sort in the analysis panel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa4eff1d04c049e3a8540a941f5de080~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-保存为图表"></span>
## **Save as chart**

Click Save on the toolbar to save as a chart. If a dashboard has already been created, you can directly select the saved dashboard to quickly add the chart to the dashboard. If you have not created a dashboard or do not intend to display it on a dashboard, you do not need to select anything. Later, you can find this chart in [Chart Management](https://docs.byteplus.com/docs/DataWind/Chart_Management).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9496a5d49cf44bff8841a2e03dc68900~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-名词解释"></span>
# Glossary

<span id="_4-1-字段"></span>
## 4.1 Field

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a33235c36f0940248aab7070af329eae~tplv-goo7wpa0wc-image.image) </span>

In the field list area, you can view and use the fields of the current dataset. The visual query provides five field types: string, integer, float, date, and datetime. For detailed usage, see [Overview of Field Configuration](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration)


|Field type |Example value |
|---|---|
|String |hello |
|Integer |15 |
|Float |3.14 |
|Date |2020\-01\-04 |
|DateTime |2020\-01\-04 14:00:00 |


<span id="_4-2-维度和指标"></span>
## 4.2 Dimensions and metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c7703b45afd418b8622f9a8923c9290~tplv-goo7wpa0wc-image.image) </span>

Fields have two roles: dimension and metric. A dimension divides the data for analysis and determines the perspective from which to view the data. It is a non\-aggregated field, such as date or author UID. A metric measures data using different aggregation methods. In most cases, it is a number, such as the number of submissions by an author. For example, to view the number of students under each course category, set "course category" as the dimension and "number of students" (that is, the sum of students) as the metric.

<span id="_4-3-维度和指标在不同业务场景下的应用"></span>
## 4.3 **Application of dimensions and metrics in different business scenarios**

A field may serve as a dimension or a metric in different scenarios. Detail table example:


* When an author submits once, one record is generated.

* Filtered 2,230 rows of data from January 6, 2020 to January 8, 2020.



|Date |Author UID |Number of submissions |…… |
|---|---|---|---|
|2020\-01\-08 |71539701417 |1 | |
|2020\-01\-08 |71539701417 |1 | |
|2020\-01\-07 |71539701417 |1 | |
| |…… | | |
|2020\-01\-08 |9744333079 |1 | |
|2020\-01\-07 |9744333079 |1 | |
| |…… | | |
|2020\-01\-08 |8779307635 |1 | |
|2020\-01\-07 |8779307635 |1 | |


**Scenario 1 Number of submissions per day** View the total number of submissions per day by date


* Dimension: Date

* Metric: Number of submissions, aggregation method is sum



|Date |Number of submissions |
|---|---|
|2020\-01\-08 |780 |
|2020\-01\-07 |700 |
|2020\-01\-06 |750 |


**Scenario 2 Number of submissions per author per day** View the total number of submissions by different authors per day by date and author


* Dimension: Date, author UID

* Metric: Number of submissions, aggregation method is sum



|Date |Author UID |Number of submissions |
|---|---|---|
|2020\-01\-08 |71539701417 |280 |
|2020\-01\-08 |9744333079 |400 |
|2020\-01\-08 |8779307635 |100 |
|2020\-01\-07 |71539701417 |200 |
|2020\-01\-07 |9744333079 |420 |
|2020\-01\-07 |8779307635 |80 |
|2020\-01\-06 |71539701417 |220 |
|2020\-01\-06 |9744333079 |420 |
|2020\-01\-06 |8779307635 |110 |


**Scenario 3 Number of submitting authors** View how many authors submitted between January 6 and January 8, 2020


* Metric: Author UID, aggregation method is distinct count



|Number of submitting authors |
|---|
|3 |


<span id="_4-4-指标的聚合"></span>
## 4.4 Aggregation of metrics

The product provides multiple aggregation methods. For details, see [2.1 Set aggregation method](https://docs.byteplus.com/docs/DataWind/Metric_Field_Configuration#_2-1-%E8%AE%BE%E7%BD%AE%E8%81%9A%E5%90%88%E6%96%B9%E5%BC%8F). Below are the values obtained using different aggregation methods for a detail table demo (containing 7 rows of data).


|Date |Number of submissions |
|---|---|
|2020\-01\-08 |10 |
|2020\-01\-08 |10 |
|2020\-01\-08 |20 |
|2020\-01\-08 |20 |
|2020\-01\-08 |30 |
|2020\-01\-08 |30 |
|2020\-01\-08 |40 |


Results returned by different aggregation methods:


|Date |(Sum) Number of submissions |(Average) Number of submissions |(Count) Number of submissions |(Distinct count) Number of submissions |(Maximum) Number of submissions |(Minimum) Number of submissions |
|---|---|---|---|---|---|---|
|2020\-01\-08 |160 |22.8571 |7 |4 |40 |10 |


<span id="_4-5-查询与自动查询"></span>
## 4.5 Query and auto query


* **For extracted datasets, auto query is enabled by default**

* For direct connection datasets, auto query is disabled by default

> For differences, see: [Connection methods](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview#0b15f366).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42b76b62c1954d09b2615c4965b20ec9~tplv-goo7wpa0wc-image.image) </span>

Auto query can be enabled at the top of the chart display area. If auto query is enabled, every time you change the query conditions or chart configuration, the visualization chart will refresh. If auto query is not enabled, the chart will be grayed out after each change, and you need to click the "Query" button to re\-initiate the query. When the amount of query data is large, to avoid resource waste and waiting for each minor modification, it is recommended to disable auto query.
