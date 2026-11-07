---
title: "Overview of query and analysis charts"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/chart_overview"
---

The log service provides log query and analysis functions. After you collect logs, the log service analyzes the collected data and displays the analysis results as charts. Currently, the log service supports various statistical charts such as tables. You can select the appropriate chart to view analysis results according to your business needs.

<span id=".5Zu-6KGo57G75Z6L"></span>
## Chart types

The log service supports the following types of statistical charts:


* [Table](https://docs.byteplus.com/docs/tls/Table)

* [Line chart](https://docs.byteplus.com/docs/tls/Line_chart)

* [Bar chart](https://docs.byteplus.com/docs/tls/Column_chart)

* [Pie chart](https://docs.byteplus.com/docs/tls/Pie_chart)

* [Flow chart](https://docs.byteplus.com/docs/tls/Flow_chart)

* [single value chart](https://docs.byteplus.com/docs/tls/Single_value_chart)

* [China map](https://docs.byteplus.com/docs/tls/China_map)

* [world map](https://docs.byteplus.com/docs/tls/World_map)

* [histogram](https://docs.byteplus.com/docs/tls/Histogram)

* [heatmap](https://docs.byteplus.com/docs/tls/Heat_map)

* [progress bar](https://docs.byteplus.com/docs/tls/Progress_bar)

* [treemap](https://docs.byteplus.com/docs/tls/Treemap)

* [meter chart](https://docs.byteplus.com/docs/tls/Gauge_chart)

* [statistical chart](https://docs.byteplus.com/docs/tls/Statistics_chart)

* [timeline](https://docs.byteplus.com/docs/tls/Timeline)

* [Radar chart](https://docs.byteplus.com/docs/tls/Radar_chart)

* [Scatter plot](https://docs.byteplus.com/docs/tls/scatter_chart)

* [Funnel chart](https://docs.byteplus.com/docs/tls/funnel_chart)

* [Text chart](https://docs.byteplus.com/docs/tls/markdown_chart)

* [Topology chart](https://docs.byteplus.com/docs/tls/Topology_chart)

* [Word cloud](https://docs.byteplus.com/docs/tls/Word-cloud)

* [Cross table](https://docs.byteplus.com/docs/tls/cross-table)

* [Sankey diagram](https://docs.byteplus.com/docs/tls/Sankey-diagram)


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before viewing analysis data in chart form, ensure that log data has been successfully collected, the index is configured, and analysis is enabled—that is, the **index status** in the index settings is **enabled**, and the **statistics** switch for the corresponding fields is turned on.

* The log service displays query and analysis results as statistical charts only after executing query and analysis statements. The types of statistical charts displayed relate to the analysis statements. Please refer to the documentation for each statistical chart and enter the correct query and analysis statements.

* The default limit is 100, meaning 100 rows of data are returned. You can use the `limit` function to customize the number of entries returned, up to 10,000 rows.


<span id=".5Zu-6KGo5bGe5oCn"></span>
## Chart properties

The log service supports a variety of statistical chart property configurations, with different configuration properties for each chart type. In addition to basic settings like title, pagination, and style, it also supports customized style configurations for specific query results or columns of data.


|Configuration category |Description |
|---|---|
|General settings |Globally configure specified types of statistical charts. This configuration applies to the entire chart scope. Currently supported general configurations include basic settings like titles, standard settings like custom units, style settings like alignment, and advanced settings like thresholds.<br><br>For example, select the chart type as **table**, and under **general settings** \> **style**, set the **alignment** to **center**. After this, all characters in the columns of the entire table are displayed centered. |
|Field configuration |Configure personalized styles for specific data. Field configuration applies only to specified data, such as styles for designated query and analysis results or specified result fields. The meanings of field configuration options are the same as those in general settings. Currently, only some chart types support field configuration.<br><br>For example, select the chart type as **table**, then select the field name in the **field configuration** area. You can set the **alignment** of this field to **center**. |
|Interactive events |Some statistical charts in log service support setting interactive events. After successfully configuring interactive events and saving the chart on the dashboard, clicking a specified field on the dashboard triggers the corresponding interaction.<br><br>For example, setting an interactive event in a table on the dashboard, assigning the event "open log topic" to the field UV. After saving, clicking any cell in the UV column on the dashboard table and selecting "open log topic" in the popup will redirect to the specified log topic search and analysis page. |


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

Q: Why can't query and analysis statements automatically generate statistical charts?

A: The log service cannot automatically determine your **X\-axis**, **Y\-axis**, **value**, and other chart analysis settings. If you run query and analysis multiple times on the same query page, the log service will retain the chart analysis settings from your last query by default. If these settings do not match the current query and analysis statement, the chart cannot be generated automatically. The page may display an error. Please reselect the **chart analysis settings** according to the current query and analysis statement.
