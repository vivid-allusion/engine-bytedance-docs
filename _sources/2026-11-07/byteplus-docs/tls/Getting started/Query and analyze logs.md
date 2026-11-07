---
title: "Query and analyze logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/getting_started_query_and_analyze_logs"
---

Torch Log Service (TLS) offers log query and analysis features, allowing you to filter and search log data through query and analysis statements. The query and analysis results can be displayed in charts.

<span id="注意事项"></span>
## Precautions


* In TLS, the storage period of log data is determined by **Log storage period** set for the corresponding topic. Expired and deleted log data cannot be queried or analyzed.

* Only the log data collected after the statistics feature is enabled can be included in statistical analysis.


<span id="前提条件"></span>
## Before you begin


* Create a project and a topic.

* Collect log data through LogCollector or other methods.

* Configure indexes correctly, with the statistics feature enabled for the fields involved in analysis. For more information, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Common functions** \> **Query and analysis**.

3. In the Project/topic list, select a project and a topic.

4. Set the time range.

   The default time range is 5 minutes. You can change the time range as needed. When the specified time range exceeds the time\-to\-live (TTL) of log data, the expired and deleted data cannot be queried.

5. Type the query and analysis statement in the input box, then click **Search**.

   The statement consists of a query statement and an SQL analysis statement, separated by a pipe symbol ( | ). You can perform statistical analysis based on the query results. For more information, refer to [Analysis overview](https://docs.byteplus.com/docs/tls/Analysis-overview).

6. On the **Chart analysis** tab, view the analysis results.

   By default, the analysis results are displayed in a table. You can choose a chart and configure the chart settings accordingly. For more information, refer to [Chart overview](https://docs.byteplus.com/docs/tls/chart_overview).

   In the **Query results** area, the basic information on log analysis is displayed, including the total volume of logs and whether the search results are precise. For more information, refer to [View analysis data](https://docs.byteplus.com/docs/tls/Analyze-logs-2#b06c0da2).
