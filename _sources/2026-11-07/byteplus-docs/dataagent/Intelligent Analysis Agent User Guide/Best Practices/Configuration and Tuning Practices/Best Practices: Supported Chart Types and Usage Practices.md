---
title: "Best Practices: Supported Chart Types and Usage Practices"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Best_Practices_Supported_Chart_Types_and_Usage_Practices"
---

When using the Intelligent Analysis Agent for data queries, the returned results support multiple chart types, including line charts, bar charts, pie charts, and more. You can specify the chart type for the returned results in your query according to your business data query scenario. This article introduces the currently supported chart types, their applicable scenarios, and example queries.

<span id="840f3041"></span>
# Supported chart types and usage recommendations

<span id="99c9af16"></span>
## line (line chart)


* Suitable for displaying data trends over time.

* Keywords: trend, growth, decline, fluctuation, time series.

* Example queries: Show annual sales revenue changes, display user growth trends.

* Diagram:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ffb47a65c65c4b4a9d9e6cf42e947ad5~tplv-goo7wpa0wc-image.image) </span>

<span id="0d05f85c"></span>
## column_parallel (bar chart)


* Suitable for comparing data across different categories.

* Keywords: comparison, ranking, category, quantity.

* Example queries: Compare sales revenue by region, display product sales rankings.

* Diagram:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91c9215c3d014677b07aa0f206b98020~tplv-goo7wpa0wc-image.image) </span>

<span id="73e26cb4"></span>
## pie (pie chart)


* Suitable for showing the proportion of each part to the whole.

* Keywords: proportion, percentage, distribution.

* Example queries: Display market share distribution, show user age group proportions.

* Diagram:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18f6f3bef93d44e799741c2dcccec91e~tplv-goo7wpa0wc-image.image) </span>

<span id="9c0f482e"></span>
## measure_card (metric card)


* Suitable for displaying a single key indicator or value.

* Keywords: key indicator, value, summary.

* Example queries: Show current sales revenue, display total number of users.

* Diagram:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d80f25983af4ea3bc0492f8023a53f8~tplv-goo7wpa0wc-image.image) </span>

<span id="10b3b7a7"></span>
## table (table)


* Suitable for presenting detailed data and supporting multidimensional views.

* Keywords: detail, detailed, multidimensional, list.

* Example queries: List sales data for each product, display detailed user information.

* Diagram:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0cb5d6849e143fb8ac290b6ad450b6c~tplv-goo7wpa0wc-image.image) </span>

<span id="880d214c"></span>
## scatter (scatter plot)


* Suitable for displaying correlations between fields. Best used when there are two indicators and for continuous data.

* Keywords: impact, performance, correlation, distribution, grouping.

* Example queries: Show the impact of sales revenue on sales revenue, display the distribution of age and income.

* Diagram:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d75f089a4da4889ac0482de692b9fd9~tplv-goo7wpa0wc-image.image) </span>

<span id="64489cbb"></span>
## map (China map)


* Suitable for displaying the distribution and differences of data across provinces in China.

* Keywords: regional distribution, geographic differences, regional comparison, geographic trends, heat map, marker points.

* Sample question: Display the distribution of sales amount across provinces.

* Diagram:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3563c1e514344cc49bafbeb554ad917a~tplv-goo7wpa0wc-image.image) </span>

<span id="0de3e643"></span>
## double_axis (dual\-axis chart)


* Suitable for displaying two sets of data with different units simultaneously. Suitable for use when chartFieldGroup consists of two groups.

* Keywords: dual axis, different units, comparison.

* Sample question: Display sales amount and profit margin, show temperature and precipitation.

* Diagram:

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e00b735021d74102916084496d34caa0~tplv-goo7wpa0wc-image.image" width="1582px" />   </div>
   


<span id="742e67f9"></span>
## combination (combination chart)


* Suitable for displaying multiple sets of different types of data simultaneously or emphasizing relationships between data; applicable to complex scenarios. Suitable for use when chartFieldGroup consists of two or more groups.

* Keywords: combination, complex, multidimensional.

* Sample question: Display the trend and proportion of sales amount and profit.

* Diagram:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ced0f2b3233040c1bf9d58ae6d7b889a~tplv-goo7wpa0wc-image.image) </span>

<span id="c837ba1f"></span>
# Frequently asked questions

<span id="84cf8d5e"></span>
## How to specify the chart type in the query result?

You can specify it directly in the query, such as "Top 10 countries by sales amount, displayed as indicator cards." (Currently, "Prompt configuration" in the agent backend is not supported)

<span id="1ffd4b49"></span>
## Why is the expected chart type A, but the final rendering is chart type B?

If the current data and fields are not appropriate, the expected chart type cannot be rendered. For example:


1. **When the number of dimension and measure fields recalled by SQL does not meet expectations**

   For example: A pie chart cannot display "product", "sales amount", and "profit" simultaneously. This is because a pie chart can only accept one measure for size mapping, such as "sales amount".

   
   |Chart types |Dimension (dimension) |Measure (measure) |Description |
   |---|---|---|---|
   |Line chart |[1,10] |[1,10] |A line chart requires at least one dimension (as the X axis) and one measure (as the Y axis). |
   |Bar chart |[1,10] |[1,10] |A bar chart requires at least one dimension (as the X axis) and one measure (as the Y axis). |
   |Pie chart |[1,1] |[1,1] |A pie chart only accepts one dimension (as the name) and one measure (as the size). |
   |Indicator card |[0,1] |[1,8] |Indicator cards can accept only one dimension (as core information) and multiple metrics (as supplementary information). |
   |Table |/ |/ |Tables have no restrictions on dimensions or metrics. |
   |Scatter plot |[0,100] |[2,4] |Scatter plots have no restrictions on dimensions. At least two metrics are required (as X\-axis and Y\-axis), and up to four metrics can be used (the third as color, the fourth as size). |
   |China map |[1,1] |[1,1] |The China map accepts only one dimension (as province) and one metric (as color). |
   |Dual\-axis chart |[1,1] |[2,10] |Dual\-axis charts accept only one dimension (as X\-axis) and require at least two metrics (for the left and right Y\-axes). |
   |Dual\-axis chart |[1,1] |[2,10] |Dual\-axis charts accept only one dimension (as X\-axis) and require at least two metrics (for the upper and lower Y\-axes). |
   

2. Due to differences in chart presentation, **If the user does not explicitly specify the chart type, other chart types may be used for better effect when there are too many or too few entries.** 

   For example: If a pie chart displays 300 slices, the large amount of data makes the pie chart barely readable, so unless explicitly specified, a pie chart will not be used by default in such scenarios.

   
   |Chart type |Recommended maximum rendering quantity |Note |
   |---|---|---|
   |Line chart |366 |Line charts are suitable for rendering 366 points (covering a full year of detailed data). Rendering more points results in severe crowding and low readability, making tables preferable. |
   |Bar chart |181 |Bar charts are suitable for rendering 181 bars (covering half a year of detailed data). Rendering more bars results in severe crowding and low readability, making tables preferable. |
   |Pie chart |181 |Pie charts are suitable for rendering 181 sectors (covering half a year of detailed data). Rendering more sectors results in severe crowding and low readability, making tables preferable. |
   |Indicator card |20 |Indicator cards are suitable for rendering 20 indicator blocks. Rendering more blocks results in a lack of key information and low readability, making tables preferable. |
   |Scatter plot |1000 |Scatter plots are suitable for rendering 1000 scatter points. Rendering more points results in severe crowding and low readability, making tables preferable. |
   |China map |34 |The China map can display up to 34 regions (corresponding to the 34 primary administrative divisions in China). There are no cases where more than 34 regions are displayed. |
   |Dual\-axis chart |181 |Dual\-axis charts are suitable for rendering 181 points (covering half a year of detailed data). Rendering more points results in severe crowding and low readability, making tables preferable. |
   |Dual\-axis chart |181 |Dual\-axis charts are suitable for rendering 181 bars (covering half a year of detailed data). Rendering more bars results in severe crowding and low readability, making tables preferable. |
   |Table |No limit |Tables have no rendering limit. |
