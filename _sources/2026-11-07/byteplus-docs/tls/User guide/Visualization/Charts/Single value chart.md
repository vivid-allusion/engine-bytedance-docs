---
title: "Single value chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Single_value_chart"
---

Torch Log Service (TLS) supports single\-value charts for displaying query and analysis results. This topic describes how to configure a single\-value chart.

<span id=".5Zu-6KGo6K-05piO"></span>
## Chart description

A single\-value chart is a rectangular box displaying query and analysis results, and a result typically is a single numeric value. This type of chart is suitable for displaying specific key information collected at a specific moment or over a specific period.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart, read <a href="https://docs.byteplus.com/docs/tls/chart_overview#.5rOo5oSP5LqL6aG5">Precautions</a>.</div>


<span id=".6YCa55So6YWN572u"></span>
## Common settings

Configure the global settings that apply to the entire chart. The basic settings of a single\-value chart are as follows:


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Field configuration |Field |Select the field whose value you want to display in the single\-value chart.<br><br><br>* We recommend that you select a field of a numeric data type.<br><br>* If the selected field contains multiple numeric values, the first value is displayed in the single\-value chart. |
|Standard configuration |Unit |The unit of the numeric value that you want to display in the single\-value chart. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="9bc28b34"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, set a drill\-down event on the **PV** field in a line chart. After you set Open topic drill\-down event on the PV field, click the PV field on the single\-value chart, then select **Open topic** drill\-down event. You are then navigated to the topic that is specified in the drill\-down event configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/827cc065ac8b41e5a202b97ce1d7dde8~tplv-goo7wpa0wc-image.image) </span>

<span id="7c60e227"></span>
## Example

Use a single\-value chart to display the total PVs of the last week.


* Sample query statement:

   ```SQL
   * | SELECT COUNT(*) as PV
   ```
   

* Chart configurations:

   * **Field source column**: The `PV` field is specified as the field to display. The single\-value chart displays the value of the PV field. If the PV field has multiple rows of values, the value in the first row is displayed.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0861d79d2f6a489bbd11bb67eabe8cd0~tplv-goo7wpa0wc-image.image) </span>
