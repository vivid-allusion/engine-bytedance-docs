---
title: "Rectangle Tree chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Treemap"
---

Torch Log Service (TLS) supports rectangle tree charts for displaying query and analysis results. This topic describes how to create a rectangle tree chart.

<span id="ebca003a"></span>
## Chart description

In a rectangle tree chart, rectangles are used to display hierarchical data. The rectangles are arranged without gaps, and each rectangle represents a category of data. A larger rectangle represents a larger proportion of the categorical data. The sum of the values in all rectangles is the total value.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="9d7d2400"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Value |Select the field that specifies categories. |
||Classification field |Select the field that specifies the numeric values you want to view in the chart. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Rectangle Tree Style |Display value |Specify whether to display specific values in the rectangle tree chart. |
|Color Configuration |Color scheme |Set the color of the bar chart.<br><br>**Built\-in**: Display the bar chart according to the built\-in color scheme.<br><br>**Monochrome**: Display in the color of your choice.<br><br>**Threshold**: After specifying a threshold and color, if the actual value is greater than this threshold, it will be displayed in the corresponding color. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="1144b630"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

<span id="eed8efb2"></span>
## Example

Use a treemap chart to display the proportion of requests from each IP address.


* Sample query statement:

   ```SQL
   * | select COUNT(*) as PV, IP group by IP
   ```
   

* Chart configurations:

   * **Numeric source column**: In this example, `IP` is specified as the field that specifies categories.

   * **Category field source column**: In this example, the `PV` field is specified as the field to display. The clause `COUNT(*) as PV` is used to calculate the number of logs and use the log count as the value of PV.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36bfb5bead514bd2970c0ebb09cf33d0~tplv-goo7wpa0wc-image.image) </span>
