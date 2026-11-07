---
title: "Pie Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Pie_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

A pie chart is a statistical chart that uses a circle to represent the total amount, with the size of each sector within the circle representing the percentage of each part relative to the total. It is also known as a sector chart. The product provides three components: basic pie chart, donut chart, and Nightingale rose chart.


* Donut chart: Represents the total amount in the form of a ring. Compared with a standard pie chart, a donut chart can simultaneously plot data series for multiple samples or populations.

* Nightingale rose chart: Also known as a polar area chart, invented by Florence Nightingale, it is a colorful circular histogram.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common use cases

A pie chart can clearly display the proportion of each data item within a data series. It is suitable for viewing the relationship between the quantity of each part and the total, and also allows for intuitive comparison of the sizes of each part.

**Pie chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d758c40cc2134f6184753798dd2ac770~tplv-goo7wpa0wc-image.image) </span>

**Donut chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b9dec303fa14f0983db376df78f79f5~tplv-goo7wpa0wc-image.image) </span>

**Nightingale rose chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a69444794614fe6b0c8c344a1ce603e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Set dimensions, metrics, and filter conditions**

Select [sale_province] as the dimension and [price] as the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff6cae23505d4631b0e78f29c009af45~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- Pie chart**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/689f0927793548f5af0a63387b74df66~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

For example, to focus only on the top 3 regions by [Brand Sales], you can set the number of sectors to 4, so that the sectors for other regions are merged into one sector for display.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eaf0e07043c94921b1f38e72debec228~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-饼图图标"></span>
## 3.1 Pie chart icon

Click the small triangle under the pie chart to switch between (basic) pie chart, donut chart, and Nightingale rose chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40462e65106f4220a25ece8dd1e0e477~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

Basic pie chart, donut chart, and Nightingale rose chart support multi\-dimension single metric (one or more dimensions and one metric), and zero\-dimension multi\-metric (zero dimensions and multiple metrics) plotting.

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit colors

You can set the corresponding colors for the pie chart. The product provides multiple built\-in color schemes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f246c3ff3a5e4853873e4eb0d8c3ea89~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-4-扇区"></span>
## 3.4 Sectors


* **Number of sectors**: Set the maximum number of sectors to display. The default is 20. If the total number of sectors is less than or equal to the set value, the chart is displayed normally. If the total number of sectors is greater than the set value, the chart will display the (number of sectors \- 1) categories with the largest proportions, and the remaining sectors will be merged into one category labeled [Other].

   Example: The total number of sectors is 5, and the number of sectors is set to 4.

* **Sector radius**: Allows adjustment of the sector radius.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c3ab030b00541129644e28c8c0b5275~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eaf0e07043c94921b1f38e72debec228~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-特殊值"></span>
## 3.5 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-6-图例、标签"></span>
## 3.6 Legend, labels

**Legend:** 


* You can click the toggle button on the right to choose whether to display the legend information.

* You can set the legend's display position in the chart: top, bottom, left, or right.

* You can set the legend's alignment: align to the top/left, center, or align to the bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.

* You can set the legend's display mode. When there are too many legend items, you can choose between a pager or a scrollbar for display.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ec9d763cd624e9096782805da948b2b~tplv-goo7wpa0wc-image.image) </span>

**Labels:** 

See [3.8 Legend and labels](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-9-%E5%9B%BE%E4%BE%8B%E3%80%81%E6%A0%87%E7%AD%BE).

<span id="_3-7-提示信息"></span>
## 3.7 Tooltip information

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

<span id="_3-8-图内控件样式"></span>
## 3.8 In\-chart control styles

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-9-恢复默认设置"></span>
## 3.9 Restore default settings

Click [Restore default settings] to reset all the above chart configurations to their default values.
