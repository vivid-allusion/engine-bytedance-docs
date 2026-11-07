---
title: "Custom dashboard"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Custom_dashboard"
---

The custom dashboard allows users to flexibly configure metrics and chart types.

<span id="AQMmgaLT"></span>
## Create dashboard

Currently, creating a custom dashboard is prohibited. Use the new [Custom Dashboard](https://console.byteplus.com/observe/dashboard/dashboard) for analysis and insights.


* The new custom dashboard now supports workspace compatibility and provides a richer set of dashboard charts and data sources. For more details, see: [Custom Dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/Custom_dashboard).

* Historical dashboards on the current page can still be viewed and edited.


<span id=".6YWN572u5Zu-6KGo"></span>
## Dashboard management


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation bar, select **Custom Dashboard**.

3. In the dashboard list, click the target dashboard name to view or edit the dashboard. The following management actions are supported for existing dashboards:



|Actions |Descriptions |
|---|---|
|Edit name |Click the edit button to the right of the dashboard name to customize it. |
|Add container |Click the **Add Container** button in the upper right corner of the dashboard to add a container as needed and group a set of charts together. |
|Modify container name |The default name for an added container is "Unnamed Container". Click the edit button to the right of the container name to customize the name. |
|Add component |Click the **Add component** button in the upper right corner of the dashboard to create a new chart and configure parameters as needed. When finished, click **Save**. |


<span id="IlMRJk3r"></span>
## Configure charts

The custom dashboard supports adding three types of charts: trend charts, numeric cards, and tables.

<span id="6UJanuB0"></span>
### Trend chart

The parameter description for trend charts is as follows:


|**Parameter** |**Descriptions** |
|---|---|
|Chart name |Customize the chart name to identify the current chart. |
|Decimal places |Decimal places for numerical display. The default is 2 decimal places; you can configure to display none, 1, 2, 3, or 4 decimal places. |
|Y\-axis |Maximum and minimum values of the Y\-axis, used to limit the display range of the Y\-axis in the trend chart. |
|Legend |Whether to display the legend below the trend chart. Enabled by default, indicating that the legend is displayed. The legend name defaults to the metric name.<br><br>The legend fields display the maximum, minimum, average, and current metric values by default. |
|Metric |Support selecting the metrics to query; multiple metrics can be added. Support metrics related to hosts, processes, containers, services, and custom metrics. |
|Filter |Filter dimension. |
|Statistical method for time interval |The default is Group by. Custom metrics support other statistical methods.<br><br><br>* Group by.<br><br>* AVG: SUM(metric values for each time granularity) / number of periods<br><br>* SUM: SUM(metric values for each time granularity)<br><br>* MAX: Maximum value within the selected time range<br><br>* MIN: Minimum value within the selected time range |
|Time granularity statistical method |* count: Counted based on the time granularity, used to calculate the request count, with a unit of 1.<br><br>* rate: Count/duration, used to calculate the request count per second (QPS), with a unit of 1/s. |
|Name metrics |Supports naming legends. |
|Quick filter |To link with the dashboard's quick filter criteria, select a preconfigured quick filter. |
|Add arithmetic operation |To perform arithmetic operations on existing metrics, for example, to sum the error count of all exception types, use the arithmetic operation feature. |
|Add marker |Supports adding markers. You can add marker lines or marker areas to the trend chart and name them. Multiple markers are supported. |


<span id="nLNkgd3I"></span>
### Numeric card

The numeric card displays a statistical value. The parameter description for numeric cards is as follows:


|**Parameter** |**Descriptions** |
|---|---|
|Chart name |Customize the chart name to identify the current chart. |
|Decimal places |The number of decimal places displayed for values. The default is 2 decimal places. Configuration supports none, 1, 2, 3, or 4 decimal places. |
|Metric |Support selecting the metrics to query. Supports configuration of metrics for hosts, processes, containers, services, and custom metrics.<br><br>When multiple raw metrics are added, only the most recently added metric is displayed. |
|Selected function statistical method |The statistical methods and descriptions are as follows:<br><br><br>* diff: Calculates the difference from the metric of the previous minute<br><br>* per_second_rate: Calculates the per\-second rate of change of the metric value<br><br>* per_minute_rate: Calculates the per\-minute rate of change of the metric value<br><br>* per_second: Metric value/drawing interval, with a unit of /s |
|Statistics for the selected time interval |The statistical methods and descriptions for time segments are as follows:<br><br><br>* AVG: SUM(metric values for each time granularity) / number of periods<br><br>* MAX: Maximum value within the selected time range<br><br>* MIN: Minimum value within the selected time range<br><br>* SUM: SUM(metric values for each time granularity)<br><br>* LAST: The last metric value within the selected time period<br><br>* NUMS: Items with metric values |
|Unit |Support configuring the unit of the final displayed value. |
|Quick filter |To link with the dashboard's quick filter criteria, select a preconfigured quick filter. |
|Add the four basic arithmetic operations. |When arithmetic operations are added to metrics, the final metric calculated through these operations is displayed. |


<span id="TwqT5ExP"></span>
### Table

The parameter description for tables is as follows:


|**Parameter** |**Descriptions** |
|---|---|
|Chart name |Customize the chart name to identify the current chart. |
|Decimal places |Decimal places for numerical display. The default is 2 decimal places; you can configure to display none, 1, 2, 3, or 4 decimal places. |
|Sorting |When there are multiple metrics, select which metric to sort by and configure the table to display the Top values according to the sorting method.<br><br><br>* Sorting methods support ascending and descending order.<br><br>* Top values include Top 10, 20, 30, 40, 50, and 100. |
|Metric |Supports selecting the metrics to query, and allows adding multiple metrics. Supports configuring metrics for hosts, processes, containers, services, and custom metrics. |
|Selected function statistical method |The statistical methods and descriptions are as follows:<br><br><br>* diff: Calculates the difference between the metric and the previous minute's metric<br><br>* per_second_rate: Calculates the per\-second rate of change of the metric value<br><br>* per_minute_rate: Calculates the per\-minute rate of change of the metric value<br><br>* per_second: Metric value divided by the plotting interval, with the unit /s |
|Statistics for the selected time interval |The statistical methods and descriptions for the time interval are as follows:<br><br><br>* AVG: SUM (the metric value for each time granularity) / number of periods<br><br>* MAX: The maximum value within the selected time range<br><br>* MIN: The minimum value within the selected time range<br><br>* SUM: SUM (the metric value for each time granularity)<br><br>* LAST: The last metric value within the selected time interval<br><br>* NUMS: Items with metric values |
|Column Name |Supports custom table column names, with column names automatically including the selected statistical value Type. |
|Unit |Support configuring the unit of table column data. For example, the unit for FPS can be configured as s (seconds). |
|Quick filter |To link with the dashboard's quick filter criteria, select a preconfigured quick filter. |
|Add arithmetic operation |Supports adding multiple metrics and performing arithmetic operations on multiple raw metrics. |
