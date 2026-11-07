---
title: "Sankey Diagram"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Sankey_Diagram"
---

<span id="_1-概述"></span>
# 1. Overview

A Sankey diagram, also known as a Sankey energy balance diagram, is a specific type of flowchart. Data flows from nodes on the left to nodes on the right, with the height of each node representing the magnitude of the data; the width of each link is proportional to the flow value—the wider the link, the greater the flow. Sankey diagrams are used to illustrate the distribution of flows and compare structures, and are commonly applied in data visualization analyses in fields such as energy, material composition, and finance.

**Node**: The "rectangular" part in the diagram, as shown below. Nodes represent different categories, which are the dimensions of the visualization query.

**Link**: The flow line connecting nodes. The thickness of the flow line reflects the magnitude of the flow, which is the metric used in the visualization query.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62fdfb1101944e13bcde8fc096acf8c9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

Sankey diagrams are typically used for data visualization analyses involving flow relationships, such as population migration between different countries or the destinations of product sales and more.

**Sankey diagram example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46637f817a9d4343892dfc777b332181~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Set dimensions, metrics, and filter conditions**

The first step in using a Sankey diagram is to set the dimensions, metrics, and filter conditions for the diagram. Dimensions correspond to the nodes in the Sankey diagram, and metrics correspond to the thickness of the links.

For example, we want to visualize the following sales data table as a Sankey diagram in order to observe the regional flow of sales amounts.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29df1c70ffec483a949dcf7d95af2d66~tplv-goo7wpa0wc-image.image" width="615px" /></div>


Select the dimensions: country, region, and province/autonomous region. These correspond to the three columns of nodes in the Sankey diagram.

Select the metric: sales amount (sum), which corresponds to the links in the Sankey diagram.

**Step 2: Draw the Sankey diagram**

The Sankey diagram is drawn as follows: the links connect the nodes "from country to region" and "from region to province/autonomous region", representing the proportion of "national sales amounts flowing to each region" and "regional sales amounts flowing to each province" respectively. The thickness of the links indicates the amount of sales.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adcebaa42acf4056bd84c8218200d44f~tplv-goo7wpa0wc-image.image) </span>

**Highlight flow paths and display data results**

When the mouse hovers over any node or path, a data tooltip is displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5904c6399f384b38bbf4528aeed8802b~tplv-goo7wpa0wc-image.image) </span>

When a traffic path is clicked, that path is highlighted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb644013a77c44c6a0ad2023063d0656~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-桑基图图标"></span>
## 3.1 Sankey diagram icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c21ff674343d4e6d98b683e543d56e80~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

The Sankey diagram supports two or more dimensions and one metric.

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit colors

The Sankey diagram supports custom color settings, and the product includes multiple built\-in color schemes.

<span id="_3-4-线条样式"></span>
## 3.4 Line styles

The links in the Sankey diagram support both curved and straight line styles, which can be selected as needed. The product uses the curved style by default.

**Curved line example:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44d177e9e25346f1aee970d6a1dbcec2~tplv-goo7wpa0wc-image.image) </span>

**Straight line example:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe6d362da1774b53a3c8b8b42c76dec5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-维度标签"></span>
## 3.5 Dimension labels

Dimension labels can be enabled, and alignment styles can be set.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e522cd3a75f46f0860f17e4759401e4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-图例、标签"></span>
## 3.6 Legend and labels

**Legend:** 


* You can choose whether to display legend information. Click the switch button on the right to configure.

* You can set the legend's display position in the chart to the top, bottom, left, or right.

* You can set the legend's alignment to top/left alignment, center alignment, or bottom/right alignment.

* You can set the maximum number of legend rows or columns, as well as the font and color.

* You can set the legend's display mode. When there are too many legend items, you can choose between pagination or a scrollbar for display.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/496da1b4d3c74d68b6074466d8208308~tplv-goo7wpa0wc-image.image) </span>

**Labels:** 


* Users can choose whether to display labels. After enabling labels, they appear on the top layer of the chart, and metric values are shown on the chart.

* The "Allow overlap" feature is disabled by default. When enabled, label display is not restricted by spacing, which may result in overlapping labels.


Caution: Only one of "Sparse display" or "Allow overlap" can be selected as the display mode. If one is selected, the other is grayed out, with a prompt stating "Allow overlap and sparse display cannot be selected at the same time." When label display is crowded by default, it is recommended to select "Sparse display."


* Users can customize the font size and color of labels.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cdec33adb97c43358359c4cb998ce3cb~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-7-图内控件样式"></span>
## 3.7 In\-chart control styles

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-8-恢复默认设置"></span>
## 3.8 Restore default settings

Click [Restore Default Settings] to restore all content in the above chart configuration to its default settings.
