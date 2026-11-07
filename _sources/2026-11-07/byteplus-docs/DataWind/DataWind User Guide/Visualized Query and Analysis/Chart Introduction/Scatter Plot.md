---
title: "Scatter Plot"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Scatter_Plot"
---

<span id="_1-概述"></span>
# 1. Overview

A scatter plot, also known as an X\-Y chart, displays all data as points on a Cartesian coordinate system to show the degree of interaction between variables. The position of each point is determined by the values of the variables. The product provides scatter plot components that support multiple colors, sizes, and legend options.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common use cases

On a scatter plot, the position of each point is determined by the values of the variables. Scatter plots are commonly used to determine the relationships or degree of interaction between variables.

**Scatter plot example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/103d4628816d47f1a75d2a3b0cf51d1f~tplv-goo7wpa0wc-image.image) </span>

<span id="使用过程示例"></span>
## Usage process example

**Step 1: Set dimensions, metrics, and filter conditions**

Select "Province" as the dimension, and "Income" and "Expenditure" as metrics. Filter the partition date to the most recent day with data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8c7cc0272724d3c8e837261edbc6481~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- scatter plot**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45c8b39e037846d9ae6a62da72bf2265~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7afd5f8337bb448f903148cfc9914508~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-散点图图标"></span>
## 3.1 Scatter plot icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45c8b39e037846d9ae6a62da72bf2265~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

Select one or more dimensions and two metrics. The two metrics correspond to the X and Y axes, respectively. Changing the order of the metrics will change the correspondence between the X and Y axes.

<span id="_3-3-颜色与尺寸"></span>
## 3.3 Color and size

**Color**: Different colors can be configured for different values based on a specific dimension. For example, the following figure groups cities by configuring different colors according to the province. The color scheme can be modified in "Edit Color".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/780ce759a8e24879b410a9ccfa862a4f~tplv-goo7wpa0wc-image.image) </span>

**Size**: The size of the scatter points can be configured based on a specific metric and its value. For example, the following figure configures the scatter point size according to "Fixed Cost".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/368ba1523e0942dd86799476de7baed6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-x-轴-y-轴"></span>
## 3.4 X axis/Y axis


* **X axis / Y axis**: You can click the toggle button to the right of the X axis/Y axis to choose whether to display the X axis/Y axis information.

* **Axis name checkbox**: You can check or uncheck the box. After checking, you can modify the name, which defaults to the field name.

* **Axis range**: There are three options: Auto, Auto (excluding 0), and Specified range:

   * Auto: (negative values, 0, positive values), includes 0.

   * Auto (excluding 0).

   * Specified range: You can manually enter the minimum and maximum values. The value on the right must be greater than the value on the left and cannot be empty.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9348c4b050eb4019a7ee82d4db3bb09a~tplv-goo7wpa0wc-image.image) </span>

* **Data format**: Click to configure the label data format of the axis in the popup window. Can be set to number, percentage, per mille, or raw value.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16608c04004f41eb99da4d4be8cc5f32~tplv-goo7wpa0wc-image.image) </span>

* **Axis scale**: Controls the scale display ratio of the axis. Typically, it is linear, but logarithmic processing is also supported, such as log(base 2), which takes the logarithm with base 2. This is generally applicable to scenarios like operations monitoring where the values of two metrics on the same axis differ significantly.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis label**: You can set the font size, font color, and text tilt angle (0–360 degrees).

* **Axis line**: You can set the color of the axis line.

* **Thumbnail**: Can be used to zoom the chart horizontally or vertically.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/185c1dfbc95442089203c07556e0b642~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-5-网格线"></span>
## 3.5 Grid lines

You can enable grid lines to assist in observing values. Both horizontal and vertical display are supported, and the grid line style can also be adjusted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d0861cf099c496393a7a37f46dbb60e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-特殊值"></span>
## 3.6 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-7-图例、标签"></span>
## 3.7 Legend and label

**Legend:** 


* You can click the switch button on the right to choose whether to display legend information.

* You can set the position of the legend in the chart: top, bottom, left, or right.

* You can set the legend alignment: align to top/left, center, or align to bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.

* You can set the legend display mode. When there are too many legends, you can choose between pager or scrollbar display effects.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee0a6c83860343179817af83f485ccb0~tplv-goo7wpa0wc-image.image" width="2938px" />   </div>
   


**Label:** 


* You can click the switch button on the right to choose whether to display label information. Both default and custom styles are supported.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/249bf8ad10434a9094fbd79801caa4ca~tplv-goo7wpa0wc-image.image) </span>


* Custom styles support setting the display position.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cdad3924fa274e8398432a37baec29aa~tplv-goo7wpa0wc-image.image) </span>


* Custom styles support setting the display mode.


Caution: Only one of "sparse display" or "allow overlap" can be selected. If one is selected, the other will be grayed out, with a prompt stating "Allow overlap and sparse display cannot be selected at the same time." When labels appear crowded by default, it is recommended to select "sparse display."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32236522f7c94d8db356b687cfbbb1b4~tplv-goo7wpa0wc-image.image) </span>


* Custom styles support setting the label font and color.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef1b9c8c4cc84b33b36feb8870c8cd45~tplv-goo7wpa0wc-image.image) </span>


* Supports setting the display content.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39dcefbae49f4fa49478ba1bb73b57b4~tplv-goo7wpa0wc-image.image) </span>

Caution: You can set the percentage data format, the default value for percentages, and historical data to two decimal places.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcc9f73f0d5d416fbcba94b61f4a8d85~tplv-goo7wpa0wc-image.image) </span>


* You can set the label display type: choose to display all, minimum value, maximum value, minimum & maximum values, or both end values.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcab499e33224f7abaa82ba06c96c2e9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-提示信息"></span>
## Note

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

<span id="_3-9-图内控件样式"></span>
## 3.9 In\-chart control styles

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-10-恢复默认设置"></span>
## 3.10 Restore default settings

Click [Restore Default Settings] to revert all of the above chart configurations to their default values.
