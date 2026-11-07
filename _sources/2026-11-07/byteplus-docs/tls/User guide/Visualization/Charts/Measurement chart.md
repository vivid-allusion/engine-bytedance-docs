---
title: "Measurement chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Gauge_chart"
---

TLS supports measurement charts for displaying query and analysis results. This topic describes how to create a measurement chart.

<span id="37d75809"></span>
## Chart description

A measurement chart consists of one or more bars. Statistical values of the specified fields are displayed in the chart, allowing you to view the proportion of the statistical values collected within a specific range. Measurement charts support multiple display styles and color schemes for customizing display effects. Measurement charts support the following display styles: solid colors, gradient colors, segmented bars, and dashboards.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="6d74a5d6"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Main field |Select the fields that you want to display in the measurement chart. You can select multiple fields. |
||Maximum value |Specify the maximum value that you want to display in the measurement chart. If you enable **Query maximum value by field**, specify the column from which you want to get the maximum value. Torch Log Service (TLS) automatically displays the maximum value in the column. |
||Minimum value |Specify the minimum value that you want to display in the measurement chart. If you enable **Query maximum value by field**, specify the column from which you want to get the minimum value. TLS automatically displays the minimum value in the column. |
|Data configuration |Display content |Specify the display mode of the measurement chart. Valid values:<br><br><br>* **Calculated value**: If you select this option, only the value calculated by the calculation function is displayed.<br><br>* **All values**: If you select this option, all values of the specified fields from a query result are displayed. |
||Calculation function |Specify the function that you want to use to calculate values. If you set the value of **Data display mode** to **Calculated value**, you must configure this parameter for computing query results. |
||Tag |Specify the tag information.<br><br>If you set the value of **Data display mode** to **Calculated value**, you must configure this parameter. |
||Number limit |Specify the number of bars that you want to display in the chart. If you set the value of **Data display mode** to **Calculated valueAll values**, you must configure this parameter. |
||Tag source column |Specify the bar title. If you set the value of the **Data display mode** parameter to **Calculated valueAll values**, you must configure this parameter. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Gauge chart style |Chart Type |Specify the display style of the measurement chart. |
||Layout |Specify the layout mode of the bars. The arrangement of the bars can be horizontal, vertical, or self\-adaptive. |
||Rounded corners |Specify the corner radius of the shape. |
||Thickness |When setting the **Chart Type** to **basic**, **continuous gradual change**, or **A gradual change**, this parameter is used to adjust the thickness of the bars. |
||Main field font size |Specify the font size of the title. |
||Tag font size |Specify the font size of the text indicating the percentage values. |
||Display base color |After checking the **Display base color** option, the background color will be displayed.<br><br>When setting the **Chart Type** to **basic**, **continuous gradual change**, or **A gradual change**, this parameter needs to be set. |
||Title |Specify whether to display the chart title on the dashboard. |
||Percentage |Specify whether to display the percentage value of each bar. |
|Color configuration ||Specify the color scheme of the measurement chart. Valid values:<br><br><br>* **Threshold**: After specifying the threshold point and color, if the actual value of a bar exceeds this threshold point, it will be displayed in the corresponding color.<br><br>* **Percentage threshold**: After specifying the threshold point and color, if the percentage of a bar exceeds this threshold point, it will be displayed in the corresponding color. |
|Value mapping ||Click **Add map value**, then configure a mapping. TLS automatically maps matched content to the specified field. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="32144192"></span>
## Field configuration

Select a field on the **Field configuration** tab, then configure a custom style for the field. The configurations on this tab apply only to the specified field, while other fields follow the settings configured on the **Common configuration** tab. The parameters on the **Field configuration** tab are the same as the parameters on **Common configuration** tab. For more information on the parameters, refer to [Common settings](https://docs.byteplus.com/docs/tls/Gauge_chart#6d74a5d6).

The following figure demonstrates that a special configuration is added to the `normal` field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20ac85931fd447a9b37be6726de2c6c7~tplv-goo7wpa0wc-image.image) </span>

<span id="69171e1f"></span>
## Example

Use a measurement chart to display the number and proportion of normal request.


* Sample query statement:

   ```SQL
   * | SELECT SUM(if(HeartbeatStatus = 'normal',1,0)) as normal, COUNT(*) as total
   ```
   

* Chart configurations:

   * **Main field source column**: In this example, `normal` is specified as the field to display.

   * **Maximum value**: In this example, `total` is specified. In the SQL statement, `COUNT(*) as total` is used to calculate the number of requests.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36ccdee9f4d647cb9a5fd7ed66c7f697~tplv-goo7wpa0wc-image.image) </span>
