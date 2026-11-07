---
title: "Sankey diagram"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Sankey-diagram"
---

Torch Log Service (TLS) supports sankey diagrams for displaying query and analysis results. This topic describes how to create a sankey diagram.

<span id="3192c194"></span>
## Chart description

A sankey diagram is a specific type of flowchart used to illustrate the flow of a series of values from the initial source to the final destination.

The key characteristics of Sankey diagrams are as follows:


* Flow visualization: Represents the flow of data from one node to another using directed lines.

* Width coding: The width of the line is scaled according to the amount of flow they represent, visually indicating the relative quantities between different flow channels.

* Resource conservation: Ideally, the sum of all the traffic flowing into a node is equal to the sum of the traffic flowing out of that node.

* Multi\-level branching: Suitable for displaying the multi\-stage input, processing, transformation, and output processes in complex systems, with a clear display of the distribution and loss of each stage.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="a28e2dec"></span>
## common configuration


|Parameter ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Query and analysis field |starting point |Select the field representing the starting node. |
||Terminal vertex |Select the field representing the destination node. |
||conversion value |A field that counts traffic values between the starting and ending nodes. |
|Standard configuration |Format |Specify the unit to which you want to convert the numeric values in the specified fields. |
||Preserve decimal point |Specify the decimal places of the numeric values. |
||Unit |Specify the custom unit of the numeric values of the specified fields. |
|Color Configuration |Color scheme |Sets the color of the Sankey diagram.<br><br><br>* **Built\-in** : Display the lines according to the built\-in color scheme.<br><br>* **Monochrome** : Display the lines in the color you have chosen.<br><br>* **Threshold** : After specifying the threshold point and color, if the actual value exceeds this threshold point, it will be displayed in the corresponding color. |
|Link ||Support adding additional links to enrich chart information.<br><br>After setting, the link icon will be displayed in the upper left corner of the chart, and you can click the link icon to view the link content. |


<span id="d0cb975e"></span>
## Example

The Sankey diagram shows the traffic relationship between different `sources`and `targets`and the size of the traffic.


* Query and analysis statement

   ```SQL
   *| select sum(streamValue) as streamValue, source, target group by source, target
   ```
   

* Chart settings

   * **Starting point** : Specify as `source`.

   * **Terminal vertex** : Specify as `target`.

   * **Conversion value** : Specify as `streamValue`, which is calculated using the sum of `streamValue`.

* Statistical chart

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17b39f0385bc4fd0975e729647495098~tplv-goo7wpa0wc-image.image) </span>
