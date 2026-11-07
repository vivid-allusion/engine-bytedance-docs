---
title: "Common Functions Usage"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Common_Functions_Usage"
---

<span id="_1-统计一个字符串的某个指定字符出现次数"></span>
# 1. Count the number of occurrences of a specified character in a string

**Function used**: length(extractAll(target_str, char))

**Explanation**: target_str is the target string to be counted, and char is the specified string

**Example**: Given the string "aaabc", to count the number of times the character "b" appears, you can use the countif function in Excel,

Here, you can **write it like this**: length(extractAll('aaabc', 'b'))

The returned result is a numeric value; in this case, the result is 1

<span id="_2-表计算函数"></span>
# 2. Table calculation functions

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Table calculation expressions can only be used as metrics in the product.</div>


* <div data-tips="true" data-tips-type="warning">The dimension specified in along must exist in the query panel, otherwise an error will occur.</div>



<span id="_2-1-计算总额百分比"></span>
## 2.1 Calculate the percentage of the total amount

**Function**: TOTAL( ) along ( )

**Meaning:**  Calculate the total value of the metric based on the dimension. This function is typically used in scenarios where the percentage of the total amount needs to be calculated.

In the following example, the function is used to calculate the total payment amount for each province based on the province dimension. This prepares for the subsequent calculation of the proportion of [payment amount for each city] to [total payment amount for the province].

**Function example:**  TOTAL(sum([Payment Amount])) along([City]), which calculates the total payment amount for all cities. As shown in the figure, when there are other dimensions (such as province) in the chart, the total payment amount for all cities under each province is calculated.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e30927f0a7dd4a72b4b1e87d125f5f6a~tplv-goo7wpa0wc-image.image) </span>

**Percentage of total amount**: Taking the above example, calculating *sum([Payment Amount])/TOTAL(sum([Payment Amount])) along([City])*  yields the proportion of each city's total payment amount to the province's total payment amount.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0edec69d033449086da3ad9e9296f39~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-依据维度滚动求和"></span>
## 2.2 Rolling sum by dimension

**Function:**  RUNNING_SUM( ) along( )

**Meaning:**  Rolling sum by dimension

**Example:**  RUNNING_SUM(sum([Payment Amount])) along([City]), which performs a rolling sum by city. As shown in the figure, 118,578 is the sum of the payment amounts for Lincang and Lijiang, and 174,599 is the sum for Lincang, Lijiang, and Baoshan. When there are other dimensions (such as province) in the chart, the rolling sum of payment amounts for all cities under each province is calculated.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2579533d3524c63a17d4ce9f41cce22~tplv-goo7wpa0wc-image.image) </span>

**Extension:**  In addition to the RUNNING_SUM expression, you can also use RUNNING_AVG, RUNNING_MIN, and RUNNING_MAX to perform rolling calculations for average, minimum, and maximum values. Example: RUNNING_AVG(sum([Payment Amount])) along([City])

> This function cannot be searched, but it can be used directly


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2579533d3524c63a17d4ce9f41cce22~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-计算指标正序与倒序百分位"></span>
## 2.3 Calculate ascending and descending percentiles of a metric

**Function:**  RANK_PERCENTILE( , 'asc') along( )

**Meaning:**  Calculate the ascending percentile of the metric based on the dimension (replace asc with dsc to calculate the descending percentile)

**Example:**  RANK_PERCENTILE(sum([Payment Amount]),'asc') along([城市]), which calculates the percentile rank of each city's payment amount in ascending order. When there are other dimensions (such as province) in the chart, the percentile rank of each city's total payment amount is calculated within each province.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2013ef913f2040f185b2201b4dcb732d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-依据维度计算指标指定窗口内所有指标均值"></span>
## 2.4 Calculate the average of all metric values within a specified window based on a dimension

**Function:**  WINDOW_AVG( ,start,end) along( )

**Meaning:**  Window function. Based on the dimension, calculates the average of all metric values within the window from start to end. For example, if start is \-1 and end is 1, the function calculates the average of three values in the window from the previous to the next position along the dimension.

**Example:**  WINDOW_AVG(sum([Payment Amount]),\-1,1) along([Payment Date]), which calculates the average payment amount from the previous day to the next day for each payment date.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3251ae877a92422da8201c92ee79874e~tplv-goo7wpa0wc-image.image) </span>

**Extension:**  In addition to the WINDOW_AVG expression, you can also use WINDOW_SUM, WINDOW_MIN, and WINDOW_MAX for windowed sum, minimum, and maximum calculations.

**Common scenario:**  When viewing data trends with large fluctuations, use WINDOW_AVG to smooth the curve and serve as a trend line.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb347877c3fd497eb341ec06338b42a5~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-依据维度计算指标位置-偏移量的指标值"></span>
## 2.5 Calculate the metric value at the position plus offset based on a dimension

**Function:**  LOOKUP( , offset) along( )

**Meaning:**  Based on the dimension, retrieves the metric value at the current position plus the offset. For example, if the offset is \-1, it retrieves the metric value at the previous position.

**Example:**  LOOKUP(sum([Payment Amount]),\-1) along([Payment Date]), which displays the total payment amount for the previous day.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c3d33fb4b6d4636a575d29c6f7fc145~tplv-goo7wpa0wc-image.image) </span>
