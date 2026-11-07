---
title: "Radar chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Radar_chart"
---

TLS supports radar charts for displaying query and analysis results. This topic describes how to create a radar chart.

<span id="064e06e1"></span>
## Chart description

A radar chart can be used to compare multiple columns of data in the same dimension.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="6facb7ef"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Classification field |Specify the dimension to display data. |
||Value |Specify the numeric value to be displayed. |
||Maximum classification limit |Specify the maximum number of categories for the classification field. When the number of different values in the classification field exceeds the maximum number of categories, the system will display the first N values.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An excessive number of categories can cause the page to lag.</div><br> |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Radar chart style |Type |Specify the shape of the radar chart. Valid values: Polygon and Round. |
||Display tick text |If you enable **Display tick text**, the scale text information will be displayed in the radar chart. |
||Point size |Specify the size of the points in the radar chart. |
||Line width |Specify the width of the line in the radar chart. |
|Legend |Show legend |After checking the **Show Legend** option, the system will display the legend according to the position you have set. |
||Location |Specify the location of the legend in the chart. |
||Action behavior |The action that is performed when you click a legend item.<br><br><br>* **single legend**: When you click a legend item, only the data of the legend item is displayed in the chart.<br><br>* **all legends**: When you click a legend item, the data of the legend item is hidden and the data of other legend items is displayed. |
|Color Configuration |Color scheme |Specify the color of the radar chart.<br><br><br>* **built\-in**: displays the radar chart according to the built\-in color scheme.<br><br>* **Monochrome**: displays the color you have chosen. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="d7c2175f"></span>
## Field configuration

Select a field on the **Field configuration** tab, then configure a custom style for the field. The configurations on this tab apply only to the specified field, while other fields follow the settings configured on the **Common configuration** tab. The parameters on the **Field configuration** tab are the same as the parameters on **Common configuration** tab. For more information on the parameters, refer to @radar.

The following figure demonstrates that a special configuration is added to the `avg_SuccessReq` field. **Line width** is set to 10.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da0fe2ad8f044acc9c29cddf2ad06d75~tplv-goo7wpa0wc-image.image) </span>

<span id="20bb92ab"></span>
## Example

Use a radar chart to display the average request length and average length of successful request corresponding to requests at each IP address within a specified time range.


* Sample query statement

   ```SQL
   * | SELECT ip, AVG(SendTotalReqs) AS avg_TotalReqs, AVG(SendSuccessReqs) AS avg_SuccessReqs GROUP BY ip
   ```
   

* Table view

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3537b07785ae4d9db3fb28823c676d5e~tplv-goo7wpa0wc-image.image) </span>

* Chart configurations

   * **Category field source column**: `level`

   * **Numeric field source column**: `avg_TotalReqs`, `avg_SuccessReqs`

* Radar chart

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b723a9dacdd74549a766814a473b295a~tplv-goo7wpa0wc-image.image) </span>
