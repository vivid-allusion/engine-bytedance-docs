---
title: "Statistics chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Statistics_chart"
---

Torch Log Service (TLS) supports statistics charts for displaying query and analysis results. This topic describes how to create a statistics chart.

<span id="366f2e75"></span>
## Chart description

A statistics chart consists of one or more single\-value charts. In a statistics chart, each field queried is displayed and highlighted in a single\-value chart. This helps you quickly view key information. Statistics charts also allow you to compute the data in the specified fields, and provide optional charts and comparison charts.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="3267840a"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Main field |Select the field that you want to display in a single\-value chart. You can select multiple fields. |
||Trend comparison field |Select the field whose values you want to compare with the specified comparison threshold. You can select only one field.<br><br>The same calculation function is used to calculate values for the comparison field and the displayed field. |
||Trend comparison field description |Describe the comparison. The description is displayed in a single\-value chart. |
||Trend comparison threshold |Specify the threshold value that you want to use to measure the trend. If the value of the **Trend comparison field** is greater than or equal to the **Trend comparison threshold**, a red upward arrow is displayed in the single\-value chart; otherwise, a green downward arrow is displayed. |
|Data configuration |Display content |Specify the display mode of the chart. Valid values:<br><br><br>* **Calculated value**: If you select this option, only the value calculated by the calculation function is displayed.<br><br>* **All values**: If you select this option, all values of the specified fields from a query result are displayed. |
||Calculation function |Specify the function that you want to use to calculate values.<br><br>If you set the value of **Data display mode** to **Calculated value**, you must configure this parameter for computing query results. |
||Tag |Specify the tag information.<br><br>If you set the value of **Data display mode** to **Calculated value**, you must configure this parameter. |
||Number limit |Specify the number of bars that you want to display in the chart.<br><br>If you set the value of **Data display mode** to **All value**, you must configure this parameter. |
||Tag source column |Specify the description field.<br><br>If you set the value of **Data display mode** to **All value**, you must configure this parameter. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
||Contrast value formatting |Specify the format of the comparison value. |
||Comparison value preserving decimal point |Specify the number of decimal places after the comparison value. |
||Unit of comparison |Specify the unit of comparison value. |
|Chart style |Layout |Specify the layout of the single\-value charts in the chart. Valid values:<br><br><br>* Adaptive: The layout is automatically adjust based on the size of each single\-value chart.<br><br>* Vertical: The single\-value charts are horizontally arranged from left to right.<br><br>* Horizontal: The single\-value charts are vertically arranged from top to bottom. |
||Text mode |Specify the display mode of texts in the single\-value charts.<br><br><br>* Automatic: The text content is automatically displayed based on the statistical results.<br><br>* Value: Only the numeric values are displayed. The titles of the single\-value charts are not displayed.<br><br>* Value and title: Both numeric values and titles are displayed.<br><br>* Title: Only the titles of the single\-value charts are displayed. The numeric values are not displayed.<br><br>* without: No content is displayed. |
||Text alignment |Specify the method of aligning texts.<br><br><br>* Automatic: The text is automatically aligned based on the length of the content.<br><br>* Center: The text is centered. |
||Main field font size |Specify the font size of the titles of the single\-value charts. |
||Description value font size |Specify the font size of the description value. |
||Tag font size |Specify the font size of the numeric values. |
||Show trend chart |After checking **Show trend chart** , the trend of each value of the main field will be displayed on the chart. |
|Color Configuration |Define text color |Specify the color mode of the single\-value charts.<br><br><br>* **Monochrome**: Only the area charts representing the values are filled with colors.<br><br>* **Defined by threshold**: The background color is displayed, and the area charts representing the values are filled with colors. |
||Define the background color |Specify the display mode of the area charts.<br><br><br>* **Monochrome**: The area charts representing the values are not displayed. Only the numeric values are displayed.<br><br>* **Defined by threshold**: The area charts representing the values are displayed. |
|Value mapping |Value mapping |Click **Add map value**, then configure a mapping. TLS automatically maps matched content to the specified field. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="16784425"></span>
## Field configuration

Select a field on the **Field configuration** tab, then configure a custom style for the field. The configurations on this tab apply only to the specified field, while other fields follow the settings configured on the **Common configuration** tab. The parameters on the **Field configuration** tab are the same as the parameters on **Common configuration** tab. For more information on the parameters, refer to [Common settings](https://docs.byteplus.com/docs/tls/Statistics_chart#3267840a).

The following figure demonstrates that a special configuration is added to the `pv` field. The font size of the corresponding title is set to 80.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9caf3d69cdbd461899f56ef29aad3aa8~tplv-goo7wpa0wc-image.image) </span>

<span id="dccfebcd"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, set a drill\-down event on the **pv** field in a chart. After you set an Open topic drill\-down event on the **pv** field, click the value of this field in the chart, then select **Open topic**. You are then navigated to the topic specified in the drill\-down event configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb2754d33dab4033bb680d3d3d2a10a9~tplv-goo7wpa0wc-image.image) </span>

<span id="ed6d93fb"></span>
## Example

Use a statistics chart to display the difference between the PVs of the current day and the previous day.


* Sample query statement:

   ```SQL
   * |select pv, (pv - yesterday) as count ,time from (select pv,lag(pv,1,0) over() as yesterday,time  from (SELECT COUNT(*) AS pv, ((__time__ / 1000) - ((__time__ / 1000) % 86400)) as time GROUP BY time ORDER BY time DESC limit 10000) limit 10000) order by time ASC limit 1
   ```
   

* Chart configurations:

   * **Main field source column**: In this example, `pv` is specified as the field to display. The `pv` field specifies the page view statistics of the current day. In the SQL statement, `((__time__ / 1000) - ((__time__ / 1000) % 86400))` specifies that the data aggregation dimension is one day.

   * **Compare field source column**: In this example, `count` is specified as the field for comparison. `lag(pv,1,0) over()` is used to retrieve the page view statistics of the previous day, and `(pv - yesterday)` is used to calculate the difference between the page view statistics of the two days.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a266f0ea94549f0844c29bd88f943c6~tplv-goo7wpa0wc-image.image) </span>
