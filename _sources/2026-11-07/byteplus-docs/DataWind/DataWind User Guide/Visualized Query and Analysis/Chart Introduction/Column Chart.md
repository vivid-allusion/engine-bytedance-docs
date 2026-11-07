---
title: "Column Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Column_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

A column chart is a statistical chart that displays data using the length of rectangles as variables. Column charts are typically used to compare a single variable across categories (such as different times or conditions), and are generally used for analyzing smaller data sets. The product provides three types of column chart components: stacked column chart, percentage column chart, and grouped column chart. It also supports flexible configuration of colors, arrangement, legends, labels, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd5978c09d744a27ab2b4b9299748cbd~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

Column charts provide an intuitive way to see differences between groups of data. Column charts are suitable for two\-dimensional data, usually with only one variable, and can be used to compare, display, and sort data. In a percentage column chart, the proportion of each series can be seen directly.

<span id="_2-2-使用过程示例"></span>
## 2.2 Usage example

**Step 1: Set dimensions, metrics, and filter conditions**

Select [Province] and [Sales year] as dimensions, and select [order_count] as the metric (you can drag fields from the field list on the left to the data panel to select them, or click to select fields so that they appear in the dimensions or metrics row of the data panel).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e14b0fc0f1494be8ac95ae51f8f13686~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the column chart**

Click the column chart icon on the chart panel to select the column chart. The system will display the column chart according to the default settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75524bda2ee44a32ac1d6e972b37bdc5~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

You can modify the format of the chart as needed, including colors, arrangement, X\-axis, Y\-axis, legends, labels, tooltips, and more. After making the changes, you will get the chart you want.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f388d85b210343fb9d9f740986cb60df~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-柱状图图标"></span>
## 3.1 Column chart icons

Three types of column charts are supported. Click the small triangle under the column chart icon to switch between them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22d1036f93624d42bd28e8a3413f3eca~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-1-堆叠柱状图"></span>
### 3.1.1 Stacked column chart

Dimensions: Supports one or more dimensions. If there is more than one dimension, the columns are stacked to represent each dimension, distinguished by different colors.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b84bd007f89740459b0e9ee56320b156~tplv-goo7wpa0wc-image.image) </span>

Metrics: Supports one or more metrics. If there is more than one metric, they are displayed separately along the X\-axis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e016e0efae5543d3976ecf24bbe196ac~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-百分比柱状图"></span>
### 3.1.2 Percentage column chart

Dimensions: Supports one or more dimensions. If there is more than one dimension, the columns will be stacked, with different colors used to distinguish them. Each column represents 100%.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2919507a49ea4570909a38ebd29a7548~tplv-goo7wpa0wc-image.image) </span>

Metrics: Supports one or more metrics. If there is more than one metric, they will be displayed separately along the x\-axis by default. The sum of all columns for the first dimension is 100%.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5accf44954434330b464e6cdda524258~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-3-并列柱状图"></span>
### 3.1.3 Grouped column chart

Supports one or more dimensions and one or more metrics. If there is more than one dimension or metric, they will be displayed side by side in the column chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/984e84fdf1a5445aa90acbfae7ad8a0a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

You can plot after setting one or more dimensions and one or more metrics.

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit colors

You can assign colors to metrics, and multiple built\-in color schemes are available:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/204f1d64c6824df4985120e4e1c6e937~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-5-排列方式"></span>
## 3.4 Arrangement options

This feature applies to stacked column charts and percentage column charts, allowing you to choose whether to enable metric grouping.


* When metric grouping is enabled, multiple metrics are displayed side by side in the columns, that is, metrics are arranged horizontally, while groups are stacked.

* When metric grouping is disabled, data is stacked or proportionally allocated by metric and group, and metrics are not displayed side by side.


<span id="_3-5-1-开启指标并列"></span>
### 3.4.1 Enable metric grouping

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1cf7e7109dd4983bd4ef945a8a8b6e2~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-2-关闭指标并列"></span>
### 3.4.2 Disable metric grouping

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb3290559064dc289af56457f81aef9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-x-轴-y-轴"></span>
## 3.5 X\-axis/Y\-axis


* **X\-axis / Y\-axis**: You can click the toggle button on the right side of the X\-axis/Y\-axis to choose whether to display X\-axis/Y\-axis information.

* **Axis name checkbox**: You can check or uncheck it. After checking, you can edit the name, which is set to the field name by default.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis label**: You can set the font size, font color, and label angle (0–360 degrees).

* **Axis line**: You can set the color of the axis line.

* **Label spacing**: Can be used to zoom the chart horizontally or vertically. When the slider is enabled on the X\-axis, and the Y\-axis value range and data format are set to auto, adjusting the slider range will dynamically update the Y\-axis labels.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ddc659c570348ea965b154d8faf596a~tplv-goo7wpa0wc-image.image) </span>

* **Axis range (only available for the Y\-axis)** : There are three options: Auto, Auto (excluding 0), and Custom range:

   * Auto: (negative values, 0, positive values), includes 0;

   * Auto (excluding 0);

   * Specified range: You can manually enter the minimum and maximum values. The value entered on the right must be greater than the value on the left, and neither field can be empty.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bac4fe04488847ed888ba06ccd61ed63~tplv-goo7wpa0wc-image.image) </span>

* **Data format (only available for the Y axis)** : Click to set the label data format for the axis in the pop\-up window. You can set the format to number, percentage, per mille, or raw value.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a549bf4ab1824357acd06bbdb3d80ea4~tplv-goo7wpa0wc-image.image) </span>

* **Axis scale (only available for the Y axis)** : Controls the scale display of the axis. By default, it is linear, but logarithmic processing is also supported, such as log(base 2), which takes the logarithm with base 2. This is generally used in scenarios such as operations monitoring where two metrics on the same axis differ greatly in value.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2b88171b0ca44b5b59699fb99ef7faf~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-7-网格线"></span>
## 3.6 Grid lines

You can enable grid lines to assist in observing values. Both horizontal and vertical display are supported, and the grid line style can also be adjusted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62d26d1637f54fce951f5524c4c69369~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-特殊值"></span>
## 3.7 Special values

You can customize settings for special values of dimensions or metrics. Special values can be displayed as blank, NULL, 0, or \-\-.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d4f30592c184b0995eda64b76f1e376~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-1-在表格类型图表中"></span>
### 3.7.1 In table\-type charts

The display of special values for dimensions affects all dimensions; the display of special values for metrics affects all metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd36376c6a1c451cbc77aa59a4cb2a21~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-2-在折线图中"></span>
### 3.7.2 In line charts

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f9e46ee6ac047dcac57caa2479864f2~tplv-goo7wpa0wc-image.image) </span>

Connect the line across missing values.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1da80f3b8c6c4ada9806e3458ef4bf79~tplv-em5hxbkur4-noop.image) </span>

Break the line at missing values.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e42a81f8a96942f782550399963e6827~tplv-em5hxbkur4-noop.image) </span>

Set the value to 0 for missing values.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/0e14d0dc3e624f1189f575a2848e409c~tplv-em5hxbkur4-noop.image) </span>

<span id="_3-9-图例、标签"></span>
## 3.8 Legend and labels

**Legend:** 


* You can click the switch button on the right to choose whether to display legend information.

* You can set the legend's display position in the chart: top, bottom, left, or right.

* You can set the legend's alignment: top/left alignment, center alignment, or bottom/right alignment.

* You can set the maximum number of rows/columns for the legend, as well as its font and color.

* You can set the legend's display mode. When there are too many legend items, you can choose between a pager or a scrollcolumn for display.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccbaa7579077471482e97b37b7b6f3e7~tplv-goo7wpa0wc-image.image" width="2936px" /></div>


**Labels:** 


* You can click the switch button on the right to choose whether to display label information.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73f481d4a846458a93e34cfe241ddf62~tplv-goo7wpa0wc-image.image) </span>


* You can choose between default style and custom style.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c363df9f822427cb4abaf80d2fb5b1f~tplv-goo7wpa0wc-image.image) </span>


* You can set the display position for custom style.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/892daa6320bd4daf941eb565395979ad~tplv-goo7wpa0wc-image.image) </span>


* You can set the display mode for custom style.


Caution: Only one of "Sparse display" or "Allow overlap" can be selected. If one is selected, the other will be grayed out, with a prompt stating "Allow overlap and sparse display cannot be selected at the same time." When labels appear crowded by default, it is recommended to select "Sparse display."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3799e87e5a6e4cc2ab1d729299a09233~tplv-goo7wpa0wc-image.image) </span>


* Custom styles support setting the label font and color.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f484f9c51044aff8c7e646d8c2d60f9~tplv-goo7wpa0wc-image.image) </span>


* Supports setting the display content.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5652980828cf46bc9404330c0db8a8fa~tplv-goo7wpa0wc-image.image) </span>

Caution: You can set the percentage data format, the default percentage value, and the display of historical data to two decimal places.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a999459504f04b31a8bedb6400fa407a~tplv-goo7wpa0wc-image.image) </span>


* Supports setting the label display type: you can choose to display all, minimum value, maximum value, minimum & maximum values, or both endpoints.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efac367be8864b2e9e1b03202c4b0958~tplv-goo7wpa0wc-image.image) </span>


* Supports selecting the display mode: you can choose single data point, total, or both single data point and total.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d42c4f1445cc499fa6a74e041375c8e3~tplv-goo7wpa0wc-image.image" width="2938px" /></div>


<span id="_3-10-提示信息"></span>
## 3.9 tooltips information

When the mouse hovers over the data area, the tooltips will display information.

By default, the dimensions and metrics of the current data are displayed. You can also customize the tooltips information as needed.

**Default tooltips information**

After enabling tooltips information, you can select "Display content" and choose from three display modes: "Single data point + whole row data", "Single data point only", or "whole row data only".

Note: To display single data point information, you can add fields to the single data point and customize the tooltips information. The added fields will only appear in the tooltips information for single data points and will not be involved in chart rendering.


* Single data point + whole row data

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c610415ced8645bb92f00bb95bd3aec0~tplv-goo7wpa0wc-image.image) </span>

* Single data point only

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69c33eeaa4cd4d8f828dfe33ae586b5f~tplv-goo7wpa0wc-image.image) </span>

* Whole row data only

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94972ec6322741a6819f6de07f81760a~tplv-goo7wpa0wc-image.image) </span>


**Custom tooltips information**

(1) Supports adding other metrics from the dataset to supplement the tooltips information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cdcab6aa1e74cd7b46ccc96904c0d23~tplv-goo7wpa0wc-image.image) </span>

(2) Click the "Advanced settings" button to further configure in the pop\-up edit box[Custom Tooltips Information](https://docs.byteplus.com/docs/DataWind/Custom_Tooltips_Information). Supports entering text and inserting fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13b6e032d4c741519d5713f674780d9b~tplv-goo7wpa0wc-image.image) </span>

After editing text and fields and adjusting the layout, you can achieve a customized effect. Click Preview to preview the effect.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/144284958ee647c484bf277ce420b704~tplv-goo7wpa0wc-image.image) </span>

Click "OK" to apply to the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43603faecf8f4ccda746a3eae23ef7c4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-11-显示模式"></span>
## 3.10 Display mode

Supports modifying the display mode. There are four modes: Standard, Adaptive window, Adaptive width, and Adaptive height.


* Standard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/178e3c470dab4b5ea757ed21942bd9a9~tplv-goo7wpa0wc-image.image) </span>

* Adaptive window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89135b617d304217bfa0f2de2a10c301~tplv-goo7wpa0wc-image.image) </span>

* Adaptive width.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4331d2f595d49b69e3ad477855c48df~tplv-goo7wpa0wc-image.image) </span>

* Adaptive height.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a430b79f414542a5ab12bb8c9bd03d39~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-12-图内控件样式"></span>
## 3.11 In\-chart control styles

See [3.5 Set conditional formatting](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-5-%E8%AE%BE%E7%BD%AE%E6%9D%A1%E4%BB%B6%E6%A0%BC%E5%BC%8F).

<span id="_3-13-恢复默认设置"></span>
## 3.12 Restore default settings

Click [Restore default settings] to restore all settings in the above chart configuration to their default values.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efb3940dabeb4c10bcdccc698a084acb~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-14-透视"></span>
## 3.13 Pivot

See [Pivot Chart](https://docs.byteplus.com/docs/DataWind/Pivot_Chart).
