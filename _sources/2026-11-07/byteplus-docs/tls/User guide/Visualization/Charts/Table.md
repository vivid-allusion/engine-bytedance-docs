---
title: "Table"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Table"
---

Torch Log Service (TLS) supports tables for displaying query and analysis results. This topic describes how to create a table.

<span id="图表说明"></span>
## Chart description

Tables are popular charts used to display data. TLS allows you to display results of SQL queries in tables.

Tables support the paging feature. By default, each page can contain up to 10 data entries.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart, read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="通用配置"></span>
## Common settings

Configure the global settings that apply to the entire chart. The basic settings of a table are as follows:


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Hidden field |Specify the fields that you want to hide. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Table style |Column width |Specify the column width of the table. Unit: pixels. |
||Font size |Specify the font size of the text in the table. |
||Text alignment |Specify the method of aligning the content in each column. By default, content is aligned left. |
||Display sorting |When the **Display sorting** is checked, the system supports sorting the table contents according to the specified field values.<br><br><br>* Sort field: Select the field to sort.<br><br>* Sort by: Select ascending or descending order. |
||Display filter component |When the **Display filter component** is checked, the filter icon will be displayed in the header, and you can filter field values by the filter component. |
||Display row count |After checking **Display row count**, the system will display the total number of rows in the table in the lower right corner of the table. |
||Paging |Specify whether to enable the paging feature. If you want to enable the paging feature, you must specify the number of data entries displayed on each page. |
||Header |Specify whether to display the headers of the table. |
|Color Configuration |Define text color |Set the color of the text in the table.<br><br><br>* **Monochrome**: Set uniformly to one color.<br><br>* **Defined by threshold**: Click **Add threshold point**, then specify a color and a threshold. If a value exceeds the threshold, the text color is highlighted in a custom color. |
||Define the background color |Set the color of the table background.<br><br><br>* **Monochrome**: Set uniformly to one color.<br><br>* **Defined by threshold**: Click **Add threshold point**, then specify a color and a threshold. If a value exceeds the threshold, the cell background for that value is highlighted in a custom color. |
|Value mapping |Value mapping |Click **Add map value**, then configure a mapping. TLS automatically maps matched content to the specified field. |
|Link ||Support for adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="字段配置"></span>
## Field configuration

Select a field on the **Field configuration** tab, then configure a custom style for the field. The configurations on this tab apply only to the specified field, while other fields follow the settings configured on the **Common configuration** tab. The parameters on the **Field configuration** tab are the same as the parameters on **Common configuration** tab. For more information on the parameters, refer to [Common settings](https://docs.byteplus.com/docs/tls/Table#%E9%80%9A%E7%94%A8%E9%85%8D%E7%BD%AE).

The following figure demonstrates that a special configuration is added to the `SendFailReqs` field and the threshold value is set to `6000`. In the column, values greater than 6000 will be highlighted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acd5523ce0b547e09de8663460a1ebf1~tplv-goo7wpa0wc-image.image) </span>

<span id="1bc4eaab"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, set a drill\-down event on the **area** field in a table. After you set the Open dashboard drill\-down event named ViewDatabyCity on the **area** field, click a value in the area column, then select **ViewDatabyCity**. You are then navigated to the dashboard specified in the drill\-down event configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/462677105ab648aab74d6950e2184bb2~tplv-goo7wpa0wc-image.image) </span>

The configurations of the drill\-down event are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9949228c6de145c7b3ead346db62f45b~tplv-goo7wpa0wc-image.image) </span>
