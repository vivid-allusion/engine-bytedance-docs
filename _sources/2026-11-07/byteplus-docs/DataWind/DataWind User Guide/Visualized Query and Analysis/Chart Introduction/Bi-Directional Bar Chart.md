---
title: "Bi-Directional Bar Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Bi-Directional_Bar_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

A bi\-directional bar chart uses forward and reverse bars to display numerical comparisons between categories. In this chart, the categorical axis represents the categorical dimension to be compared, and the continuous axis represents the corresponding values. There are two cases: one where the positive and negative scale values are completely symmetrical, and another where the positive and negative scale values are inversely symmetrical, that is, they are negatives of each other.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

Suitable for scenarios comparing opposing categories, such as income and expenditure, completed and incomplete, and similar comparisons.

**Bi\-directional bar chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f0aebb57d5845fe8b3ee56809582807~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Set dimensions, metrics, and filter conditions**

Select "Industry Name" as the dimension, and "Income" and "Expenditure" as the metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64d0c2037b774c2daeb2d82df2151028~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- Bidirectional bar chart**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ae6611e041a4a5694f68cbd7bb571c5~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf47f491f2ae46829a997071685dd505~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-双向条形图图标"></span>
## 3.1 Bi\-directional bar chart icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ae6611e041a4a5694f68cbd7bb571c5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

After selecting one dimension and two metrics, select the bidirectional bar chart to draw the chart. You can change the field order of the two metrics to adjust the left and right axis order in the chart.

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit colors

You can set corresponding colors for the two metrics, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36696592ae8248949a6b676128a553ac~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-y-轴"></span>
## 3.4 Y axis


* **Y axis**: You can click the toggle button on the right side of the Y axis to choose whether to display Y axis information.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis label**: You can set the font size, font color, and text angle (0\-360 degrees).

* **Axis line**: You can set the color of the axis line.

* **Navigator**: Can be used for vertical zooming of the chart


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1089990137544188d1a14cff9c0b6b5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-x-轴-左轴-x-轴-右轴"></span>
## 3.5 X axis \- left axis / X axis \- right axis


* **X axis \- left axis / X axis \- right axis**: You can click the toggle button on the right side of X axis \- left axis / X axis \- right axis to choose whether to display X axis \- left axis / X axis \- right axis information.

* **Axis name checkbox**: You can check or uncheck it. After checking, you can modify the name, which defaults to the field name.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis range**: There are three options: Auto, Auto (excluding 0), and Custom range.

   * Automatic: (negative values, 0, positive values), including 0;

   * Automatic (excluding 0);

   * Specified range: You can manually enter the minimum and maximum values. The value on the right must be greater than the value on the left, and neither field can be empty;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0735cd4b8ee44d199d651162bfad352~tplv-goo7wpa0wc-image.image) </span>


* **Data format**: Click to configure the axis label data format in the pop\-up window. You can set it to number, percentage, per mille, or raw value;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05309685f00c49ecaf79835f2579de21~tplv-goo7wpa0wc-image.image) </span>


* **Axis scale**: Controls the scale display of the axis. Typically linear, but logarithmic scaling is also supported, such as log(base 2), which means taking the logarithm with base 2. This is generally used in scenarios such as operations monitoring where two metrics on the same axis have large value differences.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfa271d3fad947fd9ca4ad6ec59368e1~tplv-goo7wpa0wc-image.image) </span>


* **Axis label**: You can set the font size, font color, and text rotation angle (0–360 degrees);

* **Axis line**: You can set the color of the axis line;

* **Thumbnail**: Can be used to zoom the chart horizontally or vertically;


<span id="_3-6-图例、标签"></span>
## 3.6 Legends and labels

**Legend:** 


* You can click the switch button on the right to choose whether to display the legend information;

* You can set the display position of the legend in the chart: top, bottom, left, or right.

* You can set the legend alignment: align to top/left, center, or bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.

* You can set the legend display mode. When there are too many legends to display, you can choose between a pager or a scrollbar for display.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/467c05a591fc424694a89c6339d70f36~tplv-goo7wpa0wc-image.image) </span>

**Label:** 

See [3.8 Legend and labels](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-9-%E5%9B%BE%E4%BE%8B%E3%80%81%E6%A0%87%E7%AD%BE).

<span id="_3-7-提示信息"></span>
## 3.7 Tooltips

When the mouse hovers over the data area, the tooltips will display information.

By default, the dimensions and metrics of the current data are displayed. You can also customize the tooltip as needed.

**Default tooltips**

After enabling the tooltips, you can select "Display content" and choose from three display modes: "Single data point + whole row", "Single data point only", or "Whole row only".

Note: To display single data point information, you can add fields to single data points and configure custom tooltips information. The added fields only appear in the tooltips for single data points and are not involved in chart rendering.


* Single data point + whole row


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e403b7c5afc47579e6a719c226b0388~tplv-goo7wpa0wc-image.image) </span>


* Single data point only


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8175214602614e3b89e46d4e6858f995~tplv-goo7wpa0wc-image.image) </span>


* Whole row data only


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/741306560ef14b99ab5e94c1513174a1~tplv-goo7wpa0wc-image.image) </span>

**Custom prompt message**

(1) Supports adding other metrics from the dataset to supplement the prompt message.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b34068c05ab4de79c5b83e741807e21~tplv-goo7wpa0wc-image.image) </span>

(2) Click the "Advanced settings" button to further configure [Custom Tooltips Information](https://docs.byteplus.com/docs/DataWind/Custom_Tooltips_Information) in the pop\-up edit box. Supports entering text and inserting fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec8d22e8e4794572862d8ec8c7e4ec5b~tplv-goo7wpa0wc-image.image) </span>

After editing text and fields and adjusting the layout, you can achieve a customized effect. Click Preview to preview the effect.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2880fc467bc249de8af58fff0625c76a~tplv-goo7wpa0wc-image.image) </span>

Click "OK" to apply to the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8aa1835f42054595ab03e59fbcf7981f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-组内控件样式"></span>
## 3.8 Group control style

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-9-恢复默认设置"></span>
## 3.9 Restore default settings

Click [Restore default settings] to restore all of the above chart configuration content to the default settings.
