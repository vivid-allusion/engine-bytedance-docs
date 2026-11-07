---
title: "Table Calculation"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Table_Calculation"
---

<span id="_1-概述"></span>
# 1. Overview

Sometimes, charts created using dimension and metric fields are not sufficient to support deeper analytical needs. Table calculations allow for further computation and analysis of displayed charts to support more use cases.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-表格-透视表表计算"></span>
## 2.1 Table calculations for tables and pivot tables

**Step 1:**  Select the type of calculation to analyze, such as percentage of total. Each analysis type will be described in detail in the feature overview.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10effa188f2a45cab5fdd2d24c56c3cc~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Confirm the metric to be calculated. Table calculations must be performed on a single metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97cd688b2beb4e4fa325b55061a10f30~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  Determine the calculation area and addressing direction to define the calculation range and direction.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39770b2570ad4442b1034ef3f8fea708~tplv-goo7wpa0wc-image.image) </span>

**Step 4:**  Using percentage of total for the entire table as an example, click Apply to generate the calculation result. The percentage of total creates a virtual field in the metrics column, showing the proportion of each item in the entire table. You can click to adjust the field name, format, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd2add0d76694dffbe1826072d092fa8~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-图表的表计算"></span>
## 2.2 Table calculations for charts

**Step 1:**  Select the type of analysis calculation, such as summary, and then select sum.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14d7ee0f453944b692f42cf00ae75a5a~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Confirm the metric to be calculated.

**Step 3:**  Confirm the calculation area and addressing direction. If the calculation area is the legend, the calculation is performed on the metric values represented by the bars on the horizontal axis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d633402eac94fdcbc03c27cc94de706~tplv-goo7wpa0wc-image.image) </span>

**Step 4:**  Click Apply to generate the calculation result. For example, when using summary sum, a table calculation field is generated to show the cumulative sum of the metric up to each item.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9fad4af5e8d4590a70d325bf4c68eb0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-计算类型"></span>
## 3.1 Calculation types

<span id="_3-1-1-差异"></span>
### 3.1.1 Difference

**Result:**  Calculates the difference in the value of the same metric across different dimension items. Supports calculating the difference based on the first/last item in the selected area or the previous/next calculation unit, and supports horizontal or vertical comparison calculations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe43ae8e494e4d60b12d121b01a82bb5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-相对于"></span>
### 3.1.2 Relative to

**Result:**  Compares the current value with the first, last, previous, or next item in the calculation area.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6052326a78aa47a897b9ea4d345e3e49~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-3-差异百分比"></span>
### 3.1.3 Difference percentage

**Result:**  Calculate the percentage difference of the same indicator value across different dimension items. Supports calculating the difference based on the first or last item in the selected area, or the previous or next calculation unit, and supports horizontal and vertical comparisons.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbb91957471f4d70954a65a01c14ee5f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-4-总额百分比"></span>
### 3.1.4 Total percentage

**Result:**  Calculate the proportion of the indicator value to the total indicator value within the selected calculation area. The indicator percentage can be calculated by column, row, entire table, or by dimension partitions. When the calculation type is total percentage, the reference direction is not meaningful.

As shown in the figure, by calculating the total percentage by partition, the payment amount percentage for each order type under each secondary channel within each primary channel can be obtained.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/136d2110d498495a9591ea12723743d6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-5-汇总"></span>
### 3.1.5 Cumulative value

**Result:**  Sequentially calculate the cumulative value of the indicator within the selected calculation area. Supports four calculation types: sum, average, maximum, and minimum.

As shown in the figure, calculating the cumulative sum by column yields the daily cumulative payment amount for each order type in January.

Taking the figure below as an example, after applying the calculation, the results are D=A+B and E=A+B+C.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74c93889933048869fb55a5ea29066e6~tplv-goo7wpa0wc-image.image) </span>

In the chart, the cumulative payment amount for each day can also be visually displayed by showing the cumulative sum.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34f423b934c749f3bcb7f025839db29d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-6-百分位"></span>
### 3.1.6 Percentile

**Result:**  Display the percentile value of the indicator within the selected area. If ascending order is set, the maximum value is at the 100th percentile; if descending order is set, the minimum value is at the 100th percentile.

As shown in the figure, calculating the percentile of the indicator value by column gives the percentile of the payment amount for each secondary channel under each order type.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4481f4ec9df24d61bd11ffb2a907c197~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-7-排名"></span>
### 3.1.7 Ranking

**Result:**  Rank the indicator within the selected area.

As shown in the figure below, in ascending order, the city with the lowest payment amount is ranked first, while in descending order, the city with the highest payment amount is ranked first.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d847f998112410bb0900e1103ed76c9~tplv-goo7wpa0wc-image.image) </span>

In the chart, you can also view the daily ranking changes of orders in each status by checking their rankings. At this point, set the calculation unit to the dimension axis scale, meaning to calculate the ranking for each data point on each axis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5de1448c60a5497b9934f87cfb676a8c~tplv-goo7wpa0wc-image.image) </span>

**When indicator values are equal**

**Competitive ranking:**  When indicator values are equal, the items share the top rank. This method is commonly used.

As shown in the figure, Wuxi and Xuzhou are tied for 6th place, Shantou and Foshan are tied for 8th place.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51fb7e6c4f134771aaaf7a6799b55b35~tplv-goo7wpa0wc-image.image) </span>

**Adjusted competitive ranking:**  When indicator values are equal, the items share the lowest rank.

As shown in the figure, Wuxi and Xuzhou are tied for 7th place, Shantou and Foshan are tied for 9th place.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3ae91054d0f4515ac7d81b920c8ce82~tplv-goo7wpa0wc-image.image) </span>

**Dense ranking:**  When indicator values are equal, the items share the top rank, and subsequent rankings continue in order according to the ranking value, regardless of the number of items sharing the rank.

As shown in the figure, Wuxi and Xuzhou are tied for 6th place, Shantou and Foshan are tied for 7th place.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5dc463e080a45abb9a609e534f92002~tplv-goo7wpa0wc-image.image) </span>

**Unique ranking:**  Each item is assigned a unique ranking. Even if the indicator values are the same, the rankings will differ.

As shown in the figure, Wuxi and Xuzhou have the same payment amount, Shantou and Foshan have the same payment amount, but their rankings are different.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6097597366074e4496a2bf6ec013f6bd~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-8-移动计算"></span>
### 3.1.8 Moving calculation

**Result:**  For each indicator value within the selected area, perform interval calculations.

As shown in the figure, the moving calculation computes the average of the previous, current, and next values, resulting in A1 being the average of B, C, and D; for data at the ends of the table, such as A2, since there is no previous value, the result is the average of B and C. Four calculation methods are supported: sum, average, maximum, and minimum.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88a451c0efad40c7969925bf2013d80a~tplv-goo7wpa0wc-image.image) </span>

In the chart, you can also use moving calculation to compute the average value of the most recent 30 days for each day.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb6686e62b2d45c0a8f663ba65ae5dc2~tplv-goo7wpa0wc-image.image) </span>

After obtaining the curve of the most recent 30\-day average, click the original indicator capsule to hide the field. In this way, you can also smooth out the fluctuations in the indicator changes throughout the year and obtain a more intuitive trend change.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f9a11873c524de2aa131b94bf3842eb~tplv-goo7wpa0wc-image.image) </span>

**Window**

This refers to the calculation window for the indicator's moving calculation. After configuring the window, the sum, average, maximum, or minimum of each metric from the nth previous to the nth subsequent value will be calculated.

<span id="_3-2-单位计算区域与寻址方向"></span>
## 3.2 Unit calculation region and addressing direction

<span id="_3-2-1-单列-单行"></span>
### 3.2.1 Single column/single row

Calculations are performed by column or by row, and recalculated separately for each column or row, as shown in the figure.

At this time, the addressing direction only supports downward or rightward.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94972c04b26d445c875cfb3a214bd01a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-整张表"></span>
### 3.2.2 Entire table

Table calculations are performed on the metric across the entire table, and the addressing direction can be set to downward then traverse or traverse then downward.

Taking downward then traverse as an example, the calculation direction is as shown in the figure below. According to the configuration in the figure, A1 = C \- B, A2 = D \- C

<span id="_3-2-3-区"></span>
### 3.2.3 Region

The calculation region is grouped by configuring column depth and row depth.

As shown in the figure below, to calculate the proportion of payment amount for each secondary channel under each primary channel and order type, the table region needs to be partitioned by primary channel and order type, and then the metric proportion is calculated within each region. Therefore, select the table calculation type as total percentage, and set the unit calculation region to region.

**Row and column depth are selected according to partition dimensions**: In this case, the calculation region needs to be divided by **primary channel (the first row dimension)**  and **order type (the first column dimension)** , so both row depth and column depth are set to 1. Click Apply to obtain the result.

The sum of the percentages in each yellow block in the figure below is 100%.

**How to understand column depth and row depth?** 

**Column depth:**  Determines the column dimension used for partitioning. If column depth is 0, no grouping is performed by column dimension; if column depth is 1, grouping is performed by the first column dimension; if column depth is 2, grouping is performed by the second column dimension, and so on.

**Row depth:**  Determines the row dimension used for partitioning. If row depth is 0, no grouping is performed by row dimension; if row depth is 1, grouping is performed by the first row dimension; if row depth is 2, grouping is performed by the second row dimension, and so on.

After selecting different columns and row depths, the table will highlight one unit calculation region in yellow to help with understanding and reference.

<span id="_3-3-二次表计算"></span>
## 3.3 Secondary table calculation

Starting from version V2.58.0, "Table Calculation" supports the secondary table calculation feature. Users can configure a table calculation again based on the results of the current table calculation after the initial configuration. The specific configuration includes: calculation type, reference field, unit calculation area, addressing direction, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a1a0de943784610aaf5de23c6d8685c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-快速表计算"></span>
## 3.4 Quick table calculation

 **(1) Operation path**

For the "7\-day moving average" in the table calculation feature, the system supports quick configuration. You can use **Quick Table Calculation** to increase efficiency. The operation path is as follows:

**Step 1**: Configure the relevant metrics on the visual query page.

**Step 2**: Click the dropdown button on the left side of the metric dimension.

**Step 3**: Click Quick Table Calculation \- 7\-day moving average.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/daa2fd9e13494ee08ebf165acb4381e1~tplv-goo7wpa0wc-image.image) </span>

 **(2) 7\-day moving average**

For the configuration of the 7\-day moving average, refer to the following steps:

**Operation condition**: There is a date field in the dimension bar.

**Step 1**: Click the "7\-day moving average" button.

**Step 2**: Add a table calculation configuration to the current metric and generate the corresponding derived metric capsule. Please refer to the following content to complete the configuration.


* Calculation type: Moving calculation. Average

* Window: 6 before, 0 after. Select "Show empty result if the number of window items is insufficient"

* Calculation metric: Current metric capsule

* Unit calculation area: The default value of "unit calculation area" when creating a table calculation in the current chart.

* Addressing direction: The default value of "addressing direction" when creating a table calculation in the current chart.

* Do not enable secondary table calculation.


 **(3) Special cases**

When using a pivot table for quick table calculation, if there is only one dimension in either the row or column, the same applies. Unlike the above default values, if the date dimension is in the row, the unit calculation area defaults to a single column; if the date dimension is in the column, the unit calculation area defaults to a single row.


|Table name |Dimension |Unit calculation area |Addressing direction |
|---|---|---|---|
|Table, detail table |There is only one date dimension |Single column |Vertically |
|Pivot table |The date field is the last field among the row and column dimensions.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f25c652b48734f749e2bdac60e558268~tplv-goo7wpa0wc-image.image) </span><br><br>If the date field is on the rows |Area<br><br>The column depth is equal to the number of column dimensions, and the row depth is equal to the number of row dimensions minus one. As shown in the left diagram: column 2, row 1. |Horizontally |
||If the date field is on the columns |Area chart<br><br>The row depth is equal to the number of row dimensions, and the column depth is equal to the number of column dimensions minus one. |Down |
|Column chart, bar chart, line chart, area chart |There is only one date dimension |Legend |Follows the chart default value |
||The first field is the date dimension |Legend |Follows the chart default value |
