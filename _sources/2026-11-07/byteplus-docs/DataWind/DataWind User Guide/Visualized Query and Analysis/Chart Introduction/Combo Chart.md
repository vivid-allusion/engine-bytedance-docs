---
title: "Combo Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Combo_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

Combo charts are typically used to compare and display multiple metrics and their changes under a unified dimension. The product's combo chart supports five types of sub\-charts: bar chart (stacked bar chart / grouped bar chart), line chart, area chart, percentage area chart, and dual\-axis chart.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

Combo charts are typically used to compare and display multiple metrics and their changes under a unified dimension.

**Combo chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6beb35c47e3e4077b668f9585910a82e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Set dimensions, metrics, and filter conditions**

Select the "sale_province" as the dimension, and select "sale_price", "price" as metrics;

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d84ddd3911748c6942f2604ba39d966~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select the chart panel \- Combo chart**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ac5160aa05f4778b942b320a3c10173~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Group metrics as needed and modify the chart format**

For example, group the metrics "sale_province" and "sale_price" to create a line chart; group "sale_province" and "price" to create a bar chart.

Note: Dragging a metric capsule to another capsule allows you to combine them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52e63ab74c424e0fb2232554eaca2031~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-组合图图标"></span>
## 3.1 Combo chart icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82ed1d1a039447189336df15e0121cb9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

You can create charts after setting one or more dimensions and one or more metrics.

**Dimension**: Supports one or more dimensions. If there is more than one dimension, the second and subsequent dimensions are displayed according to the style of the selected chart type.

**Metric**: Supports one or more metrics. If there is more than one metric, the second and subsequent metrics are displayed as multiple charts within the combo chart, or multiple metrics can be grouped into a metric set.


* You can configure the chart type for each metric or metric set in the "Combo Chart" options.


<span id="_3-3-指标集"></span>
## 3.3 Metric set

When the composite chart is selected, users can drag and drop multiple indicators to form an indicator set. An indicator set will be displayed as a subplot within the composite chart.

**Indicator set style**: When multiple indicators are combined into an indicator set, the display style will change accordingly.

**Form indicator set**: Drag an indicator capsule onto another indicator or indicator set capsule to create a new indicator set.

<span id="_3-4-编辑颜色"></span>
## 3.4 Edit color

You can assign colors to indicators, and multiple built\-in color schemes are available:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/096b97168897440db27626f3f639c76c~tplv-goo7wpa0wc-image.image) </span>

You can also set the color for each indicator individually.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b8be85e65e44a85a4e5de148c263333~tplv-goo7wpa0wc-image.image) </span>

Also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-5-组合方向"></span>
## 3.5 Combo direction

You can choose either horizontal or vertical orientation. For horizontal combo, the dimension is used as the Y\-axis and the indicator as the X\-axis; for vertical combo, the dimension is used as the X\-axis and the indicator as the Y\-axis.

Horizontal

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e4d482e4514484085bc97e81f4ebcdb~tplv-goo7wpa0wc-image.image) </span>

Vertical

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78675015ba1b44d1badc05c1a6030967~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-组合图表"></span>
## 3.6 Composite chart

You can set the chart type for a single indicator or indicator set as a subplot of the composite chart. Five types of subplots are supported: bar chart, line chart, area chart, percentage area chart, and dual\-axis chart. Among them, bar charts include stacked bar charts and grouped bar charts. Clicking the icon defaults to the stacked bar chart, and you can switch between different bar chart types via the dropdown list.

When the subplot type is set to dual\-axis chart, you also need to configure the primary and secondary Y\-axes, as well as the chart types corresponding to the primary and secondary axes.

<span id="_3-7-线条样式"></span>
## 3.7 Line style

**Line type**: You can choose between polyline and smooth line, adjust the thickness, and select solid, dashed, or dotted lines.

**Marker**: You can choose no marker, hollow circle, solid circle, square, diamond, and select the marker size.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/101e08cfccbf4fe3b6ccb75ec63cdc3c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-排列方式"></span>
## 3.8 Arrangement

**Parallel indicators**:


* The switch is enabled by default.

* For multiple indicators in a subplot, they are displayed according to the subplot's display rules. Refer to the corresponding entry in "Help Center \- Visual Query \- Chart" for details.


<span id="_3-9-x-轴-y-轴"></span>
## 3.9 X\-axis / Y\-axis

<span id="_3-9-1-纵向组合图"></span>
### 3.9.1 Vertical composite chart


* **X\-axis**: You can click the switch button on the right side of the X\-axis to choose whether to display X\-axis information.

   * **Axis name checkbox**: Can be selected or deselected. After selection, the name can be modified. The default is the field name.

   * **Axis name (gray)** : You can set the font size and font color.

   * **Axis label**: You can set the font size, font color, and text angle (0–360 degrees).

   * **Axis line**: You can set the color of the axis line.

* **Y\-axis**: By default, the axis name is displayed. Settings are applied to each sub\-chart.

   * **Axis name checkbox**: Can be selected or deselected. After selection, the name can be modified. The default is the field name.

   * **Axis name (gray)** : You can set the font size and font color.

   * **Axis label**: You can set the font size, font color, and text angle (0–360 degrees).

   * **Axis line**: You can set the color of the axis line.

   * **Axis range**: There are three options: Auto, Auto (excluding 0), and Custom range:

      * Auto: (negative values, 0, positive values), includes 0.

      * Auto (excluding 0).

      * Custom range: You can manually enter the minimum and maximum values. The value on the right must be greater than the value on the left and cannot be empty.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e03a0c5f21964d1a8ee374ed21f72f16~tplv-goo7wpa0wc-image.image) </span>

   * **Data format**: Click to set the label data format of the axis in the pop\-up window. You can set it to number, percentage, per mille, or raw value.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/340de83cb04a4a0e81b88b6c37654469~tplv-goo7wpa0wc-image.image) </span>

   * **Axis scale**: Controls the scale display of the axis. Generally, it is linear, but logarithmic processing is also supported, such as log(base 2), which means taking the logarithm with base 2. This is typically used in scenarios such as operations monitoring where there is a large difference between two metrics on the same axis.


<span id="_3-9-2-纵向组合图"></span>
### 3.9.2 Vertical combo chart

The functions of the X\-axis and Y\-axis are interchangeable. See 3.9.1.

<span id="_3-10-网格线"></span>
## 3.10 Grid lines

See [3.6 Grid lines](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-7-%E7%BD%91%E6%A0%BC%E7%BA%BF).

<span id="_3-11-特殊值"></span>
## 3.11 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-12-图例、标签"></span>
## 3.12 Legend and labels

**Legend:** 


* You can click the switch button on the right to choose whether to display legend information.

* You can set the display position of the legend in the chart: top, bottom, left, or right.

* You can set the legend alignment: align to top/left, center, or align to bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.

* You can set the legend display mode. When there are too many legends, you can choose between a pager or a scrollbar for display.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ed9ec3bcd4c4344840de9f455be40e7~tplv-goo7wpa0wc-image.image" width="2938px" />   </div>
   


**Tags:** 

See [3.8 Legend and labels](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-9-%E5%9B%BE%E4%BE%8B%E3%80%81%E6%A0%87%E7%AD%BE).

<span id="_3-13-提示信息"></span>
## 3.13 Notification message

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

<span id="_3-14-图内控件样式"></span>
## 3.14 Style of in\-chart controls

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-15-恢复默认设置"></span>
## 3.15 Restore default settings

Click [Restore default settings] to reset all the above chart settings to their default values.

<span id="_3-16-透视"></span>
## 3.16 Perspective

See [Pivot Chart](https://docs.byteplus.com/docs/DataWind/Pivot_Chart).
