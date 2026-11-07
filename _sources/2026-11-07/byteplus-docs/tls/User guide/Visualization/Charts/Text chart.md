---
title: "Text chart"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/markdown_chart"
---

TLS supports adding text charts in markdown format to the dashboard. This topic describes the configuration of chart parameters and markdown syntax of text chart.

<span id="595169c6"></span>
## Diagram Description

You can insert images, links, videos, text descriptions, and other elements into a text chart to expand the way information is presented in the dashboard. For example, you can add text elements such as chart descriptions, annotation information, and background information of the dashboard to make it easier for users to understand the data and indicators in the dashboard; you can add links to resources such as quick analysis, projects, and dashboards, so that users can quickly jump to other resource pages to further view information; you can add elements such as pictures and videos to more vividly display dashboard information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you configure a chart,read <a href="https://docs.byteplus.com/docs/tls/chart_overview#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9">Precautions</a>.</div>


<span id="71e23636"></span>
## General Configuration


|Configuration ||Description |
|---|---|---|
|Panel configuration |Title |Enter a title for the chart. |
||Show chart title bar |Specify whether to display the chart title on the dashboard. |
|Text Style |Chart Type |Specify the chart type. |


<span id="31d76f74"></span>
## Edit Markdown

You can add Markdown elements in the Markdown editor.

<span id="473d9530"></span>
## Add variables

TLS supports inserting query analysis results or dashboard variables into text chart in the form of variables, the format is `${{variable name}}`.


* When adding a query analysis result, you need to specify a specific result column name. If multiple values exist in the specified result column, TLS will take the first value in the current result data and insert it into the text chart.

* Before adding a dashboard variable, you need to create a dashboard variable. For detailed explanations about variables, please refer to [Add filters or variables to a dashboard](https://docs.byteplus.com/docs/tls/Adding_filters_to_a_dashboard).


The relevant steps are as follows:


1. Execute the query analysis operation.

   Here, you need to add a variable placeholder in the query analysis statement, the format is `${{variable name | default value}}`. The example is as follows:

   ```SQL
   * | SELECT DATE_FORMAT(__time__ - __time__ % ${{interval|60000}}, 'HH:mm:ss') AS time, COUNT(*) AS PV GROUP BY time ORDER BY time
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e68f8713d3a437594af003d0ef90287~tplv-goo7wpa0wc-image.image) </span>

2. Insert dashboard variables and query analysis result column variables in a text graph.

   For example, `${{interval}}`is the dashboard variable, and `${{time}}`and `${{PV}}`are the result column variables.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5e3de52c335457ca64a065cb1a8e20a~tplv-goo7wpa0wc-image.image) </span>

3. Click **Apply to dashboard** .

4. Filter variables to show different search results.

   * Select the **time interval** variable as 1000 and the text graph will show the number of visits in one second.

   * Select the **time interval** variable as 60000 and the text graph will show the number of visits in one minute.

   * Select the **time interval** variable as 360000 and the text graph will show the number of visits in one hour.


<span id="93cc1f82"></span>
## Common Markdown syntax


|Element |Syntax example |Display effect |
|---|---|---|
|Title |```Markdown```<br>```# First-level Heading```<br>```## Second-level Heading```<br>```### Third-level Heading```<br> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d09481fe772244669c8d83f1abbebee0~tplv-goo7wpa0wc-image.image) </span> |
|Link |```Markdown```<br>```Click [Statistical Charts](https://docs.byteplus.com/en/docs/tls/Statistics_chart) to view detailed explanations of the statistical charts.```<br> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4986667a58645d9a20390ce8c9dc925~tplv-goo7wpa0wc-image.image) </span> |
|Picture |```Markdown```<br>```![image](https://p3-starry.byteimg.com/tos-cn-i-p5uoocn1jn/47cd9f98a68f49399c1c8437f356a1cd~tplv-p5uoocn1jn-image.image "title")```<br> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abc2f34dd66f487c9f86f5d6f9d3e11f~tplv-goo7wpa0wc-image.image) </span> |
