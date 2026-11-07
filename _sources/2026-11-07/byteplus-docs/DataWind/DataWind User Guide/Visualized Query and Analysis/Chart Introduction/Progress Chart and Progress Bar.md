---
title: "Progress Chart and Progress Bar"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Progress_Chart_and_Progress_Bar"
---

<span id="_1-概述"></span>
# 1. Overview

The progress chart visually displays the completion level of an indicator by setting the current value and target value. Users can view the completion level of a specific indicator through interval colors or the pointer, or monitor the gap from the target value.

The progress chart consists of the gauge face and the pointer. The pointer must be assigned to one indicator, such as total profit or business growth rate. The gauge face supports configuring the starting value and target value to help users obtain reference information.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常见应用场景"></span>
## 2.1 **Common application scenarios**

Monitoring the progress of KPI indicators. For example: monitoring sales revenue and comparing it with the target amount set by the group to track the store's sales progress.

The following are the display styles for the standard progress chart, graduated progress chart, and progress chart.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3787edc95b042148cde78c9a2c4bb07~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8773f3d7af84ff2b5e76805e11f5c3f~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90cb2225e0c049c99cb0f0ae2393420c~tplv-goo7wpa0wc-image.image" width="759px" /></div>


<span id="_2-2-使用过程示例"></span>
## 2.2 Usage example

**Step 1:**  Set the indicator to display and the filter conditions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cc93756cc5f42939f363e2ef310a070~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  In the chart type, select progress chart; or hover the mouse over the progress chart and select progress chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4ecc55b31da4f4783ab07edba8e8ec9~tplv-goo7wpa0wc-image.image) </span>

If the progress chart is selected, you can switch to the graduated style in the style settings below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c60243b63d094d16a6881ae7b93f354e~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  Configure the target value and the maximum/minimum values to display. You can select dynamic values and drag in existing indicators to enable dynamic changes in the scale values.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc2c7d206e154b97970480b262ef6cea~tplv-goo7wpa0wc-image.image) </span>

**Step 4:**  Configure the color style according to display requirements.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b7d09a225044c68b7938d7da6fbe307~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-图表样式选择"></span>
## 3.1 Chart style selection


* progress chart: In chart type, select progress chart.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/804ffa7eba2c4da0995230c5622fc4df~tplv-goo7wpa0wc-image.image) </span>

Scale progress chart: After selecting progress chart, switch to scale in the style settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5a2c9f7c221444db35bf8f48156f1fe~tplv-goo7wpa0wc-image.image) </span>


* Progress chart: In chart type, hover the mouse over the progress chart and select progress bar.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d891b14d5a46c6bd11fc868bfcca4a~tplv-goo7wpa0wc-image.image) </span>

Ring graduated chart: In the style settings, you can switch to ring graduated chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/082ae9bf04044374b2b46400846baa01~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

The progress chart supports setting 0 dimensions and 1 indicator.

<span id="_3-3-数值设置"></span>
## 3.3 Value settings

Supports configuring the minimum, target, and maximum values for the gauge. Provides two options: fixed value and dynamic value.


* Fixed value: The user manually enters the value.

* Dynamic value: Configure dynamic values that can change based on detailed data by dragging metrics and adjusting the aggregation method (it is recommended to select average or maximum value, but you can adjust this as needed).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb96ddb35cfc4d059afae23bd05a9a5e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-指标"></span>
## 3.4 Metrics

Supports showing or hiding metric names, and allows adjustment of the font, color code, and display content for metric names and values.

Within the metric value options, three display modes are supported: current value, proportion of target value, and proportion of target value plus current value.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8adfa3027f744fba6d17d730c47ca01~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-刻度"></span>
## 3.5 Scale

Enable or disable scale display; when enabled, scale styles can be adjusted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb1f32e2a0a74a06b3c82f833ca91663~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-区间设置"></span>
## 3.6 Interval setting


* Division type

   * Divide by proportion: Split intervals by percentage between the maximum and minimum values.

* Divide by value: Split according to metric values.

* Division method

   * If automatic equal division is enabled, intervals are automatically divided equally based on the minimum value, maximum value, and the number of intervals.

* If automatic equal division is not enabled, you can manually set boundary values for each interval.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b1923db9f1d4cd7a462f70b5387fa42~tplv-goo7wpa0wc-image.image) </span>


* Two methods for adding new intervals


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e79c943e6e604d7aa7ae4e7c0ac5db20~tplv-goo7wpa0wc-image.image) </span>


* Interval color, name, and value configuration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e3c8e2b913f488c84da586f3deb3ff4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-7-恢复默认设置"></span>
## 3.7 Restore default settings

Click [Restore Default Settings] to revert all the above chart configurations to their default values.
