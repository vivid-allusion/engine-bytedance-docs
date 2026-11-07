---
title: "Viewing ArkClaw log analysis"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_log_analysis"
---

The platform provides log search and log analysis capabilities for ArkClaw instances, enabling you to query ArkClaw logs, quickly identify the root cause of failures, and monitor system performance. This topic describes how to perform log search and log analysis.

<span id="smlvsdXn"></span>
## Prerequisites


* The administrator has completed basic settings (such as enterprise system permissions and callback configuration) and has activated ArkClaw Enterprise. For details, see [Getting started with space activation](https://docs.byteplus.com/en/docs/ArkClaw/Getting_Started).

* Enterprise employees have provisioned ArkClaw instances and started conversations with ArkClaw to process tasks. For details, see the [ArkClaw guide for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employee_use_of_ArkClaw_new_version).


<span id="tB2agAmr"></span>
## Retrieve logs

Log retrieval can only be used to filter and query log data. When data statistics and analysis are not required, you only need to enter the retrieval condition in the text box and specify the log time range and topic. Then, you can query logs that match the specified condition.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **O&M \> Observability**.

3. Select the data source for the observability dashboard and data analytics. The Claw instance page displays the observability dashboards and data analysis related to employee Claw instances. The enterprise service agent page displays the observability dashboards and data analysis related to enterprise service agents.

4. Click the **Log analysis** tab, and enter the query statement as needed. For example, use `service = "ci-yej5dzoxxxxxc4gutwj"` to retrieve log data related to the `ci-yej5dzoxxxxxc4gutwj` instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For detailed descriptions of retrieval syntax, see <a href="https://docs.byteplus.com/en/docs/tls/Log-query-syntax-2">Retrieval syntax</a>. For more detailed descriptions of log retrieval, see <a href="https://docs.byteplus.com/en/docs/tls/Search_logs">Retrieving logs</a>.   </div>
   

5. Enter the retrieval condition and click **Search**.

   The detailed description of retrieval conditions is as follows:

   
   |Item |Description |
   |---|---|
   |Search precision |Set the time precision for log retrieval and analysis.<br><br><br>* Millisecond\-level retrieval precision (default).<br><br>* Nanosecond retrieval precision: With the high\-precision timestamp feature enabled, logs can be searched at nanosecond precision. |
   |Search and analysis time |Set the time range for log retrieval and analysis. Data outside the specified query time range will not be retrieved.<br><br><br>* Last 5 minutes (default).<br><br>* Supports quick selection of time periods, custom time range, and hour\-aligned time. |
   |Automatic refresh query |Specify whether to automatically refresh the query results at specified intervals.<br><br><br>* Disable (default).<br><br>* Enable: The query result can be automatically refreshed at a specified interval, including 15 seconds, 1 minute, 5 minutes, 10 minutes, 30 minutes, and 60 minutes. |
   

6. Click the **Raw logs** tab to view the filtered logs.

   You can perform the following basic operations on the "Raw logs" tab.

   
   |Serial number |Item |Description |
   |---|---|---|
   |1 |Display field |Specify the fields to be displayed. By default, all fields are displayed. You can also select specific fields from "Index fields" and "Other fields" to show them only. |
   |2 |Display format |The format in which log data is displayed. The original and table formats are supported. The table format is used by default. |
   |3 |Sort by time |Sort the filtered logs data by time. |
   |4 |Advanced configuration |The advanced settings related to data filtering and display format. You can specify configurations as needed. For example, filtering predefined fields, filtering empty fields, using a paginator to navigate pages, sorting tables, and forcibly parsing JSON fields. |
   |5 |Log interpretation |Quick access to AI\-powered log analysis. Enter analysis requirements, and the system will retrieve the log topic of the current page, perform different summarizations based on raw logs and chart analysis, and quickly analyze the overall status of log data for you. |
   |6 |Download log |Download raw log data or retrieval and analysis results to your local computer for data viewing or further analysis. |
   |7 |Global view |View log data in full\-screen mode. |
   


<span id="fPgXRiAg"></span>
## Analyze logs

Log analysis provides real\-time data analysis capabilities based on log retrieval. It supports real\-time retrieval and analysis of massive log data, and SQL analysis and computing based on log retrieval results. The analysis results are displayed in charts.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **O&M \> Observability**.

3. Click the **Log analysis** tab and enter the retrieval and analysis statement as needed. For example, `* | SELECT COUNT(*) AS total, service GROUP BY service` indicates that all data is grouped by the `service` field, and then the number of logs in each group is counted.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For detailed descriptions of analysis syntax, see <a href="https://docs.byteplus.com/en/docs/tls/Analyzing_Grammar">Analysis syntax</a>. For more detailed descriptions of log analysis, see <a href="https://docs.byteplus.com/en/docs/tls/Analyze_logs">Analyzing logs</a>.   </div>
   

4. Enter the retrieval condition and click **Search**.

   The detailed description of retrieval conditions is as follows:

   
   |Item |Description |
   |---|---|
   |Search precision |Set the time precision for log retrieval and analysis.<br><br><br>* Millisecond\-level retrieval precision (default).<br><br>* Nanosecond retrieval precision: With the high\-precision timestamp feature enabled, logs can be searched at nanosecond precision. |
   |Search and analysis time |Set the time range for search and analysis logs. Data outside the specified query time range will not be retrieved.<br><br><br>* Last 5 minutes (default).<br><br>* Supports quick selection of time periods, custom time range, and hour\-aligned time. |
   |Automatic refresh query |Specify whether to automatically refresh the query results at specified intervals.<br><br><br>* Disable (default).<br><br>* Enable: The query result can be automatically refreshed at a specified interval, including 15 seconds, 1 minute, 5 minutes, 10 minutes, 30 minutes, and 60 minutes. |
   

5. Click the **Chart analysis** tab. Specify chart parameters in the "Chart analysis settings" section on the right as needed, and then you can view the log analysis chart.
