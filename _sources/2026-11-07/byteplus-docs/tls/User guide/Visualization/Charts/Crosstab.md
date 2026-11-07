---
title: "Crosstab"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/cross-table"
---

Torch Log Service (TLS) supports crosstabs to show the log query and analysis results. This topic describes how to create a crosstab .

<span id="b2a4e8a0"></span>
## Diagram description

Cross tables are mainly used to classify data and to show the relationships between categories. The row headers in the crossover table represent different values of one categorical variable, and the list headers represent different values of another categorical variable.

For example, if you display the number of logs corresponding to each log level every 5 minutes through a normal table, the effect is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d377107380c24f8fa78b529e049f79db~tplv-goo7wpa0wc-image.image) </span>

When you use a cross table, the system classifies the display by time and log level, with the following effects:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f2993b09f144de1adba8acd783237df~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart, read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="b393bd3f"></span>
## Common settings

Configure the global settings that apply to the entire chart. The basic settings of a crosstab are as follows:


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Line field |Specify the row field used for classification. |
||Column dimension |Specify the column field used for classification. |
||Cross value |Specify the field to use for aggregate statistics. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|crosstab style |Column width |Specify the width of each column in px. |
||Font size |Specify the font size of the text in the crosstab. |
||Text alignment |Specify the alignment of each column to the left by default. |
||Display sorting |When **Show Sort** is checked, the crosstab table is sorted by the specified field value.<br><br><br>* Sort field: Select the field to sort.<br><br>* Sort by: Select ascending or descending order. |
||Paging |When **Paging** is checked, paging is supported according to the number of pages you specify. |
||Display filter component |When the **Display filter component** is checked, the filter icon is displayed in the header, allowing you to filter field values by the filter component. |
||Display row count |When the **Display row count** is checked, the total number of rows in the crossover table is displayed in the lower right corner of the crossover table. |
||Header |When the **Header** is checked, the header will be displayed in the cross table. |
|Color Configuration |Define text color |Specify the color of the text in the crosstab.<br><br><br>* **Monochrome**: Uniformly set to one color.<br><br>* **Defined by threshold**: After clicking **Add Threshold Point** and setting the color and threshold, a value is highlighted in a custom color if it exceeds the threshold. |
||Define the background color |Specify the color of the crosstab background.<br><br><br>* **Monochrome**: Uniformly set to one color.<br><br>* **Defined by threshold**: After clicking **Add Threshold Point** and setting the color and threshold, if a value exceeds the threshold, the cell background for that value is highlighted in a custom color. |
|Value mapping |Value mapping |When you click **Add map value** and set the mapping method,TLS automatically maps the matched content to the specified text. |
|Link ||Support for adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="0a3060c4"></span>
## Example

Display the number of logs for each log level in 5\-minute intervals using a crosstab.


* Query and analysis statement

   ```SQL
   * | SELECT  DATE_FORMAT(__time__ - __time__ % 300000, 'Y-M-d HH:mm') AS time, level, COUNT (*) AS total GROUP BY time, level ORDER BY time
   ```
   

* Chart settings

   * **Line field** : Specified as `time`. Here, `time` is an alias for the time field `time`, and the time interval is set to 5 minutes using `DATE_FORMAT(time - time % 300000, 'Y-M-d HH:mm')`, converting the time format to `Y-M-d HH:mm`.

   * **Column dimension** : Specified as `level`.

   * **Cross value** : Specified as `total`, calculated using `COUNT(*)`.

* Statistical chart

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e47d13cd6714014af3d6b8438361c96~tplv-goo7wpa0wc-image.image) </span>
