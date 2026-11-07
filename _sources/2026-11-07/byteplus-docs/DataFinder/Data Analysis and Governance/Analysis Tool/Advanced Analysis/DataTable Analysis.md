---
title: "DataTable Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/DataTable_Analysis"
---

<span id="5595e625"></span>
# 1. Background information

<span id="11cb654f"></span>
## Application scenario

When we approach scenario\-based analysis, we need to comprehensively apply event analysis, retention analysis, and other metrics, and we need to simultaneously view multiple metrics, data performance in different dimensions, different segments, and other conditions, in order to better understand the business status.

For example, you need to see the difference between the performance of "active metrics, retention metrics, and conversion metrics" of "new and old client bases" in "different provinces and cities", and hope to do a separate drill for a "city dimension value" to further analyze the performance of personalized data under a certain city. At this time, you need to use the analysis ability of the metric DataTable.

<span id="c86eaf3b"></span>
## Precautions


* This function Saas is currently in the grey release, and privatization is selectively open. If you have any intention to open it, please contact the account manager.

* When using DataTable analysis, there are some differences between the calculation logic of the metric data and the calculation logic of the event analysis tool. Take the calculation scenario of the TOPN metric as an example. Please refer to the following [3. DataTable analysis index calculation logic example](https://docs.byteplus.com/docs/DataFinder/DataTable_Analysis#%E4%B8%89%E3%80%81%E5%A4%9A%E7%BB%B4%E8%A1%A8%E6%A0%BC%E5%88%86%E6%9E%90%E8%A7%86%E9%A2%91%E8%AE%B2%E8%A7%A3)sections.


<span id="二、功能界面介绍"></span>
# 2. Function interface introduction

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14a73398d23947929bb42b1a7f7bee49~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-功能入口"></span>
## 2.1 Function entrance

The path of the function entrance is: Top Guide Menu Bar Click **Analysis Tools** \> **Advanced Analysis** \> **DataTable Analysis**

<span id="_2-2-指标区"></span>
## 2.2 Metric area

The index area is mainly used to display the functions related to the addition, deletion, modification, relocation, and storage of metrics and metric columns;

<span id="_2-2-1-添加指标"></span>
### 2.2.1 Add metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/325a4752e8854a86aeda70e6c27da7aa~tplv-goo7wpa0wc-image.image) </span>


1. Click the **Add metrics** button to evoke the Add window; two metric modes are supported: select Event Quick Add, and select Saved metric to add.

   1. After selecting the event, the default operator is "total number of times". After the selection is completed, you can switch to other operators such as "total number of people" and "penetration rate";

   2. After selecting the metric, the previously saved metric is added.

2. Target metrics can be filtered according to event classification and event type to improve search efficiency.


<span id="_2-2-2-指标类型"></span>
### 2.2.2 Metric types


|**Metric type** |**Metric source** |**Support status** |
|---|---|---|
|Event metrics |Created and saved by "Event Analysis" |Privatization version 4.4 is supported |
|Event Combination Metrics |Created and saved by "Event Analysis \- Combination Metrics" |Privatization version 4.4 is supported |
|Retention metric |Created and saved by "Retention Analysis" |Privatization version 4.4 is supported |
|Conversion metric |Created and saved by Transformation Analysis |Not supported yet |


<span id="_2-2-3-添加指标过滤条件"></span>
### 2.2.3 Add metrics filter

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/503f7ce7ade140b0a418aa4323349f80~tplv-goo7wpa0wc-image.image) </span>


1. Click the **Add Filter** button to make further conditional filters for the current metrics to change the metric caliber and meet different analysis scenarios;

2. Filtering conditions support the use of "AND" and "OR" combination logic to meet complex filtering scenarios.


<span id="_2-2-4-保存指标"></span>
### 2.2.4 Save metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/161962a4238c443ba717825d099fdf2a~tplv-goo7wpa0wc-image.image) </span>

If the quick metric analysis of the event is directly selected, and it is judged that it is a long\-term use metric, then the metric can be saved, which is convenient for subsequent direct use and improves the efficiency of use.

<span id="_2-3-维度分组区"></span>
## 2.3 Dimensional grouping area

Dimension grouping area is mainly used to show dimension and dimension row add, filter, drill down and other functions;

<span id="_2-3-1-添加维度分组"></span>
### 2.3.1 Add dimension grouping

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cde07a8f679497d8a20b72649f09de1~tplv-goo7wpa0wc-image.image) </span>


1. If you need to perform multi\-dimensional analysis on metrics, you can add dimension grouping, such as multi\-dimensional viewing by province and city.

2. Dimension grouping currently supports adding up to 5 layers; note that the number of layers drilled under the dimension value is also counted in the total number of layers;


<span id="_2-3-2-维度值下钻"></span>
### 2.3.2 Dimension value drill down

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aadde573c57f4a7399b4429c57a1b888~tplv-goo7wpa0wc-image.image) </span>

You can drill down only for a certain dimension value to further disassemble and analyze a single dimension value. For example, only analyze the proportion of "new and old users" for users in the "Lujiazui" area.

<span id="_2-3-3-过滤维度值"></span>
### 2.3.3 Filter dimension value

If you need to focus on some dimension values, you can use the "dimension value filtering" ability to narrow the focus.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0ed87e1d81c43e48251b70d8f0a0793~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-细分筛选区"></span>
## 2.4 Subdivision screening area


1. If you need to compare the performance of metrics under different segments, you can use the "Segment Filter" function. Support direct filtering according to event attributes and user attributes, and can also make full use of the crowd screening ability of "in\-text grouping" to create crowd comparison;

2. The created subdivision filter will be displayed at the bottom of the metric row and displayed by column. By default, the leftmost column of the first metric is arranged in reverse order, and can be sorted by other columns;

3. After the configuration is completed, the subdivision filter area can be folded to widen the display space of the table area;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c4931ca09ba41ea8c3bac7cf7586c40~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-5-日期选择"></span>
## 2.5 Date selection

Currently, only two query granularities, day\-level and week\-level, are supported.

<span id="_2-6-下载"></span>
## 2.6 Downloads

Supports data download in Excel format.

<span id="_2-7-重置"></span>
## 2.7 Reset

Click the "Reset" button to clear the configured conditions.

<span id="_2-8-将结果保存到看板"></span>
## 2.8 Save the results to the Kanban board

It supports saving the query results to the Kanban board for daily observation, but does not support access to monitoring functions for the time being.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6224259b8b6841fc94947cc1bd6b23e7~tplv-goo7wpa0wc-image.image) </span>

<span id="三、多维表格分析视频讲解"></span>
# 3. DataTable analysis index calculation logic example

The following is a specific scenario for you to illustrate the differences between DataTable analysis in the TopN logic of calculating metrics and event analysis tools. The details of the example scenario are as follows:


* Applicable scenario: order analysis

* Analysis goal: Analyze the product details of the **purchase amount**  **++topN (within 50) ++** under a certain channel, that is, the total amount of successful payment of purchased products, the total number of successful payments, and the total number of successful supports.

* Comparison of metric configuration and calculation logic:

   
   |Segmentation |DataTable analysis |Event analysis |
   |---|---|---|
   |Analysis tool configuration example |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2af11d0335c447f5b50968c14844858d~tplv-goo7wpa0wc-image.image) </span><br><br>As depicted in the chart above, three metrics were added to the DataTable analysis:<br><br><br>* metric 1: Select the "Product Payment Successful" event and sum the events by the total payment amount (sum by goods_total_price)<br><br>* metric 2: Select the "Product Payment Successful" event, and ask the event to ask for PV.<br><br>* metric 3: Select the "Product Payment Successful" event and ask for the event to ask for UV.<br><br><br>At the same time, select "Product Name" for group conditions. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a79ce91e64dc49a48a0f13c7685df88a~tplv-goo7wpa0wc-image.image) </span><br><br>As depicted in the figure above, three metrics were added to the event analysis:<br><br><br>* metric 1: Select the "Product Payment Successful" event and sum the events by the total payment amount (sum by goods_total_price)<br><br>* metric 2: Select the "Product Payment Successful" event, and ask the event to ask for PV.<br><br>* metric 3: Select the "Product Payment Successful" event and ask for the event to ask for UV.<br><br><br>At the same time, select "Product Name" for the group conditions, and set the group display "Top 50 Items". |
   |TopN calculation logic of metrics |DataTable analysis tools:<br><br><br>1. The DataFinder takes the top N grouped by the selected grouped metric (default is the first metric).<br><br>   In the above example, metric 1 is grouped by product name and sorted in descending order, and the Top50 is displayed.<br><br>2. Then, based on the results of the first metric grouping, we can query the values of the other column metrics.<br><br><br>Example of query results:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df3e8fe742674994bd94bcb3c25cea6e~tplv-goo7wpa0wc-image.image) </span> |In the event analysis tool:<br><br>DataFinder groups each metric by top N, and then summarizes and aligns by the first metric.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5a8b5915e724b62b69b0614e8a9df2c~tplv-goo7wpa0wc-image.image) </span><br><br>Based on the above calculation logic, when querying using event analysis, there will be cases where some dimensions actually have data, but the query result is empty, such as metric 2 and metric 3 in the example. |
   |Difference point analysis/applicable scenario analysis |DataTable analysis is more suitable for grouping and sorting based on a certain metric, and then grouping query analysis based on the first metric. ||
   


<span id="1ad7f058"></span>
# 4. DataTable analysis video explanation

<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5cdda56cffd36ddb0c1a5f2436a5d4d.mp4" controls></video>
