---
title: "In-Text Grouping (Segmentation Filtering)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/In-Text_Grouping_Segmentation_Filtering"
---

<span id="_1-名词解释"></span>
# 1. Explanation of terms

In\-text grouping is also user grouping. There are two major differences from the ordinary subgroup:


* **One is the interaction path.**  You can use it directly in the Advanced Analytics Features \- Segmentation Filtering module without having to jump to the User Segmentation feature to create a subgroup, and then jump to the Analytics page for a second selection.

* **The second is the way to inquire.**  The results of grouping in the text are carried out simultaneously with each query, which can ensure the flexibility of the query and the real\-time performance of the results, while ordinary grouping can only achieve a single query or a daily routine query at present.


<span id="_2-使用方式"></span>
# 2. How to use

Enter advanced analysis, use segmentation filtering, select what users have done, and then circle the population through behavioral events.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4df21ad7749471e95489fc4fc4d1a36~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-当前支持的分析模型范围"></span>
# 3. The range of currently supported analytical models


|**Advanced Analytical Model** |**support** |
|---|---|
|Event analysis |✔️ |
|Custom Retention |✔️ |
|Funnel Analysis |✔️ |
|Distribution analysis |✔️ |
|User Component |✔️ |
|User Path |✔️ |
|Attribution Analysis |✔️ |
|User Lifecycle |✔️ |
|Heat Map Analysis |❌ |
|LTV Analysis |✔️ |
|Business Object Analysis |❌ |


<span id="_4-功能详解"></span>
# 4. Detailed functional explanation

The common use cases for grouping within a text can be classified into two categories:


* **One is to use a static population**, the calculation of the population is a population that meets certain conditions within a "fixed time range", and the query results are fixed.

* **One is to use dynamic crowds**, the calculation of crowds can query the crowds that meet certain conditions in real time for "each calculation interval", and match with the events corresponding to the time granularity, so as to achieve dynamic matching of grouping results. Taking the day\-level line chart as an example, each day is a query interval. Among them: past 0 days \- past 0 days, representing the data of the day of calculation; past 1 day \- past 1 day, representing the data of the previous day of calculation; past 7 days \- past 1 day, representing the data of the past 7 days (excluding today); the same is true for other granularities.


For the first category, behavioral circling is generally used. For example, according to the configuration of the following figure, you can circle users who have opened the application within a fixed time frame (2023.09.07 \- 2023.09.13) and visited at least two or more pages:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aba761136dc4652a432d21795ab06c5~tplv-goo7wpa0wc-image.image) </span>

For the second category, dynamic circling is generally used. For example, according to the configuration method of the following figure, assuming that the query granularity is selected at the day level, users who have opened the application on the same day and visited at least two or more pages can be matched every day:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c17b118c65ca456f87487a0a361eaab7~tplv-goo7wpa0wc-image.image) </span>

If you have configured a daily routine crowd calculation task in the user grouping module, you can also directly choose to refer to the historical results that have been calculated by the user grouping and match them according to the date of the event. As shown in the figure below, the results of the "highly active population" calculated in the cluster the day after the events participating in the analysis were matched can be achieved:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e488432547244609ad857c923e4da10~tplv-goo7wpa0wc-image.image) </span>

If you only need the historical calculation results of a certain day of the crowd to filter, you can modify the grouping calculation method in the attribute filter\-user grouping to achieve global matching according to the specified date of a certain day.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c13b22395c54148baf0d4f94cd78918~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-使用案例举例"></span>
# 5. Examples of use cases


|Common scenario examples |Configuration method |
|---|---|
|Repurchase users (daily level): Purchases made on the same day and more than two purchases made in the past 90 days |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71f1b43950454332a2e1dc9384532e13~tplv-goo7wpa0wc-image.image) </span> |
|Repurchase users (weekly level): Purchases have occurred in the past week, and at least 2 purchases have occurred in the previous month (in the past 4 weeks) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/698cafcb741b418ca7fb48acf0c7ca2a~tplv-goo7wpa0wc-image.image) </span> |
|Sleeping User Activation: Users who have purchased through App Store channels that day but have not been active in the past 180 days |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19a7f029ad384e46b54a9870d679701d~tplv-goo7wpa0wc-image.image) </span> |
