---
title: "Radar Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Radar_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

The radar chart, also known as a spider web chart, allows for the analysis and comparison of multiple indicators within the same coordinate system. It is highly effective for identifying which dimensions have similar values and for detecting outliers among dimensions. Similarly, radar charts are often used for displaying data related to ranking, evaluation, review, and more.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common use cases


* Radar charts can be used to identify which dimensions have higher or lower scores, enabling quick identification of strengths and weaknesses.

* Radar charts also facilitate comprehensive multidimensional analysis to effectively assess a company's operational status.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/910c31c4cb8541c191e12a87415fca6c~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Set dimensions, indicators, and filter conditions**

Select [product_type] as the dimension and [price] as the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41e3fba08f05470290e22ab161e3117a~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the radar chart**

Select the radar chart on the left.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48a1daaab1674a9fb738e7d1ed71ee56~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Set the style**

The display style of the radar chart can be configured.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87c94870bf2b4be18768d72fc0481138~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-雷达图图标"></span>
## 3.1 Radar chart icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fca241a893e14cdb9125cdcfe2d9cac3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

Select one or more dimensions and one or more indicators.

<span id="_3-3-轴标签配置"></span>
## 3.3 Axis label configuration

Set the dimension as the axis label.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5189125a21834f8d9a5390f7f516b087~tplv-goo7wpa0wc-image.image) </span>

Set the indicator as the axis label.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/302ce2d2d9b8425880388723476c3f6f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-编辑颜色"></span>
## 3.4 Edit colors

You can assign different colors to different indicators, and multiple built\-in color schemes are available.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e54a8bb10b2d475e9886d04a0ad13e0d~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-5-线条样式"></span>
## 3.5 Line style

**Line type**: You can set the thickness of the line, as well as solid, dashed, or dotted lines.

**Marker**: You can choose no marker, hollow circle, solid circle, square, diamond, and select the marker size.

**Example**: Line thickness = 3, dashed line; marker is hollow circle, size = 3.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cdbeae7fe9d9488eb7c4c8e62d93fd09~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-特殊值"></span>
## 3.6 Special values

You can customize the display of special values for dimensions, indicators, or polylines.


* Dimensions and indicators can be set to display special values as blank, NULL, 0, or \-\-.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3e5cb709a3a4aa1863d44ce76393426~tplv-goo7wpa0wc-image.image) </span>

* Polylines can be set to display special values as 0 at empty values or connect the polyline at empty values.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e43cf2227064f8aa2606d2f740115dd~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-7-轴"></span>
## 3.7 Axis

**Axis range**: Automatic or specified range.

**Axis label**: Enable or disable axis labels.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/263f4d7f146e42428951bbdf9344e5fa~tplv-goo7wpa0wc-image.image) </span>

**Axis and grid lines**: The display style of axis and grid lines can be adjusted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08394309e57046399583f9aa20892eb6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-图例、标签"></span>
## 3.8 Legend and labels

**Legend:** 


* You can click the switch button on the right to choose whether to display legend information.

* You can set the legend's display position in the chart: top, bottom, left, or right.

* You can set the legend's alignment: align to top/left, center, or bottom/right.

* You can set the maximum number of rows/columns for the legend, as well as the font and color.

* You can set the legend's display mode. When there are too many legend items, you can choose between a pager or a scrollbar for display.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e64d7cd10ee34d08a6930b8c3b476ad9~tplv-goo7wpa0wc-image.image" width="2938px" />   </div>
   


**Labels:** 


* You can click the switch button on the right to choose whether to display label information.

* Labels are displayed on the top layer of the chart. After enabling labels, the metric values will be shown on the chart.

* You can set custom styles for labels, including display position, display mode, label font and color, and display content.


Caution: Only one of "Sparse display" or "Allow overlap" can be selected as the display mode. If one is selected, the other will be grayed out, with a prompt stating "Allow overlap and sparse display cannot be selected at the same time." When labels are crowded by default, it is recommended to select "Sparse display."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a4f33f9227c4562b248411fb0bbe892~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-9-图内控件样式"></span>
## 3.9 In\-chart control styles

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-10-恢复默认设置"></span>
## 3.10 Restore default settings

Click [Restore Default Settings] to revert all of the above chart configurations to their default values.
