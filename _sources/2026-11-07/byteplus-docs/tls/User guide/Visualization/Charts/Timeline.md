---
title: "Timeline"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Timeline"
---

Torch Log Service (TLS) supports timeline charts for displaying query and analysis results. This topic describes how to create a timeline chart.

<span id="0095946e"></span>
## Chart description

A timeline chart displays a series of events in chronological order. You can view the time when each event occurs and the order of the events in the timeline chart. Timeline charts are suitable for scenarios such as displaying product updates, event tracking, and memorabilia.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="e6c50996"></span>
## Common settings


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Main field |Select the field that you want to display in the timeline. In most cases, specify the field that specifies time. |
||Time field |Select the fields that you want to display in the timeline chart. You can select multiple fields. |
||Tooltip field |Select the fields that you want to display in prompts. When you move the pointer over a point in the timeline, the selected fields are displayed by default. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Timeline style |Display method |Specify whether to enable the alternate mode for displaying the time value and the selected fields. |
||Paging size |Select the number of events that you want to display in the timeline chart. |
|Color configuration |Color scheme |Set the color of the timeline.<br><br><br>* **Monochrome**: displays the color you have chosen.<br><br>* **Defined by threshold**: after specifying the threshold point and color, if the actual value exceeds this threshold point, it will be displayed in the corresponding color. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="72fa2117"></span>
## Example

Use a timeline chart to display the request count of each day.


* Sample query statement:

   ```SQL
   * | SELECT date_format(__time__, 'Y-M-d') AS time ,SUM(if(Method='GET',1,0)) as GET, SUM(if(Method='POST',1,0)) as POST group by time order by time
   ```
   

* Chart configurations:

   * **Time field**: In this example, `time` is specified as the field displayed in the timeline. `time` is the alias of the time field. In the SQL statement, `date_format(__time__, 'Y-M-d')` specifies that the aggregation dimension is one day.

   * **Main field**: In the SQL statement, `SUM(if(Method='GET',1,0)) as GET` is used to specify the statistics of GET requests, and `SUM(if(Method='POST',1,0)) as POST` is used to specify the statistics of POST requests.

* Sample chart:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cad6fc831e54490da000931d936c8622~tplv-goo7wpa0wc-image.image) </span>
