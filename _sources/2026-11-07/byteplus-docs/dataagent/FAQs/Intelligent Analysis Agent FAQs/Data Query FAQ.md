---
title: "Data Query FAQ"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Query_FAQ"
---

<span id="caea5eb7"></span>
#### Question: How can data formatting be configured (such as prefix or number of decimal places)?

Answer: The formatting of the queried values is determined by the "data format" of the field in the "dataset". Users can modify this in "Data Preparation" \- "Dataset" \- "Edit Field" \- "Data Format".

The default is "**Automatic**", which intelligently adds thousand separators and retains 2 or 4 decimal places.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ed602dd1a4749029159e2edef030186~tplv-goo7wpa0wc-image.image) </span>

To change the default formatting, for example, to display `1.2324` as `$1.22`, simply modify the "Data Format" configuration for the corresponding field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9918f3064c5e4ef4bc6d761e556c9afe~tplv-goo7wpa0wc-image.image) </span>

<span id="e313ffad"></span>
#### Question: Why was chart A expected, but chart B was rendered instead?

Answer: If the fields (type and quantity) configured for the agent's data are not suitable and cannot support rendering the expected chart type, another chart type will be used for rendering. For detailed chart descriptions, see [Common chart analysis](https://docs.byteplus.com/docs/dataagent/Intelligent_Query_Agent#c0c24df5).


* When the number of **dimension and measure fields** recalled by SQL does not meet expectations.

   For example: a pie chart cannot simultaneously display "Product", "Sales", and "Profit". This is because a pie chart can only accept one measure for size mapping, such as "Sales".

   
   |Chart type |Dimension |Measure |Description |
   |---|---|---|---|
   |Line chart |[1,10] |[1,10] |A line chart requires at least one dimension (as the X axis) and one measure (as the Y axis). |
   |Bar chart |[1,10] |[1,10] |A bar chart requires at least one dimension (as the X axis) and one measure (as the Y axis). |
   |Pie chart |[1,1] |[1,1] |A pie chart only accepts one dimension (as the name) and one measure (as the size). |
   |Metric card |[0,1] |[1,8] |A metric card can accept at most one dimension (as the core information) and multiple measures (as auxiliary information). |
   |Table |/ |/ |A table has no restrictions on dimensions or measures. |
   |Scatter plot |[0,100] |[2,4] |A scatter plot has no limit on dimensions; it requires at least two measures (as the X and Y axes), and up to four measures (the third as color, the fourth as size). |
   |China map |[1,1] |[1,1] |The China map only accepts one dimension (as province) and one metric (as color). |
   |Dual\-axis chart |[1,1] |[2,10] |The dual\-axis chart only accepts one dimension (as X axis) and at least two metrics (as the left and right Y axes respectively). |
   |Combo chart |[1,1] |[2,10] |The combo chart only accepts one dimension (as X axis) and at least two metrics (as the upper and lower Y axes respectively). |
   

* Due to differences in chart presentation, **if the user does not explicitly specify the chart type, when there are too many or too few entries, another chart may be used for better effect.** 

   For example: if a pie chart displays 300 segments, the large amount of data makes the pie chart unreadable, so a pie chart will not be used in non\-mandatory scenarios.

   
   |Chart type |Recommended maximum rendering quantity |Note |
   |---|---|---|
   |Line chart |366 |The line chart is suitable for rendering 366 points (covering the scenario of one year of detailed data). When rendering more points, the chart becomes severely compressed and less readable, making tables preferable. |
   |Bar chart |181 |The bar chart is suitable for rendering 181 bars (covering the scenario of half a year of detailed data). When rendering more bars, the chart becomes severely compressed and less readable, making tables preferable. |
   |Pie chart |181 |The pie chart is suitable for rendering 181 sectors (covering the scenario of half a year of detailed data). When rendering more sectors, the chart becomes severely compressed and less readable, making tables preferable. |
   |Metric card |20 |The metric card is suitable for rendering 20 metric blocks. If there are more metric blocks, the key information is lost, readability is low, and tables are preferable. |
   |Scatter plot |1000 |The scatter plot is suitable for rendering 1000 scatter points. When rendering more points, the chart becomes severely compressed and less readable, making tables preferable. |
   |China map |34 |The China map can display up to 34 blocks (corresponding to the 34 primary administrative regions on the China map); there are no other applicable scenarios. |
   |Dual\-axis chart |181 |The dual\-axis chart is suitable for rendering 181 points (covering the scenario of half a year of detailed data). When rendering more points, the chart becomes severely compressed and less readable, making tables preferable. |
   |Combo chart |181 |The combo chart is suitable for rendering 181 bars (covering the scenario of half a year of detailed data). When rendering more bars, the chart becomes severely compressed and less readable, making tables preferable. |
   |Table |None |There is no limit to the number of items rendered in tables. |
