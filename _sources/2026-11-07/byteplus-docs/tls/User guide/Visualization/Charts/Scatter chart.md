---
title: "Scatter chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/scatter_chart"
---

Torch Log Service (TLS) supports scatter charts to show the log query analysis results. This topic describes how to create a scatter chart.

<span id="cdf6915d"></span>
## Chart description

A scatter plot distributes data in the form of points in a Cartesian coordinate system, and the position of the points is determined by the value of the variable. You can determine the correlation between variables by the distribution of data points.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="951e7d6a"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |X\-axis field |Specify the field to display on the X\-axis. |
||Y\-axis field |Specify the field displayed on the Y\-axis. We recommend that you select multiple fields of the numeric type for analyzing the interactions and effects among the fields. |
||Classification field |Specify the field for data classification. |
||Maximum classification limit |Set the maximum number of categories for the classification field. When the number of different values in the classification field exceeds the maximum number of categories, the system will display the first N values.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An excessive number of categories can cause the page to lag.</div><br> |
||Point size |Specify a field to dynamically size the data points. |
|Standard configuration (Y\-axis only) |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Scatter chart style |Line width |Specify the width of the line. |
||opacity |Specify the opacity of the area . |
||Point size |Specify the size of the point.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you set the <strong>Point size</strong> in the <strong>Query and analysis field</strong> area, the <strong>Point size</strong> configuration item does not take effect.</div><br> |
|Legend |Show legend |After checking the **Show Legend** option, the system will display the legend according to the position you have set. |
||Location |Specify the location of the legend in the chart. |
||legend interaction |The action that is performed when you click a legend item.<br><br><br>* **Click Select**: When you click a legend item, only the data of the legend item is displayed in the chart.<br><br>* **Click Hide**: When you click a legend item, the data of the legend item is hidden and the data of other legend items is displayed. |
|X, Y axis style |X\-axis title |Specify the title of the X\-axis. |
||X\-axis scale Tag Angle |Specify the angle of the X\-axis scale tag. |
||X\-axis position |Specify the position of the X axis. |
||Y\-axis title |Specify the title of the Y\-axis. |
||Y\-axis position |Specify the position of the Y\-axis. |
||Y\-axis minimum value |Specify the minimum value that can be displayed on the Y\-axis scale. Values smaller than this value are not displayed. |
||Y\-axis maximum |Specify the maximum value that can be displayed on the Y\-axis scale. Values greater than this value are not displayed. |
|Color Configuration |Color scheme |After specifying the threshold point and color, if the actual value is greater than the threshold point, it is displayed as the corresponding color. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="4da8474b"></span>
## Field Configuration

Select a field on the **Field configuration** tab, then configure a custom style for the field. The configurations on this tab apply only to the specified field, while other fields follow the settings configured on the **Common configuration** tab. The parameters on the **Field configuration** tab are the same as the parameters on **Common configuration** tab. For more information on the parameters, refer to [Common settings ](https://docs.byteplus.com/docs/tls/scatter_chart#951e7d6a).

For example, the following figure shows the `ReqSize`column and `RespSize`column in the query analysis result to add field configuration, set the data point size of the `ReqSize`column to 5, and set the data point size of the `RespSize`column to 10.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71ab50e93f144e12bb493c5f656ff08a~tplv-goo7wpa0wc-image.image) </span>

<span id="fb98e1d0"></span>
## Field configuration

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, set a drill\-down event on the `ReqSize` \*\*\*\* field in the scatter chart. After you set Open topic drill\-down event on the `ReqSize` field, click the point of a numeric value in the scatter chart, and then click **Open topic** , the page will automatically jump to the topic you set.

<span id="923f7c89"></span>
## Example

shows the distribution of request body sizes and response body sizes in different request states through a scatter chart.


* Query and analysis Statement

   ```SQL
   * | SELECT status, ReqSize, RespSize
   ```
   

* Chart Settings

   * Sets the **X\-axis field source column** to `status`.

   * Set the **Y\-axis field source column** to `ReqSize`, `RespSize`.

* Scatter chart

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ddd0f74f0e646998df3d7ae9e62843d~tplv-goo7wpa0wc-image.image) </span>
