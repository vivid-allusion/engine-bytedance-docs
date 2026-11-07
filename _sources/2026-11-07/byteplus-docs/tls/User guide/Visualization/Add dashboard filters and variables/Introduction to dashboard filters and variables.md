---
title: "Introduction to dashboard filters and variables"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Adding_filters_to_a_dashboard"
---

Dashboard filters and variables both support additional filtering of data in each chart, making it easier to quickly view key field statistics and analysis data. This document introduces the dashboard filters or variables in Log Service.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Concepts

The Log Service dashboard displays statistical data of various charts within the specified time range by default.


* Data range: depends on the chart’s time range and the query and analysis statement.

* Chart linkage: filter chart data by creating filters or custom variables to specify field values, allowing you to view statistical analysis data of key fields.


For example, set multiple filters for access log–related dashboards to support filtering and screening by fields such as access source, client IP, and HTTP code, enabling fast viewing of relevant data analysis results for different access sources and client IPs.

<span id="1bd7c867"></span>
## Filter and variable types

The specific description of filters and variables is as follows:


|Type |Description |
|---|---|
|Filter |Filter by the log’s field names and field values.<br><br>After adding a filter to the dashboard and selecting the field value, the log service adds the specified key\-value pair as an additional retrieval condition before the query and analysis statement. The additional condition connects to the original query with an AND or NOT logic relation.<br><br><br>* Format of the query and analysis statement after using a filter:<br><br>   `[Key:Value] AND/NOT [search query] \| [sql query]`.<br><br>* Example:<br><br>   `code:500 AND ip:192.168.1.2` means searching logs containing the key\-value pair `code: 500` for logs where the `ip` field equals `192.168.1.2`. |
|Custom variables |Filter by specifying variable name and variable value.<br><br>After adding a variable, the variable in the corresponding query and analysis statement of the chart will be replaced with your selected variable value, affecting all charts on the dashboard that have this variable set.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you use variables to filter chart data, you must add variable placeholders in the query and analysis statements when adding charts.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The variable syntax is: <code>${{variableName\|defaultValue}}</code>,</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Example: <code>id: ${{id\|123}} \| SELECT __time__ - __time__ %60 AS time, COUNT(*) AS PV GROUP BY time</code>.</div><br> |
|Data source variables |Filter by specifying variable names and log topic scope.<br><br>After adding a data source variable, simply switch the variable value; the specified statistical chart will automatically update the query and analysis results based on the log topic you switched to. You can flexibly switch the data source of statistical charts. |
|Preset variables |The log service provides preset variables like `__from` and `__to` that can be used directly in dashboards’ query and analysis statements, statistical chart titles, and text boxes without creating them. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The total number of filters, variables, and charts in each dashboard must not exceed 50.
