---
title: "Description of Table Calculation Functions and Examples of Common Usage Scenarios"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Description_of_Table_Calculation_Functions_and_Examples_of_Common_Usage_Scenarios"
---

This article introduces several common expressions of table calculation functions and classic usage examples—Pareto chart. You can refer to these to build your own table calculation functions.

<span id="fbc6258b"></span>
# Usage scenarios

**Table calculation** refers to performing secondary calculations on already generated visualization charts. After summarizing the basic data, table calculation can be used to perform secondary computational processing on the data.

When secondary calculations are needed, table calculation can be used to omit steps such as downloading, exporting, and then processing again in Excel. For example, summing metric aggregates, moving calculations, and more.

The product currently supports configuring table calculations visually. In addition, you can also add fields and write table calculation functions to achieve this. This article will introduce table calculation functions. At the same time, it will introduce typical application scenarios of table calculation functions, the **Pareto chart**.

<span id="85cb680d"></span>
# Common expressions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Table calculation expressions can only be applied as metrics.</div>


* <div data-tips="true" data-tips-type="tip">The dimension for along must exist in the query panel, otherwise an error will occur.</div>



<span id="d8e937ed"></span>
## TOTAL() along ()

**Meaning**: Calculate the total of the metric based on the dimension. This function is typically used in scenarios where the percentage of the total is calculated.

In the following example, the function is used to calculate the total payment amount for each province based on the province dimension. This prepares for the subsequent calculation of the proportion of [payment amount for each city] to [total payment amount for the province].

**Function example**: `TOTAL(sum([payment amount])) along([city])`, which calculates the total payment amount for all cities. As shown in the figure, when other dimensions (provinces) exist in the chart, the total payment amount for all cities under each province is calculated.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfcf83621ba34eb6a7ab3788ddeeaffa~tplv-goo7wpa0wc-image.image) </span>

**Percentage of total**: Taking the above example, calculating `sum([payment amount])/TOTAL(sum([payment amount])) along([city])` yields the proportion of each city's total payment amount to the province's total payment amount.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b89001518671446695cb927a075494c8~tplv-goo7wpa0wc-image.image) </span>

<span id="1ad8a381"></span>
## RUNNING_SUM() along()

**Meaning**: Rolling sum based on the dimension

**Example**: `RUNNING_SUM(sum([payment amount])) along([city])`, which calculates the rolling sum based on cities. As shown in the figure, 118,578 is the sum of payment amounts for Lincang and Lijiang, and 174,599 is the sum of payment amounts for Lincang, Lijiang, and Baoshan. When other dimensions (such as provinces) are present in the chart, calculate the rolling sum of payment amounts for all cities under each province.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a25b91256d74101822ea041b267aab3~tplv-goo7wpa0wc-image.image) </span>

**Extension**: In addition to the RUNNING_SUM expression, you can also use RUNNING_AVG, RUNNING_MIN, and RUNNING_MAX to calculate the rolling average, minimum, or maximum values. Example: `RUNNING_AVG(sum([Payment Amount])) along([City])`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04494e70ebd340b19ad3bf180c0b2c9d~tplv-goo7wpa0wc-image.image) </span>

<span id="70bbec6e"></span>
## RANK(,'asc'/'desc') along()

**Meaning**:

Returns the unique rank of the current row within the partition. Assigns the same rank to identical values, allowing for ties.

Use the optional "asc" or "desc" parameter to specify ascending or descending order. The default is descending order.

**Example**:

`RANK(sum([Profit]), 'asc') along([Region])` Using this function, you can rank the sum of profits by region in ascending order. Tied ranks are allowed and skipped accordingly. If the sales amounts are (6, 7, 7, 9), the ranking results are (1, 2, 2, 4).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e84a5fef14a488a8f2f6583806e7b40~tplv-goo7wpa0wc-image.image) </span>

The query results are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbb6ca3103f34c2a89911edff8caace9~tplv-goo7wpa0wc-image.image) </span>

<span id="a1d4b458"></span>
## RANK_PERCENTILE(,'asc') along()

**Meaning**: Calculates the percentile rank of the metric in ascending order based on the dimension (replace asc with desc to calculate in descending order).

**Example**: `RANK_PERCENTILE(sum([Payment Amount]),'asc') along([City])` This calculates the percentile rank of each city's payment amount from lowest to highest. When other dimensions (such as provinces) are present in the chart, calculate the percentile rank of each city's total payment amount under each province.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91c31867c6164df6968fce4f1fa9fbea~tplv-goo7wpa0wc-image.image) </span>

<span id="80caf81b"></span>
## WINDOW_AVG(,start,end) along()

**Meaning**: Window function. Calculates the average of the metric values within the window from start to end along the dimension. For example, if start is \-1 and end is 1, the average of the three values from the previous to the next position along the dimension is calculated.

**Example**: `WINDOW_AVG(sum([Payment Amount]),-1,1) along([Payment Date])` This calculates the average payment amount from the previous day to the next day for each payment date.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8814fb77d80f49b29c41635617228105~tplv-goo7wpa0wc-image.image) </span>

product_type

**Extension**: In addition to the WINDOW_AVG expression, you can also use WINDOW_SUM, WINDOW_MIN, and WINDOW_MAX to calculate the sum, minimum, or maximum values within the window.

**Common scenario**: When viewing data trends with large fluctuations, use WINDOW_AVG to smooth the curve and serve as a trend line.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96a00681ce134ad58037c191c8eeee8e~tplv-goo7wpa0wc-image.image) </span>

<span id="38e16b10"></span>
## LOOKUP(, offset) along()

**Meaning**: Retrieves the metric value at the position of the current metric plus the offset along the dimension. For example, if the offset is \-1, the metric value from the previous position is retrieved.

**Example**: `LOOKUP(sum([Payment Amount]),-1) along([Payment Date])` displays the total payment amount from the previous day.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76a0a486a53d45819dda35d989fec176~tplv-goo7wpa0wc-image.image) </span>

<span id="32dc8edf"></span>
# Classic application

This section provides examples that cannot be directly implemented through the table calculation configuration in the analytics module and require the use of table calculation functions.

<span id="d25c2255"></span>
## Pareto chart

<span id="aaca0c60"></span>
### Sample result

The Pareto chart consists of a bar chart and a line chart. The bars display metric values in descending order, while the line shows the cumulative percentage. Using sales figures for each category as an example, a Pareto chart can be drawn to display the cumulative proportion of top product categories and identify key categories.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/842044bffad846b3a6bbee1cbb4da6f2~tplv-goo7wpa0wc-image.image) </span>

<span id="e25efad8"></span>
### Procedure


1. For a Pareto chart of sales by subcategory: Select the dual\-axis chart type, set subcategory as the dimension, sales as the primary axis, and create the subcategory\-sales chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71bae6fc7fb1487db294dfb7ba802e0e~tplv-goo7wpa0wc-image.image) </span>

2. Use the sorting feature in the analytics module to sort sales in descending order.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc58192041c14750a74c4f18cfd1e8b5~tplv-goo7wpa0wc-image.image) </span>

3. Create a cumulative proportion field with the expression: `running_sum(sum([Payment Amount])) along ([product_type])/total(sum([Payment Amount])) along ([product_type])`. This combines two table calculation functions. The running_sum function calculates the rolling sum of sales for each subcategory, divided by the total sales of all subcategories, resulting in the cumulative proportion up to each subcategory.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecdd67ecd1ab42beb9a6970c12002e9b~tplv-goo7wpa0wc-image.image) </span>

4. Drag the cumulative percentage field to the secondary axis of the metric to form the Pareto chart. You can use the chart configuration on the left to adjust the axis data format and change the secondary axis format to percentage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cbaa283b3734a3aa92e6ba8635a6cae~tplv-goo7wpa0wc-image.image) </span>
