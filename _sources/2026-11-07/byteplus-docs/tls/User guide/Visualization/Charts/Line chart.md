---
title: "Line chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Line_chart"
---

Torch Log Service (TLS) supports line charts for displaying query and analysis results. This topic describes how to create a line chart.

<span id=".5Zu-6KGo6K-05piO"></span>
## Chart description

A line chart is used to display the change trends of time series data collected over a continuous time range. Therefore, a line chart allows you to analyze value changes over a time range.

Line charts in TLS support the time series mode and are used in scenarios of time series data analysis. For example, to analyze the distribution of operation types in different time ranges, you can integrate values of the dimension field such as QPS or traffic based on the values of the time field, and create a time series chart based on the time field, dimension field, and integration of values in the dimension field.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#.5rOo5oSP5LqL6aG5">Precautions</a>.</div>


<span id=".6YCa55So6YWN572u"></span>
## Common settings

Configure the global settings that apply to the entire chart. The basic settings of a line chart are as follows:


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |X\-axis field |Specify the field displayed on the X\-axis. We recommend that you specify a field with values in a specific order, such as a field specifying the time.<br><br>If the time series mode is enabled, the X\-axis is set to the time axis by default. |
||Y\-axis field |Specify the fields displayed on the Y\-axis. We recommend that you select multiple fields of the same type for analyzing the interactions and effects among the fields.<br><br>If the time series mode is enabled, the Y\-axis is the axis that displays metrics. |
|Data configuration |Timing mode |Specify whether to enable the time series mode. If you enable the time series mode, you must configure a dimension. |
||Classification field |Specify the field that you want to use to represent the data dimension. Only one dimension field is supported. The data type of the dimension field can be Long, Double, or Text, and the dimension field cannot be the same as the X\-axis or Y\-axis fields.<br><br>After enabling time series mode, you need to select a classification field. Supported field types include Long, Double, and Text, and these fields must not be duplicated with those used on the timeline or metric axis. |
||Maximum classification limit |Set the maximum number of categories for the classification field. When the number of different values in the classification field exceeds the maximum number of categories, the system will display the first N values.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An excessive number of categories can cause the page to lag.</div><br> |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Line chart style |Drawing method |Specify the display mode of data. Select the line to create a line chart, the bar to create a histogram, and the point to create a scatter chart. |
||Connection method |Specify whether to smooth the connections between data points.<br><br>When setting the **Drawing method** to **Line** , it needs to be set. |
||Line width |Specify the line width.<br><br>When setting the **Drawing method** to **Line or** **Column** , it needs to be set. |
||Fill transparency |Specify the transparency of the filled area.<br><br>When setting the **Drawing method** to **Line or** **Column** , it needs to be set. |
||Display point |Specify whether to display data points.<br><br>When setting the **Drawing method** to **Line** , it needs to be set. |
||Show Tag |Select whether to display the specific values of each data point.<br><br><br>* After setting both **Display point** and **Show Tag** to be shown, the specific values of the data points will be presented in the line chart.<br><br>* After setting **Display point** to be not shown and **Show Tag** to be shown, you need to hover the mouse over the chart in order to display the specific values of the data point. |
||Null value |Specify the mode for representing empty values in the chart.<br><br>When setting the **Drawing method** to **Line** , it needs to be set. |
||Point size |Specify the point size.<br><br>When setting the **Drawing** **method** to **Point**, it needs to be set. |
|Legend |Show legend |After checking the **Show Legend** option, the system will display the legend according to the position you have set. |
||Location |Specify the location of the legend in the chart. |
||Legend interaction |The action that is performed when you click a legend item.<br><br><br>* **Click Select**: When you click a legend item, only the data of the legend item is displayed in the chart.<br><br>* **Click Hide**: When you click a legend item, the data of the legend item is hidden and the data of other legend items is displayed. |
|Tooltip |Sort by |Specify the sorting of values, supporting default, ascending order, and descending order.<br><br>Hover your mouse over the line chart and the system will display the values according to the sort you set. |
||Display mode |Specify the display mode of the value, supporting the display of a single legend and all legends.<br><br>Hover your mouse over the line chart and the system will display the values according to the display mode you set. |
|X, Y axis style |X\-axis title |Specify the title of the X\-axis. |
||X\-axis scale Tag Angle |Specify the angle of the X\-axis scale tag. |
||Y\-axis title |Specify the title of the Y\-axis. |
||Y\-axis position |Specify the location of the axis. |
||Y\-axis minimum |Specify the minimum value that can be displayed on the Y\-axis scale. Values smaller than this value are not displayed. |
||Y\-axis maximum |Specify the maximum value that can be displayed on the Y\-axis scale. Values greater than this value are not displayed. |
|Threshold line style |Threshold configuration |Set the threshold point and color. |
||Display line |After checking the **Display line**, the system will display the corresponding threshold line in the line chart according to the threshold point you set. |
||show fill |After checking **Show Fill**, the system will display the color of the area to which the threshold belongs in the line chart according to the threshold point and color you set. |
|Color Configuration |Color scheme |Sets the color of the line chart.<br><br><br>* **Built\-in**: Displays line charts according to the built\-in color scheme.<br><br>* **Monochrome**: Displays the color of your choice. |
||Filling method |Set the color fill method, including solid color and gradual change. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id=".5a2X5q616YWN572u"></span>
## Field configuration

Select a field on the **Field configuration** tab, then configure a custom style for the field. The configurations on this tab apply only to the specified field, while other fields follow the settings configured on the **Common configuration** tab. The parameters on the **Field configuration** tab are the same as the parameters on **Common configuration** tab. For more information on the parameters, refer to [Common settings](https://docs.byteplus.com/docs/tls/Line_chart#.6YCa55So6YWN572u).

The figure below demonstrates the style configurations of the `SendFailReqs` field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de47f554ea8d42b6b1414de436576cdd~tplv-goo7wpa0wc-image.image) </span>

<span id="250126a0"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, set a drill\-down event on the **PV** field in a line chart. After you set Open topic drill\-down event on the PV field, click the point of a numeric value in the line chart, then select **Open topic**. You are then navigated to the page of the topic specified in the drill\-down event configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28e97c13143d412eb7b753330d41bdc8~tplv-goo7wpa0wc-image.image) </span>

<span id="926cc68d"></span>
## Example

Create a line chart to display the trend of PV value changes according to the time series on the X\-axis.


* Sample query statement:

   ```SQL
   * | SELECT date_format(__time__, 'Y-M-d HH:mm') AS time , COUNT(*) as PV group by time order by time
   ```
   

* Chart configurations:

   * **X\-axis field source column**: In this example, `time` is specified as the field displayed on the X\-axis. `time` is the alias of the field specifying time. In the SQL statement, `date_format(__time__, 'Y-M-d HH:mm')` specifies that the time interval is one minute.

   * **Y\-axis field source column**: In this example, the `PV` field is specified as the field displayed on the Y\-axis. The clause `COUNT(*) as PV` is used to calculate the number of logs and use the log count as the value of PV.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63fecee7c42647d895ae6822602e6985~tplv-goo7wpa0wc-image.image) </span>
