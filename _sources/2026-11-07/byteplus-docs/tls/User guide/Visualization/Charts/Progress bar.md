---
title: "Progress bar"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Progress_bar"
---

Torch Log Service (TLS) supports progress bars for displaying query and analysis results. This topic describes how to create a progress bar chart.

<span id="524571e0"></span>
## Chart description

A progress bar is a rectangular bar that is used to display percentage values. Progress bars are often used to represent the progress of tasks. TLS allows you to customize the display style of a progress bar, including the edge shape, font size, and bar thickness.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="c8a35204"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis |Progress bar field |The progress bar displays the percentage of the value specified by the<br><br>**Progress bar field source column** field to the value specified by the Total value. Set **Query the total value** by field to the field that stores the numeric values for generating percentage values displayed on the progress bar. By default, the value in the first row of the specified column is used. |
||Total value |Specify whether to use the current query result as the total value for generating a percentage value.<br><br><br>* Enable: you must select a query field, and the system will use the maximum value of the field as the total value.<br><br>* disable: You must set a custom value. Default value: 100. |
|Standard configuration |Decimal point |Specify the decimal places of the numeric values. |
|Progress bar style |Corner |Specify the edge shape of the progress bar. A progress bar can be with rounded or straight corners. |
||Display method |Specify the display method of the progress bar. |
||Font size |Specify the font size of the percentage value displayed. |
||Progress bar thickness |Specify the thickness of the progress bar. |
|Color Configuration |Progress bar base color |Specify the background color of the progress bar. |
||Text color |Specify the color of the percentage value text. |
||Color display |Specify the color scheme of the progress bar. Valid values:<br><br><br>* **Default color**: If you select this option, you must configure the default color of the progress bar.<br><br>* **Gradual change**: If you select this option, you must configure the start and end colors of the gradient.<br><br>* **Show according to the rules**: If you select this option, you must configure the **Display color**, **udgment condition**, and **critical value** parameters. If the value of the field specified in **Progress bar field source column** meets the condition specified by the rule, the progress bar is displayed in the color specified by the rule. Otherwise, the progress bar is displayed in the default color. In case of rule conflict, the last rule applies. |
|Link ||Support for adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="78b18c53"></span>
## Example

Use a progress bar to display the error rate of the day.


* Sample query statement:

   ```SQL
   * | SELECT SUM(if(Status = 'error',1,0)) as error, COUNT(*) as total
   ```
   

* Chart configurations:

   * **Progress bar field source column**: In this example, `error` is specified. The `error` field specifies the number of requests that are in the `error` state.

   * **Query the total value by field**: In this example, `total` is specified. In the SQL statement, `COUNT(*) as total` is used to calculate the total number of logs, and the calculation result is used as the total value.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bc4873938884f3286fbe9977ec688ea~tplv-goo7wpa0wc-image.image) </span>
