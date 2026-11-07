---
title: "Measure Targets"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Measure_Targets"
---

In the dataset module, it is possible to create OKR tables and use visualization query capabilities to analyze and view the monthly, quarterly, and annual target completion rates of business indicators. The indicator targets feature is used to configure target data for the indicators in the OKR table. This article describes how to configure indicator targets.

<span id="2a26759c"></span>
# Prerequisites

The user's account must have dataset editing permissions to **configure indicator targets**.

<span id="_1-概述"></span>
# Feature overview

The indicator targets feature mainly involves the following two configuration steps:


* Target value configuration

* Target completion rate configuration


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/782a92265afa4a9a961e607ba5eb4de7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8351a323e3349e0862138d3e4e84473~tplv-goo7wpa0wc-image.image) </span>

After configuring indicator targets, the OKR table will appear.

<span id="_2-快速入门"></span>
# Quick start


1. In the dataset module, in the upper\-right options of the dataset directory or dataset details page, select "Indicator targets" from the More menu.

   
   |Dataset directory entry |Dataset details page entry |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68a3f3c0c8a44dfb830a23480fa75a9e~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58cb0e04de494e73a5e7b5e34b631743~tplv-goo7wpa0wc-image.image) </span> |
   

2. In the pop\-up window for configuring indicator targets, click "Add indicator target configuration", then select the indicator for which you want to configure a target.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e9f0ecd17134255a9cf8a2a349561db~tplv-goo7wpa0wc-image.image) </span>

   * It is possible to add indicator targets for multiple indicators, but each indicator can only have one indicator target.

3. Select the type of target to configure, including monthly, quarterly, or annual targets.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8016e91834c24ffc908bc1bc83440dee~tplv-goo7wpa0wc-image.image) </span>


4. Here, as an example, configure a target value for Q2 of 2025 as a quarterly target. Select the calculation method for target completion rate, data format, and conditional format, then click Save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e00dad8bc9894f7181173815d3d04524~tplv-goo7wpa0wc-image.image) </span>


5. In the visualization query, you can use the OKR table to view target completion rates.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44ac074c065e404c8d99eeb21f5f8312~tplv-goo7wpa0wc-image.image" width="569px" /></div>


<span id="8df40c41"></span>
# Configure target values

<span id="7285a6e8"></span>
## **Configure target value granularity**

The following granularities are currently supported for target value configuration:


|Monthly target |Quarterly target |Annual target |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3ead6cfa864494cabc2990defd97e07~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ece6cea45ad74a1b9e4dc301fb485303~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7db389c2ac464aba845603e92efa1eb3~tplv-goo7wpa0wc-image.image) </span> |


Year, quarter, and month are sorted in descending order by default. For monthly targets, both the current year and the next year support filtering by the whole year, the first half, or the second half of the year.

<span id="b16f5ff8"></span>
## **Configure target value data format**

It is possible to configure the data format for target values. The configured data format will affect how target values are displayed in the OKR table. For details, see [2.2 Set data format](https://docs.byteplus.com/docs/DataWind/Metric_Field_Configuration#_2-2-%E8%AE%BE%E7%BD%AE%E6%95%B0%E6%8D%AE%E6%A0%BC%E5%BC%8F). The data formats for target values of different granularities are independent and can be configured separately.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f75addbafd424643a90bf9b1cddff7ab~tplv-goo7wpa0wc-image.image) </span>

<span id="4753ad05"></span>
## **Target value configuration scope**

Currently, target value configuration is supported from January 2020 to December of the second year after the current time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c578d6d422341d484995eb710d112a0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-目标值完成度"></span>
# Configure target completion rate

<span id="29a3baef"></span>
## **Configure calculation method**

It is possible to set the calculation time range and calculation method for target values. The following table shows the calculation methods that can be set for different time granularities:


|Different OKR granularities |Available time ranges |Calculation formula |Calculation method |
|---|---|---|---|
|Month |Past day, past 7 days, past 30 days, current month (the month in which the end date falls) |Cumulative value/target value<br><br>Target value/cumulative value (negative indicator)<br><br>2 \- (cumulative value/target value) (negative indicator)<br><br>Daily average value/target value<br><br>Daily average value \- target value<br><br>Indicator value \- target value |Daily sum (applicable to cumulative indicators such as revenue) |
|Quarter |Past day, past 7 days, past 30 days, current month (the month in which the end date falls), current quarter ||Unique count within the overall date range (applicable to indicators such as customer count) |
|Year |Past day, past 7 days, past 30 days, current month (the month in which the end date falls), current quarter, current year ||Automatic (applicable to ratio\-type indicators such as profit margin) |


**Example**

The current target completion rate is set as shown in the figure below. The calculation method for quarterly targets is the cumulative value of the last 7 days divided by the target value, calculated by summing daily values.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fec74806bcf946fe993251691118763d~tplv-goo7wpa0wc-image.image) </span>

At this time, the target completion rate for the most recent quarter in the OKR table is the sum of income for the last 7 days up to the deadline divided by the target value, that is, the sum of income during 20250528–20250603 divided by the target value.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9de4ffd791c94ede8965a6c404377547~tplv-goo7wpa0wc-image.image) </span>

Since the calculated value at this time is not the target completion rate of the most recent quarter, the column name can be modified to a more appropriate name.

<span id="4890018a"></span>
## **Configure data format**

It is possible to configure the data format for the target completion rate, which will affect how the target completion rate is displayed in the OKR table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55621e1698ad4f22b59737386e921c77~tplv-goo7wpa0wc-image.image) </span>


* Data format: It is possible to set the value of the target completion rate as a number, percentage, per mille, raw value, PP, or customize it based on the data. For details, see [2.2 Set data format](https://docs.byteplus.com/docs/DataWind/Metric_Field_Configuration#_2-2-%E8%AE%BE%E7%BD%AE%E6%95%B0%E6%8D%AE%E6%A0%BC%E5%BC%8F).


<span id="954870c9"></span>
## **Configure conditional formatting**

It is possible to configure conditional formatting for the target completion rate, which will affect the icon display style of the target completion rate in the OKR table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fca7f7b11be4d9c885233ea69f032c0~tplv-goo7wpa0wc-image.image) </span>


* Conditional formatting: Currently, it is possible to configure icon set conditional formatting for the target completion rate. When the target completion rate meets certain rules, icons are added to the data and colors are changed. For example, when the target completion rate is greater than the time progress, an upward green arrow is displayed to more clearly show the completion status of the target.

   
   |Parameter |Configuration instructions |
   |---|---|
   |Display content |Supports three display modes: icon + text, icon only, or text only. |
   |Position settings |The icon can be placed before or after the text. |
   |Icon style |Provides multiple icon styles. |
   |Condition settings |When the target completion rate meets a certain condition, the corresponding icon will be displayed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If rules conflict, only the previous rule takes effect.</div><br> |
   |Null value display |If the target completion rate is not set, it is treated as a null value. Supports setting the icon and its color for null values. |
   |Text color |Supports setting the color of the target completion rate data. You can choose to follow the icon or customize it. |
