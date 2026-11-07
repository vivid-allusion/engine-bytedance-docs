---
title: "Histogram"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Histogram"
---

<span id="_1-概述"></span>
# 1. Overview

A histogram represents data distribution using a series of rectangles or line segments of varying heights. In a Cartesian coordinate system, the horizontal axis marks the endpoints of each group, the vertical axis represents the frequency, and the height of each rectangle corresponds to the respective frequency. The product provides a histogram component with multiple configuration options, allowing you to select different display content and histogram types.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

Histograms are suitable for displaying two\-dimensional datasets, enabling the identification of data patterns and providing an intuitive visualization of data distribution.

**Histogram example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a0867a1ec784f7fb2249ebafe42a0f5~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Usage process example

**Step 1: Set dimensions and filter conditions**

Step 2: Select one numerical dimension "Purchase Amount"; filter p_date to include only the most recent day

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adf54e3765844a169c194d3df9f68433~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Select the chart panel \- Histogram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cb622613d5d4f979be6570d64d71e80~tplv-goo7wpa0wc-image.image) </span>

**Step 4: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/965d013facaf4fc8ae7484775e2ab9ef~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-直方图图标"></span>
## 3.1 Histogram icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8f1d30603b446b58cb9dd6986e8eafd~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

Select one numerical dimension and zero metrics

<span id="_3-3-编辑颜色"></span>
## 3.3 Edit colors

You can set the colors of the bars and lines, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/201635f4f3fe45f880d82381cac334c7~tplv-goo7wpa0wc-image.image) </span>

It also supports [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-4-直方图配置"></span>
## 3.4 Histogram configuration


* **Data range:**  Number of data points to filter. For example, if metric A has 100 values and you select 0\-90%, the first 90 data points will be used for plotting

* **Number of bins:**  Number of groups for data on the X\-axis

* **Display content:**  Three options: default, value, and proportion. Selecting value displays only the frequency, selecting proportion displays only the proportion, and selecting default displays both value and proportion

* **Histogram type:**  Two options: frequency and cumulative


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1236927bb7045409b1b28cc7eaf2ac7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7f778514a664e7dab32d7d475ecb339~tplv-goo7wpa0wc-image.image) </span>

For example, if you change the data range to 0\-95%, the first 95% of the data will be used; if you select 5 bins, there will be only 5 data groups on the X\-axis; if you select the cumulative histogram, both value and proportion are calculated cumulatively, as shown below

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8807ef58b5b4261a4ed13771c09e497~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-图内控件样式"></span>
## 3.5 In\-chart control styles

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-6-恢复默认设置"></span>
## 3.6 Restore default settings

Click [Restore Default Settings] to revert all the above chart configuration items.
