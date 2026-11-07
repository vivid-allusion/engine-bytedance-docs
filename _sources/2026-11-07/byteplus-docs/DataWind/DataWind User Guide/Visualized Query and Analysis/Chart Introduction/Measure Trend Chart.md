---
title: "Measure Trend Chart"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Measure_Trend_Chart"
---

<span id="_1-概述"></span>
# 1. Overview

The measure trend chart enables the simultaneous display of multiple measure data and their trend changes over a specified time period.

<span id="_2-快速入门"></span>
# 2. Quick start

(1) Select a date dimension, one or more measures, and configure the required filter conditions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15368f6c9b834c31a5c7be8886747969~tplv-goo7wpa0wc-image.image) </span>

(2) Select measure trend chart as the chart type.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8442f12ab0e9424f9d89ca4aede1b257~tplv-goo7wpa0wc-image.image) </span>

(3) Configure the basic settings, measure format, and trend chart format, and select the desired measure trend chart type.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/179f68fc84ed4f688be24e15d12693cc~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-指标趋势图维度和指标要求及配置"></span>
## 3.1 Requirements and configuration for measure trend chart dimensions and measures

The measure trend chart requires one date\-type dimension and one or more measures.

In the measure bar, you can drag one measure capsule onto another to merge two measure capsules. The former will serve as the primary measure of the measure card, and the latter as the secondary measure. Merging multiple measures simultaneously is supported.

<span id="_3-2-基础设置"></span>
## 3.2 Basic settings

<span id="_3-2-1-指标默认取数"></span>
### 3.2.1 **Default measure value**

The measure card value in the measure trend chart can be set to display either the latest date data or the period summary data (by default, it displays the latest date data).

Latest date data: The measure card displays the data for the most recent date within the currently selected time range

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3644aff3b264070bc37900a3a48b2ae~tplv-goo7wpa0wc-image.image) </span>

Period summary data: The measure card displays the summary of all data within the currently selected time range.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15397c385ec64bf798727c68200c3807~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-每行最多显示"></span>
### 3.2.2 **Maximum per row**


* You can set the number of measure cards displayed per row in the measure trend chart

* You can view measures in other rows by clicking the pagination button on the right side of the measure card


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c9d634f70804d0abd2e97d917688c21~tplv-goo7wpa0wc-image.image) </span>


* You can adjust the measure spacing mode


When the second format is selected for the measure trend chart and the small trend chart is set to display below the measure, the chart will display in multiple rows according to the maximum number of measures per row.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/448ae2fc9c954b3bbd2c7d98efe1f1bf~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-3-指标间距模式"></span>
### **3.2.3 measure spacing mode**

The measure trend chart supports adjusting the spacing between measures.


* Compact mode:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e31494dbcbb4408c9566990df741586a~tplv-goo7wpa0wc-image.image) </span>


* Standard mode:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed073932e4254d9ba322eb01b1a72327~tplv-goo7wpa0wc-image.image) </span>


* Relaxed Mode:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71a76c113939435dae0838f62b2c588e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-4-基本格式"></span>
### 3.2.4 Basic layout

The measure trend chart supports adding row dimensions. The basic layout supports both tiled and tree views.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb6d28483a204f7a9b83734c77af4278~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-指标样式"></span>
## 3.3 Measure formats

The measure format supports adjusting the font size and color of the measure name and measure value for both primary and secondary measures within the measure card.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dbc9cb705284de5aaa9185a1567d4de~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-条件格式"></span>
## 3.4 Conditional formatting

The measure trend chart supports setting conditional formatting for measure cards within the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b28dfab061a4a9db42d9ea5f30ac3a6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-趋势图样式"></span>
## 3.5 Trend chart format

<span id="_3-5-1-展示样式"></span>
### 3.5.1 **Display format**

**measure trend chart**

In the measure trend chart, measures are displayed at the top, and the trend chart for each measure is shown below. Clicking the corresponding measure card switches the measure displayed in the trend chart below, and the background of the selected measure card will be highlighted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88d04eb52cbf4f59b5ed7a5b2ea174b0~tplv-goo7wpa0wc-image.image) </span>

**measure + mini trend chart:** 

In this trend chart format, measure cards are displayed at the top, and below each measure card, a thumbnail trend chart for the corresponding measure is shown. When the mouse moves to a specific time point for an measure, the data displayed on the measure card will update in real time to show the measure data for the current time point.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a73b3c58cc7642e59aa7100d0d086264~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-2-图表类型"></span>
### 3.5.2 **Chart type**

Supports switching the chart type of the trend chart in the measure trend chart. Line chart, bar chart, and area chart are supported (the default is line chart).

Column chart:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/024da1d90a6245a6837b57c71e325ce4~tplv-goo7wpa0wc-image.image) </span>

Area chart:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6f1349f0e944c928811601545ec21d9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-3-小趋势图位置"></span>
### 3.5.3 **Mini trend chart position**

This option can only be selected when the display format is set to measure + mini trend chart. You can choose the position of the mini trend chart (the default is below the measure).

Effect when selecting the right side of the measure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b66c388c98740de812696562368bbfd~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-4-指标趋势显示"></span>
### 3.5.4 **measure trend display**

Supports switching the measure trend display to show only primary measures or all measures.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8db5080ad43742b7ab7247deac668309~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-线条样式"></span>
## 3.6 Line style

Supports selecting the scope of application for line format configuration, line type (including line type, thickness, and solid or dashed lines), and marker format.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe887fd3b2c34575ae6b6d97f4fa86d3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-7-编辑颜色"></span>
## 3.7 Color editing

The color editing feature supports editing the line color of the trend chart in the measure trend chart. Multiple system color schemes are supported, as well as custom color schemes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c61a056661084572813e43da02830ae0~tplv-goo7wpa0wc-image.image) </span>

It can also support [Custom Color Schemes](https://docs.byteplus.com/docs/DataWind/Custom_Color_Schemes).

<span id="_3-8-图内控件样式"></span>
## 3.8 In\-chart control format

See [3.11 In-chart control styles](https://docs.byteplus.com/docs/DataWind/Column_Chart#_3-12-%E5%9B%BE%E5%86%85%E6%8E%A7%E4%BB%B6%E6%A0%B7%E5%BC%8F).

<span id="_3-9-恢复默认设置"></span>
## 3.9 Restore default settings

Click [Restore default settings] to restore all settings in the above chart configuration to their default values.
