---
title: "Area Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Area_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

An area chart plots data arranged in worksheet rows or columns as points on the chart, connects them with straight lines, and displays the result as a filled area. An area chart is similar to a line chart, but the difference is that an area chart fills the space between the line and the X\-axis with color. It is suitable for illustrating data trends and the contribution of parts to the whole. The product provides both area charts and percentage area charts.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

An area chart emphasizes the magnitude of value changes over time or by category. It can also show the trend of parts within the whole, drawing attention to the overall trend. For example, changes in sales in different regions over time.

**Area chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a748471c3c041cba0ed5e12d76da097~tplv-goo7wpa0wc-image.image) </span>

**Percentage area chart example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/656ec6f3e2294097af12c46454531c83~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Set dimensions, metrics, and filter conditions**

Select [Date] and [Region] as dimensions; [Brand sales volume] as a metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9e6ae4ed699482b9d5bddc7e9188206~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Select Area Chart from the chart panel**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e4b1affdc9f45ec98680cb9d4c3de60~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/368e956a1aac47d3b1a4ac89ba0bebaf~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-面积图图标"></span>
## 3.1 Area chart icon

Click the triangle under Area Chart to switch between "Area Chart" and "Percentage Area Chart".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ed0c6ba457a48ba90cc3cf964cfee62~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

Both chart types support plotting after setting one or more dimensions and one or more metrics. In general, there are no more than two metrics.

<span id="_3-2-1-面积图"></span>
### 3.2.1 Area chart

**Dimension**: Supports one or more dimensions. If there is more than one dimension, the second and subsequent dimensions are displayed as stacked areas, distinguished by different colors.

**Metric**: Supports one or more metrics, typically one metric. If there is more than one metric, the second and subsequent metrics are displayed as stacked areas, distinguished by different colors.

**Example 1**: 1 dimension, 1 metric

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc467a3269d84232b2e87dc489db35fc~tplv-goo7wpa0wc-image.image) </span>

**Example 2**: 2 dimensions, 1 metric

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f1385739f484f7ba63f9fd24deb47a2~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-百分比面积图"></span>
### 3.2.2 Percentage area chart

**Dimension**: Supports one or more dimensions, typically multiple dimensions. If there is more than one dimension, the second and subsequent dimensions will be stacked on the bars and distinguished by different colors.

**Metrics**: Supports one or more metrics, typically one metric. If there is more than one metric, the second and subsequent metrics will be stacked and distinguished by different colors.

**Percentage stacking**: The sum of the area stacks for the first dimension is 100%.

**Example 1**: One dimension, two metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0f400f1d6684206af2f596033649d67~tplv-goo7wpa0wc-image.image) </span>

**Example 2**: Two dimensions, one metric

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88666d9ba8c94f7b8d66e6e1309964e5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-图内控件样式"></span>
## 3.3 In\-chart control styles

In\-chart controls include: filters, dynamic dimensions/metrics, and in\-chart parameters. You can configure their styles.

For example: arrange the title of the dynamic metric control style vertically; set the layout to "medium".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/825c6a8ce39340e69b6a06b7d129e3b5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-编辑颜色"></span>
## 3.4 Edit colors

You can set colors for the area chart. Multiple color schemes are built into the product.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a4af9aae1964ee89ca4c14152619454~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-5-线条样式"></span>
## 3.5 Line styles

**Scope of effect**: You can set different display styles for a specified data series.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0eb80f455104be0a2062238667ac0ab~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is supported in version V2.42 and later.</div>


**Line type**: You can choose between straight or smooth lines, set the line thickness, and select solid, dashed, or dotted lines.

**Marker**: You can choose no marker, hollow circles, solid circles, squares, diamonds, and select the marker size.

<span id="_3-6-x-轴-y-轴"></span>
## 3.6 X\-axis/Y\-axis

See [3.5 X-axis/Y-axis](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-6-x-%E8%BD%B4-y-%E8%BD%B4).

<span id="_3-7-网格线"></span>
## 3.7 Grid lines

See [3.6 Grid lines](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-7-%E7%BD%91%E6%A0%BC%E7%BA%BF).

<span id="_3-8-特殊值"></span>
## 3.8 Special values

See [3.7 Special values](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-8-%E7%89%B9%E6%AE%8A%E5%80%BC).

<span id="_3-9-图例、标签"></span>
## 3.9 Legend and labels

**Legend:** 


* You can click the switch button on the right to choose whether to display legend information.

* You can set the legend's display position in the chart: top, bottom, left, or right.

* You can set the legend's alignment: align to top/left, center, or bottom/right.

* You can set the maximum number of legend columns, as well as the font and color.

* You can set the legend display mode. When there are too many legend items, you can choose between a pager or a scrollbar for display.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d03b006b0eb04168a970138f9e270788~tplv-goo7wpa0wc-image.image) </span>

**Labels:** 

See [3.8 Legend and labels](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-9-%E5%9B%BE%E4%BE%8B%E3%80%81%E6%A0%87%E7%AD%BE).

<span id="_3-10-提示信息"></span>
## 3.10 Tooltips

See [3.9 tooltips information](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-10-%E6%8F%90%E7%A4%BA%E4%BF%A1%E6%81%AF).

<span id="_3-11-显示模式"></span>
## 3.11 Display mode

See [3.10 Display mode](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-11-%E6%98%BE%E7%A4%BA%E6%A8%A1%E5%BC%8F).

<span id="_3-12-恢复默认设置"></span>
## 3.12 Restore default settings

Click [Restore Default Settings] to revert all the above chart configuration items to their default values.

<span id="_3-13-透视"></span>
## 3.13 Pivot

See [Pivot Chart](https://docs.byteplus.com/docs/DataWind/Pivot_Chart).
