---
title: "Bar chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Column_chart"
---

Torch Log Service (TLS) supports bar charts for displaying query and analysis results. This topic describes how to create a bar chart.

<span id="图表说明"></span>
## Chart description

Bar charts are used to display the statistics of different categories. A category is represented by a bar whose height indicates the statistics of the category.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart, read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="通用配置"></span>
## Common settings

Configure the global settings that apply to the entire chart. The basic settings of a bar chart are as follows:


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |X\-axis field |Specify the field displayed on the X\-axis. We recommend that you specify a field with values in a specific order, such as a field specifying the time. |
||Y\-axis field |Specify the fields displayed on the Y\-axis. We recommend that you select multiple fields of the same type for analyzing the interactions and effects among the fields. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Bar gauge style |Heap stacking |Specify the stacking method for the data columns. |
||Display method |Specify the orientation of the data bar. |
||Column width |Specify the width of the data bar. |
||Stroke width |Specify the edge width of the data bar. |
||Opacity |Specify the opacity of the data bar. |
||Display value |specify whether to display the numeric values that are represented by the bars. |
|Legend |Show legend |After checking the **Show Legend** option, the system will display the legend according to the position you have set. |
||Location |Specify the location of the legend in the chart. |
||legend interaction |The action that is performed when you click a legend item.<br><br><br>* **single legend**: When you click a legend item, only the data of the legend item is displayed in the chart.<br><br>* **all legends**: When you click a legend item, the data of the legend item is hidden and the data of other legend items is displayed. |
|Tooltip |Sort by |Specify the sorting of values, supporting default, ascending order, and descending order.<br><br>Hover your mouse over the bar chart and the system will display the values according to the sort you set. |
||Display mode |Specify the display mode of the value, supporting the display of a single legend and all legends.<br><br>Hover your mouse over the bar chart and the system will display the values according to the display mode you set. |
|X, Y axis style |X\-axis title |Specify the title of the X\-axis. |
||X\-axis scale Tag Angle |Specify the angle of the X\-axis scale tag. |
||Y\-axis title |Specify the title of the Y\-axis. |
||Y\-axis position |Specify the location of the axis. |
||Y\-axis minimum |Specify the minimum value that can be displayed on the Y\-axis scale. Values smaller than this value are not displayed. |
||Y\-axis maximum |Specify the maximum value that can be displayed on the Y\-axis scale. Values greater than this value are not displayed. |
|Color Configuration |Color scheme |Specify the color of the histogram.<br><br><br>* **Built\-in** : Displays histograms according to the built\-in color scheme.<br><br>* **Monochrome** : Displays the color of your choice.<br><br>* **Threshold** : After specifying the threshold point and color, if the actual value is greater than the threshold point, it will be displayed as the corresponding color. |
||Filling method |Specify the color fill method, including solid color and gradual change. |
|link ||Support for adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="e028ff60"></span>
## Field configuration

Select a field on the **Field configuration** tab, then configure a custom style for the field. The configurations on this tab apply only to the specified field, while other fields follow the settings configured on the **Common configuration** tab. The parameters on the **Field configuration** tab are the same as the parameters on **Common configuration** tab. For more information on the parameters, refer to [Common settings](https://docs.byteplus.com/docs/tls/Column_chart#%E9%80%9A%E7%94%A8%E9%85%8D%E7%BD%AE).

For example, the following example shows adding field configurations to **avg_respsize** and **avg_reqsize** fields to customize different colors for the columns where the two fields are located.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb71ffa8758d4ece9ecd77c472b4252c~tplv-goo7wpa0wc-image.image) </span>

<span id="6d61e5a3"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, set a drill\-down event on the **PV** field in a bar chart. After you set Open topic drill\-down event on the PV field, click a bar in the bar chart and select **Open topic**. You are then navigated to the page of the topic specified in the drill\-down event configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d90ae78801c466584a2b947d052ef75~tplv-goo7wpa0wc-image.image) </span>

<span id="3b57a2c7"></span>
## Example

Use a bar chart to display the PV statistics of each ip.


* Sample query statement:

   ```SQL
   * |  ip, COUNT(*) as PV group by ip
   ```
   

* Chart configurations:

   * **X\-axis field source column**: In this example, `ip` is specified as the field displayed on the X\-axis.

   * **Y\-axis field source column**: In this example, the `PV` field is specified as the field displayed on the Y\-axis. The clause `COUNT(*) as PV` is used to calculate the number of logs and use the log count as the value of PV.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39df99e209344a05a5788e68f7f4f277~tplv-goo7wpa0wc-image.image) </span>
