---
title: "Waterfall Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Waterfall_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

Waterfall charts are suitable for illustrating the quantitative changes between several specific values. The product supports two types of charts: proportion waterfall plots and change waterfall charts.


* **Proportion waterfall plot**


Displays the overall structure or sequential changes. Data is presented through the vertical height of bars, providing an intuitive view of the composition of metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56f9ccc0718747ccbb1adae4a25f8d98~tplv-goo7wpa0wc-image.image) </span>


* **Change waterfall chart**


Clearly reflects the process by which a data point becomes another after a series of increases and decreases. Intuitively breaks down the contribution of dimension breakdowns to the fluctuation of a specific metric. The chart includes an initial value and a final value. Intermediate values are floating bars, with colors distinguishing the positive and negative impacts of specific dimensions on metric fluctuations. This allows for quick differentiation between positive and negative values.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2b0b5724f3c4fe98cfb8a1342936b16~tplv-goo7wpa0wc-image.image) </span>

**Common application scenarios:** 


* Analyze the proportion of expenditures in each region

* Analyze the impact of each region on annual product profit fluctuations


<span id="_2-快速入门"></span>
# 2. Quick start

**Step 1:**  Set the metrics to display and the filter criteria.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36deb6ec0ba440f5b2f84103f21e1763~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  In the chart type menu, select proportion waterfall plot; or hover the mouse over the waterfall chart and select change waterfall chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bec6271c6714dd8b1b89b7afc97bc83~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  If change waterfall chart is selected, specify the dimension breakdowns in the style settings below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a9ca977ebd74ddc9c6ef7493ddc745b~tplv-goo7wpa0wc-image.image) </span>

**Step 4:**  Modify and adjust the chart format as needed.

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-瀑布图图标"></span>
## 3.1 Waterfall chart icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82a954c0d610455f9d20634daad71482~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

The proportion waterfall plot supports one dimension and one metric.

The change waterfall chart supports two dimensions and one metric.

<span id="_3-3-细分维度设置"></span>
## 3.3 Dimension breakdown settings

For change waterfall charts, after selecting the metric, the start and end values of the change waterfall chart can be confirmed. On this basis, users still need to select the dimension breakdowns to observe their contribution to metric fluctuations. For example, to view the fluctuation of sales revenue in each region from the beginning to the end of the year, select region as the dimension breakdown.

Users can drag dimensions to the dimension breakdown field and specify how many dimension breakdowns to display.

As in the example above, if there are a total of 10 regional detail values in the system and the maximum number of subdivided dimension items is set to 3, only the top three dimensions with the largest fluctuation contribution (absolute value) will be displayed, while the remaining ones will be grouped together under a dimension named 'Other'.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a9ca977ebd74ddc9c6ef7493ddc745b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-编辑颜色"></span>
## 3.4 Edit colors

Custom color settings are supported.

For proportion waterfall plots, you can adjust the colors of the bars for increase, decrease, and total.

For change waterfall charts, you can adjust the colors of the bars for increase, decrease, other, and dimension items.

<span id="_3-5-x-轴-y-轴"></span>
## 3.5 X axis/Y axis


* **X axis / Y axis**: You can click the toggle button on the right side of the X axis/Y axis to choose whether to display the X axis/Y axis information.

* **Axis name checkbox**: You can check or uncheck it. After checking, you can modify the name, which defaults to the field name.

* **Axis name (gray)** : You can set the font size and font color.

* **Axis label**: You can set the font size, font color, and text angle (0\-360 degrees).

* **Axis line**: You can set the color of the axis line.

* **Data zoom**: Can be used to zoom the chart horizontally or vertically.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7740f1972df24be2a57cd08c41f83228~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-网格线"></span>
## 3.6 Grid lines

You can enable grid lines to assist in observing values. Both horizontal and vertical display are supported, and the grid line style can also be adjusted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04d35e085d8d4e25b3f8fc09c3325215~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-7-特殊值"></span>
## 3.7 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-8-标签"></span>
## 3.8 Labels


* You can click the toggle button on the right to choose whether to display label information.

* Labels will appear at the top layer of the chart. After enabling label display, the metric values will be shown on the chart.

* You can set the label display mode: single data point or total.

* You can customize the label style, including display position, display mode, label font and color, and display content.


Note: Only one of 'Sparse display' or 'Allow overlap' can be selected for the display mode. If one is selected, the other will be grayed out, with a prompt stating 'Allow overlap and sparse display cannot be selected at the same time.' When labels are crowded by default, it is recommended to select 'Sparse display.'


* You can set the label type: all, minimum value, maximum value, minimum & maximum value, or both ends.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42ac1a2b1fd24e35ae301f90688eadd4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-9-图内控件样式"></span>
## 3.9 In\-chart control styles

The controls within the chart include: filters, dynamic metrics and metrics, and in\-chart parameters. For more information, see [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-10-恢复默认设置"></span>
## 3.10 Restore default settings

Click [Restore default settings] to restore all of the above chart configuration settings to their default values.
