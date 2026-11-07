---
title: "Pie chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Pie_chart"
---

Torch Log Service (TLS) supports pie charts for displaying query and analysis results. This topic describes how to create a pie chart.

<span id=".5Zu-6KGo6K-05piO"></span>
## Chart description

A pie chart is used to display the proportion of each category. The arc length of each slice in a pie chart is proportionate to the quantity of each category. A pie chart is divided into multiple slices based on the proportions of the specified categories.

TLS supports the following types of standard pie charts.


* **Pie chart**: This is the default type of pie chart. This type of chart displays two dimensions.

* **Donut chart**: Compared with a pie chart, a donut chart has a **hole** in the center. Each slice represents the proportion of a category. The sum of all slice values is equal to the total value. To compare multiple data sets, you can use a donut chart to display the proportion of each data set. Compare with the visual effect of pie charts, donut charts are more intuitive.

* **Polar area chart**: Polar area charts are also known as Nightingale rose charts. A polar area chart is generated in the polar coordinate system. Each category of data is represented by a slice. The radius length of each slice varies based on the corresponding value. Compared with pie charts, polar area charts have the following advantages.

   * Polar area charts are applicable to the scenarios where many categories exist. If the result that a query statement returns is classified into more than 10 categories, a polar area chart displays each category in a more intuitive manner than a pie chart does. If a pie chart is split into many slices, it is hard for you to identify the slices with very small proportions.

   * Polar area charts provide better comparison effect. Compared with a pie chart that displays value differences by slice size, a polar area chart enhances the differences among the values of different categories, and also enhances small value differences.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you use a pie chart, we recommend that you use the <code>limit</code> function to limit the number of data entries to return. For example, if 10 data entries are returned, the pie chart is split into 10 slices to display these data entries.</div>


* <div data-tips="true" data-tips-type="tip">If the number of categories exceeds 5,000, only the first 5,000 categories are displayed. The remaining categories are classified into the <strong>Other</strong> category.</div>


* <div data-tips="true" data-tips-type="tip">Before you configure a chart, read <a href="https://docs.byteplus.com/docs/tls/chart_overview#.5rOo5oSP5LqL6aG5">Precautions</a>.</div>



<span id=".6YCa55So6YWN572u"></span>
## Common settings

Configure the global settings that apply to the entire chart. The basic settings of a pie chart are as follows:


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Classification field |Select the field that specifies the categories to display. We recommend that you select a field with the STRING data type. |
||Value |Select the field that specifies the value displayed in each slice. The proportion of each category is calculated based on the value in this field. We recommend that you select a field that specifies numeric values. |
||Maximum classification limit |Set the maximum number of categories for the classification field. When the number of different values in the classification field exceeds the maximum number of categories, the system will display the first N values.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An excessive number of categories can cause the page to lag.</div><br> |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Pie chart style |Chart Type |Specify the chart style. By default, a pie chart with two dimensions is used. You can set the chart style to pie chart, donut chart, or polar area chart. |
||Sector tag |Specify whether to display labels in the chart.<br><br>Specify the label content to display. The label content can be percentage values of the slices. |
|Legend |Show legend |After checking the **Show Legend** option, the system will display the legend according to the position you have set. |
||Location |Specify the location of the legend in the chart. |
||legend interaction |The action that is performed when you click a legend item.<br><br><br>* **Click Select**: When you click a legend item, only the data of the legend item is displayed in the chart.<br><br>* **Clink Hide**: When you click a legend item, the data of the legend item is hidden and the data of other legend items is displayed. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="55a13ae4"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, set a drill\-down event on the PV field in a pie chart. After you set Open topic drill\-down event on the PV field, click a slice in the chart, then select **Open topic**. You are then navigated to the topic specified in the drill\-down event configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de2f40dc8be24fb2b596807b29e56d23~tplv-goo7wpa0wc-image.image) </span>

<span id="b3a0e306"></span>
## Example

Use a pie chart to display the proportions of access requests from different ip addresses.


* Sample query statement:

   ```SQL
   * | select ip, COUNT(*) as PV group by ip
   ```
   

* Chart configurations:

   * **Category field source column**: In this example, `ip` is specified as the field that specifies categories.

   * **Numeric source column**: In this example, the `PV` field is specified as the field to display. The clause `COUNT(*) as PV` is used to calculate the number of logs and use the log count as the value of PV.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a812b29c90be417bb8f46dfb7508b565~tplv-goo7wpa0wc-image.image) </span>
