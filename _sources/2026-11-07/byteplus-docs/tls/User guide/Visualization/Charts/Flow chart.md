---
title: "Flow chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Flow_chart"
---

TLS supports flow charts for displaying query and analysis results. This topic describes how to create a flow chart.

<span id="0461544a"></span>
## Chart description

Flow charts are suitable for displaying data changes and distribution in different dimensions. The display forms of Log Service flow diagram include line diagram, stacked diagram and crosstab. Among them, the stacked chart is displayed by stacking columnar graphics, and the starting point of the column of the latter group of data is from the top of the column of the previous group of data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart, read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="7af04e31"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |X\-axis field |Specify the field displayed on the X\-axis. We recommend that you specify a field with values in a specific order, such as a field specifying the time. |
||Y\-axis field |Specify the fields displayed on the Y\-axis. |
||Aggregate field |Select a field based on which you want to further categorize and aggregate data. |
||Maximum classification limit |Set the maximum number of categories for the classification field. When the number of different values in the classification field exceeds the maximum number of categories, the system will display the first N values.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An excessive number of categories can cause the page to lag.</div><br> |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Flow graph style |Flow graph type |Specify the type of the flow chart. |
||Null value |Specify the mode for representing empty values in the chart. |
|Legend |Show legend |After checking the **Show Legend** option, the system will display the legend according to the position you have set. |
||Location |Specify the location of the legend in the chart. |
||legend interaction |The action that is performed when you click a legend item.<br><br><br>* **Click Select**: When you click a legend item, only the data of the legend item is displayed in the chart.<br><br>* **Click Hide**: When you click a legend item, the data of the legend item is hidden and the data of other legend items is displayed. |
|Tooltip |Sort by |Specify the sorting of values, supporting default, ascending order, and descending order.<br><br>Hover your mouse over the flow chart and the system will display the values according to the sort you set. |
||Display mode |Specify the display mode of the value, supporting the display of a single legend and all legends.<br><br>Hover your mouse over the flow chart and the system will display the values according to the display mode you set. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |
