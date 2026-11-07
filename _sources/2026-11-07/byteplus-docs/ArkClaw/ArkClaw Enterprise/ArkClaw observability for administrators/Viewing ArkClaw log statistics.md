---
title: "Viewing ArkClaw log statistics"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_log_statistics"
---

The platform provides a log statistics dashboard for ArkClaw instances to help you monitor their health globally. This topic describes how to access and use the log statistics dashboard.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The dashboard metrics and data filters for employee Claw instances and enterprise service agents differ. Refer to the console for the actual information.</div>


<span id="BnMd0fGG"></span>
## Prerequisites


* The administrator has completed basic settings (such as enterprise system permissions and callback configuration) and has activated ArkClaw Enterprise. For details, see [Getting started with space activation](https://docs.byteplus.com/en/docs/ArkClaw/Getting_Started).

* Enterprise employees have provisioned ArkClaw instances and started conversations with ArkClaw to process tasks. For details, see the [ArkClaw guide for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employee_use_of_ArkClaw_new_version).


<span id="HNcdaxJl"></span>
## Viewing the dashboard


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **O&M \> Observability**.

3. Select the data source for the observability dashboard and data analytics. The Claw instance page displays the observability dashboard and data analysis related to employee Claw instances. The enterprise service agent page displays the observability dashboard and data analysis related to enterprise service agents.

4. Click the **Log statistics** tab to access the ArkClaw log statistics dashboard.

   
   |Metric |Description |
   |---|---|
   |Total logs |The total number of logs collected within the specified time range. It reflects the scale of log generation and collection integrity and serves as the fundamental metric for log analysis. |
   |Error logs |The number of error logs collected within the specified time range. This measures the frequency and scale of system errors and directly reflects system stability and the extent of business impact. It can be used to compute the proportion of error logs for quantifying system health. |
   |Top 5 ArkClaw instances by log count<br><br>&nbsp;<br><br>> Logs Top 5 Enterprise Services Agents<br><br><br> |The top 5 ArkClaw instances ranked by log count within the specified time range. It is used to identify instances with abnormal log count or high load. It can facilitate troubleshooting by quickly locating I/O, CPU, and storage resource bottlenecks caused by excessive logs, ensuring stable and efficient operation of ArkClaw. |
   |Top 5 ArkClaw instances ranked by error log count<br><br>&nbsp;<br><br>> Number of Error Logs Enterprise Services Agent Top 5<br><br><br> |The top 5 ArkClaw instances ranked by error log count within the specified time range. This metric focuses on ArkClaw instances with the highest error\-level log volume to locate core faulty nodes. It can be used to quickly identify the most severely problematic instances, for which you may need to prioritize troubleshooting and remediation to minimize impact. |
   |Log distribution by level |The distribution trend of logs at Error, Warn, Info, and Debug levels within the specified time range. This chart presents fluctuations in the proportion of logs across different severity levels over time and reflects system health and the evolution of system operating status. It helps identify abrupt changes in log level distribution, enabling timely alerts for potential faults or performance degradation. This information can also be used to analyze system status changes and monitor system stability trends, supporting architecture iteration, operations and maintenance optimization, and capacity planning. |
   


<span id="9s0BseDE"></span>
## What to do next

The following operations are available on the monitoring dashboard:


|Serial number |Actions |Description |
|---|---|---|
|1 |Time range |The time range for data filtering. You can specify a relative or absolute time range. |
|2 |Refresh frequency |Data refresh frequency. Available refresh methods include manual refresh or auto\-refresh at the specified intervals. |
|3 |Chart actions |The operations that are supported by a chart, such as Enlarge, Compare, and Download as CSV.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported operations vary based on different charts. The displayed operations apply.</div><br><br><br><br>* Enlarge: Switch to the full\-screen view.<br><br>* Compare: Only trend charts support this action. Compares data between two time periods to provide trend insights.<br><br>* Download as CSV: Export the raw or formatted data to a CSV file for statistics or analysis. |
|4 |Chart data filtering |Click a specific item in the legend at the bottom of a chart to filter data sources in the chart.<br><br><br>* Click a data source to show or hide the corresponding data in the chart.<br><br>* On the right of the specified data source, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_121d43c534f90353b5ddce79208da3c6.png) </span> icon to display only the graph element for that data source and hide the graph elements for other data sources. |
