---
title: "Line Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Line_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

A line chart plots data points on a graph and connects them with straight lines. It displays increasing and decreasing trends in data over time or other variables through the upward or downward movement of the lines. This product provides a variety of line chart components, allowing users to flexibly configure line styles, legends, labels, and more, to analyze and present data changes more clearly.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common use cases

Line charts can clearly show increasing and decreasing trends in data, the rate of change, patterns, peaks, and other characteristics. They are suitable for displaying trends where data varies with a certain dimension. For example, [brand sales] varies with [date].

**Table example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d58d3670a68e46b2850e7041ed5bd135~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Usage example

**Step 1: Set dimensions, metrics, and filter conditions**

Select [date] as the dimension and [brand sales] as the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34a67580da3147338a8a56f6dc7deb18~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- line chart**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bf86edf3cf0473f808ab79ebb5a6f33~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a81ae4486184ca8848df034e2a90778~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-折线图图标"></span>
## 3.1 Line chart icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32f2c10c6f704f8498e13ce2fa0c7446~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

Line charts support plotting after setting one or more dimensions and one or more metrics.

**Dimension**: Supports one or more dimensions.


* The first dimension will be used as the x\-axis.

* If there is more than one dimension, the second and subsequent dimensions will generate multiple lines for display, using different colors to distinguish them.


**Metric**: Supports one or more metrics.


* Metric values will be displayed as lines on the chart.

* If there is more than one metric. The second and subsequent metrics will generate multiple lines for display, using different colors to distinguish them, and you can adjust the line style configuration as needed.


**Example 1**: 1 dimension, 2 metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/089f048fd65749879a983444c8342e51~tplv-goo7wpa0wc-image.image) </span>

**Example 2**: 2 dimensions, 1 metric

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df24d361e81a412ca94fd1f96e920bb9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit colors

You can set the corresponding colors for the line chart. The product provides multiple built\-in color schemes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7dacef5a21c947f794f92ab631860897~tplv-goo7wpa0wc-image.image) </span>

Support is also provided for [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-4-线条样式"></span>
## 3.4 Line styles

**Scope of effect**: You can set different display styles for a specified data series.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e09e39ba700d4a40815754f5e0ba1328~tplv-goo7wpa0wc-image.image) </span>

**Line style**: You can choose polyline or smooth lines, set the thickness, and select solid, dashed, or dotted lines.

**Marker**: You can choose no marker, hollow circle, solid circle, square, diamond, and set the marker size.

**Example**: Line style: smooth, thickness = 5, dotted line; marker: hollow circle, size = 5

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/524736a06f7f4bffb726cf57f8dd1aaf~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-x-轴-y-轴"></span>
## 3.5 X axis/Y axis

See [3.5 X-axis/Y-axis](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-6-x-%E8%BD%B4-y-%E8%BD%B4).

<span id="_3-6-网格线"></span>
## 3.6 Grid lines

See [3.6 Grid lines](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-7-%E7%BD%91%E6%A0%BC%E7%BA%BF).

<span id="_3-7-特殊值"></span>
## 3.7 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-8-图例、标签"></span>
## 3.8 Legend, label

**Legend:** 


* You can click the switch button on the right to choose whether to display legend information.

* You can set the display position of the legend in the chart: top, bottom, left, or right.

* You can set the legend alignment: align to top/left, center, or bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.

* You can set the legend display mode. When there are too many legend items, you can choose between pagination or a scrollbar for display.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e4c5bd0cc2a4d7fba7e3639e52a6808~tplv-goo7wpa0wc-image.image" width="2938px" /></div>


**Label:** 


* You can click the switch button on the right to choose whether to display label information.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/174e4b485d72435cb5c8419c50f22859~tplv-goo7wpa0wc-image.image) </span>


* Supports selecting the default style or a custom style.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9155ed24d514d74bcde42c0c6962313~tplv-goo7wpa0wc-image.image) </span>


* Custom style supports setting the display position.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18f6b5bb177441bc901e5a26a5668f17~tplv-goo7wpa0wc-image.image) </span>


* Custom style supports setting the display mode.


Caution: Only one of "Sparse display" or "Allow overlap" can be selected. If one is selected, the other will be grayed out, with a prompt stating "Allow overlap and sparse display cannot be selected at the same time." When the default label display is crowded, it is recommended to select "Sparse display."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ff6656b7ec6489bb5d907cb7bb4ce8b~tplv-goo7wpa0wc-image.image) </span>


* Custom style supports setting the label font and color.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18e3e2217d5443079a3321baeb846434~tplv-goo7wpa0wc-image.image) </span>


* Supports setting the display content.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/559e633a0e384e6b81deb230cab39df0~tplv-goo7wpa0wc-image.image) </span>


* You can set the label display type: choose to display all, minimum value, maximum value, minimum and maximum values, or both endpoints.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aa8868363804a0e863f7face65c6347~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-9-提示信息"></span>
## 3.9 Tooltip

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

<span id="_3-10-显示模式"></span>
## 3.10 Display mode

See [3.10 Display mode](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-11-%E6%98%BE%E7%A4%BA%E6%A8%A1%E5%BC%8F).

<span id="_3-11-图内控件样式"></span>
## 3.11 In\-chart control style

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-12-恢复默认设置"></span>
## 3.12 Restore default settings

Click [Restore default settings] to revert all the above chart configurations to their default settings.

<span id="_3-13-透视"></span>
## 3.13 Pivot

See [Pivot Chart](https://docs.byteplus.com/docs/DataWind/Pivot_Chart).
