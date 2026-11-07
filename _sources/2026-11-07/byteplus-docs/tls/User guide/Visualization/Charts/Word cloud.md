---
title: "Word cloud"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Word-cloud"
---

TLS supports word cloud charts for displaying query and analysis results. This topic describes how to create a word cloud chart.

<span id="81d68d79"></span>
## Chart description

A word cloud is a visual representation that displays words from the data in different sizes and colors, forming a cloud\-like shape, to achieve the purpose of visualization. In a word cloud, the more frequently a word appears, the larger its font size will be, effectively highlighting the key information in the data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart, read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="d80224af"></span>
## Common settings

Configure the global settings that apply to the entire chart. The basic settings of a word cloud chart are as follows:


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |Entry |Select the field used to represent the terms. |
||Entry size |Select the field used to represent the numerical information for each term. |
|Data configuration |Number of terms |Specify the number of entries. |
|word cloud style |Font style |Specify the font for the entry. |
||Font size |Specify the font size of the entry. |
|Color Configuration |Color scheme |Specify the color of the word cloud chart.<br><br><br>* **Built\-in**: Display the items according to the built\-in color scheme.<br><br>* **Monochrome**: Display the items in the color you have chosen.<br><br>* **Threshold**: After specifying the threshold point and color, if the actual value exceeds this threshold point, it will be displayed in the corresponding color. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="c8f43315"></span>
## Drill\-down events

TLS supports drill\-down events for implementing interactions among the charts on a dashboard. After you configure a drill\-down event, the drill\-down action is triggered when you click the specified field on the dashboard. The following types of drill\-down events are supported: **Open topic**, **Open dashboard**, and **Custom HTTP links**. For more information on drill\-down events, refer to [Drill-down events](https://docs.byteplus.com/docs/tls/Drill-down_events).

For example, if you set the interaction event of the `reqid` field to open a log topic, then by clicking on the `reqid` field value in the statistics chart and selecting **Open topic**, the page will automatically redirect you to the log topic you have set.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a4a87a6217542a4b5db1d0b796f1b9f~tplv-goo7wpa0wc-image.image) </span>

<span id="a0bac068"></span>
## Example

Display the request ID with the longer request time through the word cloud.


* Query and analysis statement

   ```SQL
   * | select * reqid, reqtime
   ```
   

* Common configuration

   * **Entry** : Specify as `reqid`. Where `reqid` represents the request ID.

   * **Entry size** : Specify as `reqtime`. Where `reqtime` is the request time.

* Statistical chart

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d575990413e043238c11f0ab7e124896~tplv-goo7wpa0wc-image.image) </span>
