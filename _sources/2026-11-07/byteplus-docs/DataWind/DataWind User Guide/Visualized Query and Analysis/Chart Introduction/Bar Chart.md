---
title: "Bar Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Bar_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

A bar chart is a statistical chart that displays data using the length of bars as variables, typically used to show changes in data over different periods or under different conditions. The product provides three types of components: grouped bar chart, stacked bar chart, and percentage bar chart.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/63dc4a6ede0f4f758ec7345e5e42b8d1~tplv-em5hxbkur4-noop.image?width=2236&height=414) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
### 2.1 Common use cases

Bar charts are typically used to show changes in data over different periods or under different conditions, allowing for a clear comparison of differences between data groups.

Consider using a bar chart in the following situations.


* The dimension field names are relatively long. Using a bar chart allows dimension names to be displayed more completely.

* There are many dimension categories. When the chart height is not limited, using a bar chart provides a more visually appealing layout.


<span id="_2-2-使用过程示例"></span>
### 2.2 Example usage process

**Step 1: Set dimensions, metrics, and filter conditions**

Select [Province] as the dimension and [order_count] as the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcabacb8542043ae81e786ed186bea36~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- Bar chart**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23412e39a2c0493289daa4dd32dcda8b~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87c5b813191b436ab554c173250650e8~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-条形图图标"></span>
## 3.1 Bar chart icons

Three types of bar charts are supported. Click the small triangle under the bar chart icon to switch between them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0defca5e611c4f5cb42198862675d71d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-1-并列条形图"></span>
### 3.1.1 Grouped bar chart

Supports one or more dimensions and one or more metrics. If there is more than one dimension or metric, they will be displayed side by side in the bar chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed2628a62db04e718be9b70cceb82471~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-堆叠条形图"></span>
### 3.1.2 Stacked bar chart

Dimensions: Supports one or more dimensions. If there is more than one dimension, they will be stacked within the bars and distinguished by different colors.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/175af7498d314b04b8a44663f1af1e86~tplv-goo7wpa0wc-image.image) </span>

Metrics: Supports one or more metrics. If there is more than one metric, they will be displayed separately along the x\-axis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd06738ed94f4325a5cb913dc470ae6d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-3-百分比条形图"></span>
### 3.1.3 Percentage bar chart

Dimensions: Supports one or more dimensions. If there is more than one dimension, they will be stacked within the bars and distinguished by different colors. Each bar represents 100%.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/781ecb30d1694460b6e2c87b01508fcf~tplv-goo7wpa0wc-image.image) </span>

Metrics: Supports one or more metrics. If there is more than one metric, by default they will be displayed separately along the x\-axis. The sum of the bars for each dimension is 100%.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db84e63c1dc44905a1ab35ca06a43198~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

You can set one or more dimensions and one or more metrics before generating a chart.

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit color

You can set colors for the bar chart as needed, and the product provides multiple built\-in color schemes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27725a111d60413cbcf0ea51a815f45c~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-4-排列方式"></span>
## 3.4 Arrangement method

This feature applies to stacked bar charts and percentage bar charts, allowing you to choose whether to enable metric juxtaposition.


* When metric juxtaposition is enabled, multiple metrics are displayed side by side in clusters by default, with different colors for distinction.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b5711ffea1d421fb930fec9dc9cae87~tplv-goo7wpa0wc-image.image) </span>

* When metric juxtaposition is disabled, multiple metrics and dimensions are stacked together, with different colors for distinction.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a30748a1b330461384db62b9fa674c78~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-5-x-轴-y轴"></span>
## 3.5 X\-axis / Y\-axis


* **X\-axis / Y\-axis**: You can click the toggle button on the right side of the X\-axis/Y\-axis to choose whether to display X\-axis/Y\-axis information.

* **Axis name checkbox**: You can check or uncheck it. After checking, you can modify the name, which defaults to the field name.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis label**: You can set the font size, font color, and text angle (0–360 degrees).

* **Axis line**: You can set the color of the axis line.

* **Thumbnail**: It can be used to zoom the chart horizontally or vertically. When the X\-axis thumbnail is enabled, and the Y\-axis value range is set to auto and the data format is set to auto, adjusting the thumbnail range will dynamically update the Y\-axis labels.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72f7f983f50b4695809497b6e1c6df9e~tplv-goo7wpa0wc-image.image) </span>

* **Number axis range (this setting is only available for the X\-axis)** : There are three options: Auto, Auto (excluding 0), and Specified range:

   * Auto: (negative values, 0, positive values), includes 0;

   * Auto (excluding 0);

   * Specified range: You can manually enter the minimum and maximum values. The value on the right must be greater than the value on the left and cannot be empty.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e95db4f09559490fa61052bb6b31ac19~tplv-goo7wpa0wc-image.image) </span>

* **Data format (this setting is only available for the X\-axis)** : Click to set the label data format of the number axis in the pop\-up window. You can set it to number, percentage, per mille, or raw value.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1601a52691343d7b8647bab1cfb1423~tplv-goo7wpa0wc-image.image) </span>

* **Axis scaling (this setting is available only for the X axis)** : Controls the scale display of the axis. By default, it is linear, but logarithmic scaling is also supported, such as log(base 2), which means using base 2 for the logarithm. This is generally used in operations monitoring scenarios where the values of two metrics on the same axis differ significantly.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13efe7e8a17249e690858eaf21a69b6f~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-6-网格线"></span>
## 3.6 Grid lines

See [3.6 Grid lines](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-7-%E7%BD%91%E6%A0%BC%E7%BA%BF).

<span id="_3-7-特殊值"></span>
## 3.7 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-8-图例、标签"></span>
## 3.8 Legends and labels

**Legend:** 


* You can click the toggle button on the right to choose whether to display the legend information.

* You can set the legend's position in the chart: top, bottom, left, or right.

* You can set the legend's alignment: align to top/left, center, or bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.

* You can set the legend's display mode. When there are too many legend items, you can choose between a pager or a scrollbar for display.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69ee4e53f7ea46ab82cff1b20f0af792~tplv-goo7wpa0wc-image.image" width="2938px" /></div>


**Label:** 


* You can click the toggle button on the right to choose whether to display label information. The display mode supports single data point or total.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/830e7c8a68b94162ad9b097e41d0a27f~tplv-goo7wpa0wc-image.image) </span>


* Both default and custom styles are supported.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38d6b20bb33b4dd9aae4f7f1ea4aa4bd~tplv-goo7wpa0wc-image.image) </span>


* Custom styles support setting the display position.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5c3028c59f543a0b8689a136672898c~tplv-goo7wpa0wc-image.image) </span>


* Custom styles support setting the display mode.


Caution: Only one of "Sparse display" or "Allow overlap" can be selected. If one is selected, the other will be grayed out, with a prompt stating "Allow overlap and sparse display cannot be selected at the same time." When labels appear crowded by default, it is recommended to select "Sparse display."

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ca187a503e44324b71674b7e308ac51~tplv-goo7wpa0wc-image.image) </span>


* Custom styles support setting the label font and color.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c77f29e036ab467080293939a55f5409~tplv-goo7wpa0wc-image.image) </span>


* You can set the display content.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51d0421f0ca146e99165b6bac2f72a13~tplv-goo7wpa0wc-image.image) </span>

Caution: The percentage data format, default percentage value, and historical data can be set to two decimal places.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e66984b660744156a3ce82565af91502~tplv-goo7wpa0wc-image.image) </span>


* You can set the label display type: choose to display all, minimum value, maximum value, both minimum and maximum values, or both endpoints.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f341bdc620d4effae7516318e3893cd~tplv-goo7wpa0wc-image.image) </span>


* You can select the display mode: single data point, total, or both single data point and total data. (Supported chart types: stacked bar chart, percentage bar chart)


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c336228bf5f428ea6c7b3c3ce371d7f~tplv-goo7wpa0wc-image.image" width="2938px" /></div>


<span id="_3-9-提示信息"></span>
## 3.9 Tooltips information

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

<span id="_3-10-显示模式"></span>
## 3.10 Display modes

See [3.10 Display mode](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-11-%E6%98%BE%E7%A4%BA%E6%A8%A1%E5%BC%8F).

<span id="_3-11-图内控件样式"></span>
## 3.11 In\-chart control styles

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-12-恢复默认设置"></span>
## 3.12 Restore default settings

Click [Restore Default Settings] to restore all of the above chart settings to their default values.

<span id="_3-13-透视"></span>
## 3.13 Pivot

See [Pivot Chart](https://docs.byteplus.com/docs/DataWind/Pivot_Chart).
