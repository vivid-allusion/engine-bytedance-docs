---
title: "Bubble Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Bubble_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

The bubble chart allows for comparison of data under dimensions using a scatter plot style. By adding color and size configurations, bubbles can be displayed in different sizes and colors to add more dimensions to the analysis.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用场景示例"></span>
## 2.1 Common scenario examples

In a bubble chart, the X\-axis represents the dimension and the Y\-axis represents the measure. It is common to configure color and size to add analytical perspectives and achieve multidimensional analysis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6dae3c8f86b4aa1b6961eb1d74311f8~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Usage process example

**Step 1: Set dimension, measure, and filter conditions**

Configure one dimension and one measure. After configuration, the measure values for each dimension are displayed in a scatter plot style.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3a09bfd586245c08c34110cd42c93fc~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- bubble chart**

Hover the mouse over the scatter plot in the chart selection area to display a dropdown list, then select bubble chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56dd3bc8c4354ea8826dc637f427f702~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

The display form of the bubble chart can be modified.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dab277f9e5e5428cb1bc7beedda1ba34~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-配置规则"></span>
## 3.1 Configuration rules

In the configuration panel, one dimension and one measure must be added; the dimension is the X\-axis and the measure is the Y\-axis.

<span id="_3-2-颜色与尺寸"></span>
## 3.2 Color and size

By configuring color and size, additional analytical perspectives can be added to the bubble chart. For example, using brand sales by region:

By dragging the dimension "region" into the color section, you can display "brand sales" for each region, and by using different colors, you can distinguish the sales data of different "models".

Adding the dimension "model" to the color section allows you to distinguish "models" by color while displaying "brand sales" for each region, which is equivalent to adding another measure axis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b488b4bba0043e68e8ee2d003c827e1~tplv-goo7wpa0wc-image.image) </span>

Adding the measure "price" to the size section allows you to distinguish "models" by size (with the size representing price) while displaying "brand sales" for each region, which is equivalent to adding another measure axis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a037daf32b54541bec7b7c21c5b2eef~tplv-goo7wpa0wc-image.image) </span>

Caution: The color section supports configuring one or zero dimensions and measures, and the size section supports configuring only one or zero measures.

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit color

The color scheme can be modified using the "Edit color" feature.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ca39703d2814dccb91fe61521e749cc~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-4-x-轴-y-轴"></span>
## 3.4 X\-axis/Y\-axis


* **X\-axis / Y\-axis**: You can click the toggle button to the right of the X\-axis/Y\-axis to choose whether to display X\-axis/Y\-axis information;

* **Axis name checkbox**: Can be selected or deselected. After selecting, the name can be modified. The default is the field name.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis label**: You can set the font size, font color, and text rotation angle (0–360 degrees).

* **Axis line**: You can set the color of the axis line.

* **Data zoom**: It can be used to zoom the chart horizontally or vertically.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b2cd30fcbce42888f87f8ca95758b2a~tplv-goo7wpa0wc-image.image) </span>


* **Axis range (this setting is only available for the Y axis)** : There are three options: Auto, Auto (excluding 0), and Custom range:

   * Auto: (negative values, 0, positive values), includes 0.

   * Auto (excluding 0).

   * Custom range: You can manually enter the minimum and maximum values. The value on the right must be greater than the value on the left, and neither value can be empty.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2824a94dcd21476e8d61e10576874b79~tplv-goo7wpa0wc-image.image) </span>


* **Data format (this setting is only available for the Y axis)** : Click to set the data format of the axis labels in the pop\-up window. You can set it to number, percentage, per mille, or raw value.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/949e71a717ed4ec8a8d4d2e8c0fea18f~tplv-goo7wpa0wc-image.image) </span>


* **Axis scale (this setting is only available for the Y axis)** : Controls the scale display of the axis. In general, it is linear, but logarithmic scaling is also available, such as log(base 2), which means taking the logarithm with base 2. This is generally used in scenarios such as operations monitoring where there is a large difference between the values of two metrics on the same axis.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a0788b9aa874fcdbbca1c3b6b14389d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-网格线"></span>
## 3.5 Grid lines

See [3.6 Grid lines](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-7-%E7%BD%91%E6%A0%BC%E7%BA%BF).

<span id="_3-6-特殊值"></span>
## 3.6 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-7-图例、标签"></span>
## 3.7 Legend and label

**Legend:** 


* You can click the switch button on the right to choose whether to display the legend information.

* You can set the display position of the legend in the chart: top, bottom, left, or right.

* You can set the legend alignment: align to top/left, center, or align to bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a67c7a0562c3491196bd7a510707aedf~tplv-goo7wpa0wc-image.image) </span>

**Label:** 

See [3.8 Legend and labels](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-9-%E5%9B%BE%E4%BE%8B%E3%80%81%E6%A0%87%E7%AD%BE).

<span id="_3-9-提示信息"></span>
## 3.9 Tooltip

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

<span id="_3-10-图内控件样式"></span>
## 3.10 In\-chart control style

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-11-恢复默认设置"></span>
## 3.11 Restore default settings

Click [Restore default settings] to reset all of the above chart configuration content to the default.
