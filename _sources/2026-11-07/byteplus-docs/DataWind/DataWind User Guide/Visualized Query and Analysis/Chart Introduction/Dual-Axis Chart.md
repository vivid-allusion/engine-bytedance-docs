---
title: "Dual-Axis Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dual-Axis_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

A dual\-axis chart refers to a data chart where data shares a single X\-axis while displaying multiple Y\-axes. In practical applications, it is often a combination of a bar chart and a line chart. The product provides a variety of dual\-axis chart components, allowing flexible configuration of chart types, line styles, arrangement methods, and more.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

In a dual\-axis chart, data presentation is more intuitive. Dual\-axis charts can be used to analyze the relationship between two different metrics under the same dimension. They are also suitable for scenarios such as comparing trends of different data, as well as year\-over\-year and month\-over\-month comparisons.

For example, to view both "order quantity" and "order amount" on the same chart, the significant difference in values often makes it difficult to distinguish between the data. A dual\-axis chart can address the differences in scale between different metrics, with the left axis measuring [order quantity] and the right axis measuring [sales price].

**Dual\-axis chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1de958fea8c4ef0b8f2cfc0eaa72729~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Usage process example

**Step 1: Click to select or drag in dimensions, metrics, secondary axis metrics, and select filter conditions**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cf2cf2a71bf4d869ddecd73cf7b4c05~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Click the dual\-axis chart icon. The system will automatically generate a dual\-axis chart by default, with the primary Y\-axis as a bar chart and the secondary Y\-axis as a line chart**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9ee66a790cd48f68af941d38e850e01~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcbbcdd16e394ab29a64792f6f7e2a0c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-双轴图图标"></span>
## 3.1 Dual\-axis chart icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9ee66a790cd48f68af941d38e850e01~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules


* **Dimension**: Supports N dimensions. The first dimension is the X\-axis dimension; subsequent dimensions are color dimensions.

* **Metric**: Left Y\-axis, supports multiple metrics

* **Secondary axis metric**: Right Y\-axis, supports multiple metrics. The fields for metrics and secondary axis metrics can be interchanged

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d63ce6d3373496ea0bfd46dcbeaafb3~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-3-编辑颜色"></span>
## 3.3 Edit color

You can set corresponding colors for the dual\-axis chart. The product provides multiple built\-in color schemes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08708b07ddcb40f5964295d11dfeb131~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-4-图表类型"></span>
## 3.4 Chart types

Both the primary and secondary axes of the dual\-axis chart provide four chart types, which can be switched in [Chart Type].


* The primary axis is a stacked bar chart, and the secondary axis is a line chart

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3767e649a6d440ab81bdec8e0e3791d3~tplv-goo7wpa0wc-image.image) </span>

* The primary axis is a line chart, and the secondary axis is an area chart

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a28bf75ab6e44eccb7788413f3f96ea8~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-5-线条样式"></span>
## 3.5 Line styles


* **Line type**: You can select polyline or smooth lines, adjust the line thickness (thick or thin), and choose solid, dashed, or dotted lines.

* **Marker**: You can choose no marker, hollow circle, solid circle, square, diamond, and select the marker size.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/218bc3943d8a499283dad0ea43e66a2b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-排列方式"></span>
## 3.6 Arrangement

You can choose whether to enable parallel display of indicators.


* Yes, as shown below:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d9fdb1aa50c43faa3315220d60142de~tplv-goo7wpa0wc-image.image) </span>


* No, as shown below:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f7db85144054716bb8d562bef9270fe~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-7-x轴"></span>
## 3.7 X\-axis


* **X\-axis**: Click the switch button on the right side of the X\-axis to choose whether to display X\-axis information.

* **Axis name checkbox**: You can check or uncheck this option. After checking, you can modify the name, which defaults to the field name.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis label**: You can set the font size, font color, and text tilt angle (0–360 degrees).

* **Axis line**: You can set the color of the axis line.

* **Thumbnail**: Can be used to zoom the chart horizontally or vertically.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89c49f83b91f413fa05945798c7af88e~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-8-y-轴-主轴-次轴"></span>
## 3.8 Y\-axis – primary/secondary axis

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5dddd285c3248ba9d529d1ea498aea6~tplv-goo7wpa0wc-image.image) </span>


* **Y\-axis – primary/secondary axis**: Click the switch button on the right side of the Y\-axis – primary/secondary axis to choose whether to display Y\-axis – primary/secondary information.

* **Axis name**: You can check or uncheck this option. After checking, you can modify the name, which defaults to the field name.

* **Axis range**: There are three options: Auto, Auto (excluding 0), and Specified range.

   * Auto: (negative value, 0, positive value), includes 0.

   * Auto (excluding 0).

   * Specified range: You can manually enter the minimum and maximum values. The value on the right must be greater than the value on the left and cannot be empty.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6439ccdc99384f29b0420027996e4958~tplv-goo7wpa0wc-image.image) </span>

* **Data format**: Click to set the label data format of the axis in the pop\-up window. You can set it to number, percentage, per mille, or original value.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c00d9f371573442d947b165491e75665~tplv-goo7wpa0wc-image.image) </span>

* **Axis scale**: Controls the scale display of the axis. Generally, it is linear, but logarithmic processing is also available, such as log(base 2), which means taking the logarithm with base 2. This is generally used in scenarios such as operations monitoring where the values of two indicators on the same axis differ greatly.

* **Axis format**: Refers to setting the label data format of the axis. You can set it to number, percentage, per mille, or original value.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis label**: You can set the font size, font size, and text rotation angle (0–360 degrees);

* **Axis line**: You can set the color of the axis line.


<span id="_3-9-网格线"></span>
## 3.9 Grid lines

See [3.6 Grid lines](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-7-%E7%BD%91%E6%A0%BC%E7%BA%BF).

<span id="_3-10-特殊值"></span>
## 3.10 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-11-图例、标签"></span>
## 3.11 Legend and labels

**Legend:** 


* You can click the toggle button on the right to choose whether to display the legend information.

* You can set the legend's position in the chart: top, bottom, left, or right.

* You can set the legend's alignment: align to top/left, center, or align to bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.

* You can set the legend's display mode. When there are too many legend items, you can choose between a pager or a scrollbar for display.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fd6534f80144b3ebade044814387db9~tplv-goo7wpa0wc-image.image) </span>

**Label:** 

For basic configuration, see [3.8 Legend and labels](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-9-%E5%9B%BE%E4%BE%8B%E3%80%81%E6%A0%87%E7%AD%BE).

Dual\-axis charts support displaying labels as percentages. Click the settings button next to the percentage to set the number of decimal places and the prefix or suffix.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cccbc4a91614984a6c0320f24adc502~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-12-提示信息"></span>
## 3.12 Tooltip

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

<span id="_3-13-显示模式"></span>
## 3.13 Display mode

See [3.10 Display mode](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-11-%E6%98%BE%E7%A4%BA%E6%A8%A1%E5%BC%8F).

<span id="_3-14-图内控件样式"></span>
## 3.14 In\-chart control style

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-15-恢复默认设置"></span>
## 3.15 Restore default settings

Click [Restore default settings] to revert all of the above chart configurations to their default values.

<span id="_3-16-透视"></span>
## 3.16 Pivot

See [Pivot Chart](https://docs.byteplus.com/docs/DataWind/Pivot_Chart).
