---
title: "Funnel Map"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Funnel_Map"
---

<span id="_1-概述"></span>
# 1. Overview

A funnel chart is a chart shaped like a funnel, using trapezoidal areas to represent the difference in business volume between each stage and the previous stage. The funnel chart is arranged from top to bottom in a logical sequence and is used to describe the completion of business objectives as the business process progresses.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common use cases

Funnel charts are suitable for analyzing business processes that are standardized, have a long cycle, and consist of multiple stages. By comparing the business data at each stage of the funnel, it is possible to intuitively identify and explain issues. Common analysis scenarios include the following:

(1) For example, in e\-commerce website data, funnel charts can visually display the conversion status throughout the entire process from the initial website display to the final order placement and purchase.

(2) In customer management, the customer sales funnel chart can be used to compare conversions at each stage for different customers.

**Funnel chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f5fe90058bb41dfad19e1eef34814aa~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Set dimensions, metrics, and filter conditions**

Select [sale_province] as the dimension and [sale_price] as the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cde500e20a4437abf19016e2eb550f7~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- Funnel chart**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e07243188b5e46baa544dc9aa5417fe7~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Sort by quantity**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba791ced86e84a1e99e3895a165173b8~tplv-goo7wpa0wc-image.image) </span>

**Step 4: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc3826f11b2342139dbf4a84578c7079~tplv-goo7wpa0wc-image.image) </span>

**Step 5: Multiple metrics can be used as funnel layers**

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-漏斗图图标"></span>
## 3.1 Funnel chart icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba37218c29824321b007e43c9eb819bc~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

Select one dimension and one metric; different dimension items correspond to different funnel layers

Or select zero dimensions and two or more metrics; different metrics correspond to different funnel layers

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit colors

You can configure different colors for different values of funnel layers, and there are multiple built\-in color schemes:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87d82213c96d4f1b85a3cc318c682949~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-4-展示方向"></span>
## 3.4 Display orientation


* Vertical

* Horizontal


<span id="_3-5-漏斗层名称"></span>
## 3.5 Funnel layer names


* You can click the toggle button on the right to display or hide funnel layer names

* Font size and color


<span id="_3-6-图例、标签"></span>
## 3.6 Legend and labels

**Legend:** 


* You can click the toggle button on the right to display or hide legend information.

* You can set the legend's position in the chart: top, bottom, left, or right.

* You can set the legend's alignment: top/left, center, or bottom/right.

* You can set the legend's maximum number of columns, font, and color.

* You can set the legend's display mode. When there are too many items in the legend, you can choose between pagination or a scroll bar for display.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c62041d57af4dc0a87ac6416f942ff6~tplv-goo7wpa0wc-image.image) </span>

**Labels:** 


* You can click the toggle button on the right to choose whether to display label information.

* Labels are displayed on the top layer of the chart. After enabling labels, the metric values are shown on the chart.

* You can set the label font size and color.

* You can set the displayed content: value, conversion rate, or arrival rate.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ca39655a83d44cd8f1cf8a44cb7de8c~tplv-goo7wpa0wc-image.image) </span>
