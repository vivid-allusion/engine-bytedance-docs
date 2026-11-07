---
title: "Funnel Chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/funnel_chart"
---

TLS supports funnel charts for displaying query and analysis results. This topic describes how to create a funnel chart.

<span id="ac93cfdb"></span>
## Chart Description

A funnel chart displays the quantity differences between various categories through the area of trapezoids, starting with a 100% quantity and ending with a smaller quantity. There is a logical order from top to bottom in the funnel chart, showing the progress of business objectives as the business process progresses (such as order conversion). It is suitable for single process single item analysis with standardized business processes, long cycles, and multiple stages.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="ad271397"></span>
## General Configuration

global configuration for the specified type of statistical chart, with effect for the entire chart range. The common configurations supported by funnel charts are as follows.


|Configuration ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Classification field |Specify fields for data classification, multiple fields can be selected. |
||Value |Specify the field used to display numeric values. |
||Maximum classification limit |Specify the maximum number of categories for the classification field. When the number of different values in the classification field exceeds the maximum number of categories, the system will display the first N values.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An excessive number of categories can cause the page to lag.</div><br> |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


&nbsp;
