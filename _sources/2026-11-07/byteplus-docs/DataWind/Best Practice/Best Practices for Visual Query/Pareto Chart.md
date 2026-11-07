---
title: "Pareto Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Pareto_Chart"
---

<span id="_1-示例"></span>
# 1. Example

A Pareto chart consists of a bar chart and a line chart, where the bars display metric values in descending order, and the line shows the cumulative percentage. Using sales revenue by category as an example, a Pareto chart can be drawn to display the cumulative proportion of top product categories and identify key categories.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/026afc3cd4964b99bf08cd4b51d3dc03~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-操作步骤"></span>
# 2. Procedure

(1) Using a Pareto chart of sales revenue by subcategory as an example: Select the chart type as dual\-axis chart, set subcategory as the dimension and sales revenue as the primary axis, and ensure the chart displays subcategory versus sales revenue.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/026afc3cd4964b99bf08cd4b51d3dc03~tplv-goo7wpa0wc-image.image) </span>

(2) Use the sorting function in the analysis module to sort sales revenue in descending order.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ff6bb6c29594ff38a01688154c46810~tplv-goo7wpa0wc-image.image) </span>

(3) Create a cumulative percentage field with the following expression:

`running_sum(sum([sale_price])) along ([product_type])/total(sum([sale_price])) along ([product_type])`

This is a combination of two table calculation functions. The running_sum function calculates the rolling sum of sales revenue by subcategory, which is then divided by the total sales revenue of all subcategories. The result is the cumulative proportion of the total for each subcategory.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20ba1e59c7484e98be08317b4daff455~tplv-goo7wpa0wc-image.image) </span>

(4) Drag the cumulative percentage field to the secondary axis of the metric to form a Pareto chart. The chart configuration on the left can be used to adjust the axis data format and change the secondary axis data format to percentage.
