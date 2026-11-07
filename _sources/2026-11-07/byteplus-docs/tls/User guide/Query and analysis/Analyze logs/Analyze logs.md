---
title: "Analyze logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Analyze-logs-2"
---

After you collect log data, configure indexes correctly, and enable the statistics feature for fields, you can use query and analysis statements to query and analyze logs in the Torch Log Service (TLS) console. This topic describes how to analyze logs.

<span id="Precautions"></span>
## Precautions


* In TLS, the storage period of log data depends on the **Log storage period** setting of the project. Logs that are expired and deleted cannot be queried or analyzed.

* Only log data collected after the statistics feature is enabled can be included in statistical analysis.


<span id="6a6e1735"></span>
## Before you begin


* Create a project and a topic.

* Collect log data through LogCollector or other methods.

* Configure indexes correctly and enable the statistics feature for fields to be analyzed. For more information, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2).


<span id="acc28e13"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Common functions** \> **Query and analysis**.

3. Select a project and a topic.

4. Specify a time range.

   The default time range is 5 minutes. You can change the time range as needed. If the specified time range exceeds the retention period of logs, the expired and deleted data cannot be queried.

5. Type the query and analysis statement in the input box, then click **Search**.

   The statement consists of a query statement and an SQL analysis statement, separated by a pipe symbol ( | ), which indicates that statistical analysis is performed based on the query results. For more information, refer to [Analysis overview](https://docs.byteplus.com/docs/tls/Analysis-overview).

6. On the **Chart analysis** tab, view the analysis results.

   By default, the analysis results are displayed in a table. You can choose a chart and configure the chart settings accordingly.

   In the **Query results** area, the basic information on log analysis is displayed, including the total number of logs and whether the query results are precise.


<span id="48099bdd"></span>
## View analysis results

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to the following analysis results, TLS offers histograms and raw logs to display all details of logs that meet the query condition.</div>


<span id="b06c0da2"></span>
### View analysis data

In the **Query results** area, the basic information on the current query and analysis operation is displayed, including the total number of logs and the number of rows of results.


|Item |Description |
|---|---|
|Total logs |The total number of logs that meet the search condition. |
|Hit line |The number of rows that meet the query condition. |
|Resulting rows |The number of rows of results returned. If the value of **Resulting rows** is less than that of **Hit line**, we recommend that you use a LIMIT clause to get more data. |
|Limit |The limit on the number of results to return. The default and maximum values are 100 and 1000, respectively. In query and analysis statements, you can use the LIMIT clause to specify the maximum number of results to return. We recommend that you set a proper limit based on the number of matching rows. Otherwise, too much data reduces the speed and performance of the query and analysis, while too little data cannot give you a full picture of the results. |
|Duration |Displays the time taken for this query and analysis. |


<span id="dc8345eb"></span>
### View analysis charts

By default, the query and analysis results are displayed in tables. You can choose suitable chart types based on the SQL analysis statement type and analysis purpose to facilitate data analytics. TLS supports multiple types of charts including tables, column charts, and line charts. For more information, refer to [Chart overview](https://docs.byteplus.com/docs/tls/chart_overview).

<span id="044a7c1d"></span>
### Download logs

On the upper\-right corner of theRaw log or **Chart analysis** tab, click **Download log** to download raw logs or query and analysis results to your local device for further analysis.

After you click **Download log**, TLS creates a task of exporting the current query and analysis results and exports the data to a file. After the data is exported, you can view and download the corresponding file on the **Export history** page. For more information, refer to [Download logs](https://docs.byteplus.com/docs/tls/Download-logs-2).

<span id="98d14da8"></span>
### Save results to a dashboard

TLS allows you to save query and analysis results in the form of charts to an existing or new dashboard with one click. On the dashboard, you can view the real\-time query and analysis results for different topics and query and analysis statements. The dashboard displays the status and trend of key metrics for log data to help you build data analysis dashboards in operations and O&M scenarios. For more information, refer to [Add charts to a dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard).
