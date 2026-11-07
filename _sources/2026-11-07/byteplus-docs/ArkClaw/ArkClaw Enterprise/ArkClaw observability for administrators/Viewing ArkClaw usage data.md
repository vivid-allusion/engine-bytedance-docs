---
title: "Viewing ArkClaw usage data"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_usage_data"
---

The platform provides a usage analysis dashboard that enables you to monitor resource consumption of all ArkClaw instances. This topic describes how to view the usage analysis dashboard.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The dashboard metrics and data filters for employee Claw instances and enterprise service agents differ. Refer to the console for the actual display.</div>


<span id="pZZp2DWj"></span>
## Background information

ArkClaw usage analysis supports the following data sources that you can select from as needed:


* **ArkClaw** ** Gateway**: The default token consumption data source for the new usage analysis dashboard. It directly retrieves token usage data from ArkClaw Gateway, maintaining consistency with ArkClaw's data throttling metrics for higher statistical accuracy.

* **Self\-built Gateway**: A custom token consumption data source for the new usage analysis. You can report usage data of self\-managed gateways to Server\-side Monitoring to obtain token usage metrics and accurate actual business consumption and access trends for intuitive resource monitoring. For details about integrating usage data of self\-managed gateways, see [Reporting usage data of self-managed gateways](https://docs.byteplus.com/en/docs/ArkClaw/Reporting_self-managed_gateway_usage_data).

* **Observability plugin**: The token consumption data source in the legacy usage analysis dashboard. Token usage data obtained through the observability plugins is statistically coarse\-grained and for reference only.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To improve the statistical accuracy of token consumption data, the data collection method based on observability plugins will be <strong>officially retired on August 31, 2026</strong>. We recommend using ArkClaw Gateway or Self\-Built Gateway data for usage analysis.   </div>
   

<span id="mK2uK9Uw"></span>
## Prerequisites


* The administrator has completed basic settings (such as enterprise system permissions and callback configuration) and has activated ArkClaw Enterprise. For details, see [Getting started with space activation](https://docs.byteplus.com/en/docs/ArkClaw/Getting_Started).

* Enterprise employees have provisioned ArkClaw instances and started conversations with ArkClaw to process tasks. For details, see the [ArkClaw guide for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employee_use_of_ArkClaw_new_version).


<span id="1BqIUF3a"></span>
## Viewing the dashboard


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **O&M \> Observability**.

3. Select the data source for the observability dashboard and data analytics. The Claw instance page displays the observability dashboards and data analysis related to employee Claw instances. The enterprise service agent page displays the observability dashboards and data analysis related to enterprise service agents.

4. Click the **Usage analysis** tab to access the ArkClaw usage analysis dashboard.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Metrics in usage analysis are for reference only. For actual charges, refer to the billing information of the corresponding model service. The new statistical scope of token consumption is as follows:</div>



* <div data-tips="true" data-tips-type="default">ArkClaw gateway: Request data flowing through the gateway is automatically included in statistics and displayed.</div>


* <div data-tips="true" data-tips-type="default">Third\-party self\-managed gateway: You need to integrate the instrumentation solution provided by ArkClaw and complete metric reporting before you can view data.</div>


* <div data-tips="true" data-tips-type="default">Large Model Direct Endpoint: Data from this source is not currently included in statistics or displayed. Go to the model service provider's console to view actual consumption.</div>




|Category |Metric |Description |
|---|---|---|
|Basic data |Active users |The number of users with either requests or token usage within the specified time range. |
||Active instances |The number of ArkClaw instances with either requests or token usage within the specified time range. |
||Input token |The total number of input tokens within the specified time range. This metric measures the volume of input text and is a core input item for model calculation and billing. |
||Output token |The total number of output tokens within the specified time range. It measures the length of content generated by the model, and is a core output item for model calculation and billing. |
||Cached token |The number of tokens read from the cache within the specified time range. This metric measures cache reuse efficiency and reflects resource savings brought by cache hits. |
||Cache hit ratio |The cache hit ratio for input tokens within the specified time range. It is used to evaluate the effectiveness of the cache strategy. The calculation formula is as follows: Cache hit ratio = Cached tokens / (Input tokens + Cache tokens). |
|Usage ranking |Top 50 token usage by user |The top 50 users ranked by total tokens consumed within the specified time range. It is used to quickly locate users with the highest token consumption and identify cost and performance hotspots. Total tokens consumed = Input tokens + Output tokens |
||Top 50 token usage by instance<br><br>&nbsp;<br><br>> Token Usage Top 50 By Enterprise Services Agents<br><br><br> |The top 50 ArkClaw instances ranked by total tokens consumed within the specified time range. It is used to quickly locate instances with the highest token consumption and identify cost and performance hotspots. Total tokens consumed = Input tokens + Output tokens |
||Top 50 skills by access count |Top 50 skill files ranked by total read\-and\-load count within the specified time range. It provides an intuitive view of access popularity at the skills layer and serves as a core quantitative metric for skill asset activity and business dependency. |
||Model call ranking |The ranking of model calls based on total token consumption. It visualizes the usage proportion of different models, which can be used to identify core dependencies and high\-cost models and provide quantitative data for cost control and model selection. Total tokens consumed = Input tokens + Output tokens |
|Usage trend |Token usage trends by model |The usage trend of total token calls for different models within the specified time range. It is used to identify high\-consumption models and the traffic distribution. It supports model cost accounting, selection optimization, routing scheduling, and quota planning, ensuring system stability and improving resource utilization efficiency. |
||Token usage trend by type |The usage trend of different types of tokens within the specified time range. It visualizes the trends of input/output/cached token consumption over time. These trends can be applied to scenarios including cost forecasting and business cycle analysis, and serve as the foundation for long\-term cost and performance analysis. |
|Usage details |User usage details<br><br>&nbsp;<br><br>> Enterprise Services Agent Usage Details |The total instance requests and token consumption at the user level within a specified timeframe. Key metrics include the username, department, Claw instance, request count, skill access count, input tokens, output tokens, cached tokens, and total tokens.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The Claw instances do not refer to the actual provisioned instances, but rather those that had data interaction within the specified time range.</div><br> |
||Instance usage details |The total instance requests and token consumption at the instance level within a specified timeframe. Key metrics include the Claw instance, username, owning department, request count, skill access count, input tokens, output tokens, cached tokens, and total tokens. |


<span id="wgRBiXMV"></span>
## More operations

The following operations are available on the monitoring dashboard:


|Serial number |Actions |Description |
|---|---|---|
|1 |Data source |The data source for usage analysis. Currently, supported sources include ArkClaw Gateway, Self\-Built Gateway, and Observability plugin. For details, see [Background information](https://docs.byteplus.com/en/docs/394/95097#pZZp2DWj).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To improve the statistical accuracy of token consumption data, the data collection method based on observability plugins will be <strong>officially retired on August 31, 2026</strong>. We recommend using ArkClaw Gateway or Self\-Built Gateway data for usage analysis.</div><br> |
|2 |Resource filter |Filter data by user, email, and instance. The default values of these fields are All. |
|3 |Time range |The time range for data filtering. You can specify a relative or absolute time range. |
|4 |Refresh frequency |Data refresh frequency. Available refresh methods include manual refresh or auto\-refresh at the specified intervals. |
|5 |Chart actions |The operations that are supported by a chart, such as Enlarge, Compare, and Download as CSV.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported operations vary based on different charts. The displayed operations apply.</div><br><br><br><br>* Enlarge: Switch to the full\-screen view.<br><br>* Compare: Only trend charts support this action. Compares data between two time periods to provide trend insights.<br><br>* Download as CSV: Export the raw or formatted data to a CSV file for statistics or analysis. |
|6 |Chart data filtering |Click a specific item in the legend at the bottom of a chart to filter data sources in the chart.<br><br><br>* Click a data source to show or hide the corresponding data in the chart.<br><br>* On the right of the specified data source, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_121d43c534f90353b5ddce79208da3c6.png) </span> icon to display only the graph element for that data source and hide the graph elements for other data sources. |
|7 |Quick redirection to instance details |Click the instance ID above the metering bar to quickly jump to the detail page of the current instance and view detailed information. |
|8 |Table data ranking |Click the sort icon next to a table column header to sort the data in ascending or descending order. |
