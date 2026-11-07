---
title: "Histogram"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Histogram"
---

Torch Log Service (TLS) supports histograms for displaying query and analysis results. This topic describes how to create a histogram.

<span id="b461cca6"></span>
## Chart description

A histogram consists of vertical bars that demonstrate data distribution across continuous intervals. You can determine the approximate locations of medians, locations of data gaps, and locations of significant outliers in histograms. The X\-axis represents the numeric values of the specified continuous variables.

Compared with column charts, histograms are more statistically significant. The following table describes the differences between histograms and column charts:


|Item |Histogram |Column Chart |
|---|---|---|
|Data types on X\-axis |The X\-axis displays numeric values of continuous intervals, such as time ranges, date ranges, and age ranges. |The X\-axis displays categorical data, such as provinces, countries, genders, and sources of requests. |
|Continuity of data on X\-axis |The X\-axis displays continuous data, and no gaps exist in each bar. You can use a histogram to display data distribution across continuous intervals. |The X\-axis displays discontinuous data, and each bar represents a category. You can use a column chart to display the comparison among different categorical data. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart, read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="d069fac0"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |X\-axis field |Specify the field displayed on the X\-axis. We recommend that you specify a field with values in a specific order, such as a field specifying the time.<br><br>If the time series mode is enabled, the X\-axis is set to the time axis by default. |
||Y\-axis field |Specify the fields displayed on the Y\-axis. We recommend that you select multiple fields of the same type for analyzing the interactions and effects among the fields.<br><br>If the time series mode is enabled, the Y\-axis is the axis that displays metrics. |
|Data configuration |Timing mode |Specify whether to enable the time series mode. To enable the time series mode, you must configure the following parameters:<br><br><br>* **Single column time range**: The time interval represented by each bucket.<br><br>* **Number of buckets**: The number of buckets. This parameter is available only when the value of **Single column time range** is set to **Default**. |
||Histogram coordinate unit size |The step length of each interval on the X\-axis. This parameter is available only when the time series mode is disabled. If this parameter is configured, the value on the Y\-axis of each bar is the sum of the values represented by the buckets on the Y\-axis. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Histogram Style |Display mode |The mode of merging bars. If you specify multiple fields for the Y\-axis, you must configure this parameter. Valid values:<br><br><br>* **not synthesized**: Each bar represents the value of one field, and the start value of each bar is 0.<br><br>* **synthesis**: The values of the specified fields are merged and represented by one bar.<br><br>* **Stack**: The bars representing the values of the specified fields are stacked and do not overlap with each other. |
||Display method |The direction of bars. The bars can be in horizontal or vertical direction. |
||Stroke width |The border width. |
||Filling method |The gradient style of the bars in the chart. Valid values:<br><br><br>* **Gradual change**: Each bar is filled with gradient colors, and the color gradient is affected by the value of the **Fill transparency** parameter.<br><br>* **solid color**: Gradient is disabled. Each bar is filled with solid colors. |
||Fill transparency |The transparency of the bars. |
||Display value |specify whether to display the numeric values that are represented by the bars. |
|Legend |Show legend |After checking the **Show Legend** option, the system will display the legend according to the position you have set. |
||Location |Specify the location of the legend in the chart. |
||Legend interaction |The action that is performed when you click a legend item.<br><br><br>* **Click Select**: When you click a legend item, only the data of the legend item is displayed in the chart.<br><br>* **Click Hide**: When you click a legend item, the data of the legend item is hidden and the data of other legend items is displayed. |
|X, Y axis style |X\-axis title |Specify the title of the X\-axis. |
||X\-axis scale Tag Angle |Specify the angle of the X\-axis scale tag. |
||Y\-axis title |Specify the title of the Y\-axis. |
||Y\-axis position |Specify the location of the axis. |
||Y\-axis minimum |Specify the minimum value that can be displayed on the Y\-axis scale. Values smaller than this value are not displayed. |
||Y\-axis maximum |Specify the maximum value that can be displayed on the Y\-axis scale. Values greater than this value are not displayed. |
|Color Configuration |Color scheme |Set the color of the bar chart.<br><br>**Built\-in**: Display the bar chart according to the built\-in color scheme.<br><br>**Monochrome**: Display in the color of your choice.<br><br>**Threshold**: After specifying a threshold and color, if the actual value is greater than this threshold, it will be displayed in the corresponding color. |
||Filling method |Set the color fill method, including solid color and gradient. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="ff3e809f"></span>
## Field configuration

Select a field on the **Field configuration** tab, then configure a custom style for the field. The configurations on this tab apply only to the specified field, while other fields follow the settings configured on the **Common configuration** tab. The parameters on the **Field configuration** tab are the same as the parameters on **Common configuration** tab. For more information on the parameters, refer to [Common settings](https://docs.byteplus.com/docs/tls/Histogram#d069fac0).

<span id="9c59d3ca"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, set a drill\-down event on the **GET** field and the **POST** field displayed in a histogram separately. After you add Open topic drill\-down events to the GET and POST fields, click a bucket in the histogram, then select **Open topic**. You are then navigated to the topic that you specified in the drill\-down event configuration.

<span id="4d5961d3"></span>
## Example

Use a histogram to display the statistics of GET and POST requests collected every hour.


* Sample query statement:

   ```SQL
   * | select (__time__ - __time__ % 60000) as t, SUM(if(Method='GET',1,0)) as GET, SUM(if(Method='POST',1,0)) as POST group by t order by t
   ```
   

* Chart configurations:

   * **X\-axis field source column**: In this example, `t` is specified as the field displayed on the X\-axis. `t` is the alias of the field specifying time. In the SQL statement, `(__time__ - __time__ % 60000)` specifies that the time interval is one minute.

   * **Y\-axis field source column**: In the SQL statement, `SUM(if(Method='GET',1,0)) as GET` is used to specify the statistics of GET requests, and `SUM(if(Method='POST',1,0)) as POST` is used to specify the statistics of POST requests.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cd0adfcace04d69bbeca617b77f354f~tplv-goo7wpa0wc-image.image) </span>
