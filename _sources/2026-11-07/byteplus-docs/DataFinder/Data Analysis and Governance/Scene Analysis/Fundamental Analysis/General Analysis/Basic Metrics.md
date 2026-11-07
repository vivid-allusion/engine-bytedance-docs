---
title: "Basic Metrics"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Basic_Metrics"
---

<span id="_1-概述"></span>
# 1. Function Overview

<span id="6868acfc"></span>
## Supported basic metrics

You can use the basic metrics function to view the basic situation of each end product, including the number of active users, active composition, and active viscosity in a certain period of time.


* Number of active users: the number of users who have experienced any event within a specified time frame.

* Added: The number of users who reported an event for the first time and any event occurred within the specified time frame.

* New users percentage: the ratio of the number of new users to active users in the specified time frame.

* Active viscosity: can only be viewed in the sky level, which includes two metrics:

   * DAU/Active users in the last 7 days: The number of active users in the last 7 days (excluding today) is deduplicated.

   * DAU/Active users in the last 30 days: The number of active users in the last 30 days (excluding today) is deduplicated.


<span id="2c4a7b01"></span>
## Basic metric function change description


* The basic metric function has been upgraded recently, and functions such as time filter and subdivision filter have been upgraded. The function change points after the upgrade are shown in the figure below.

* It is recommended that you use the new version of the basic metric function. This article also takes the new version of the basic metric as an example to introduce the main operation points for you. If you want to use the old version, you can click the switch button in the upper right corner to switch to the old version of the basic metric function page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d724804999ea4a15a01dc0b3d2e79912~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-指标配置"></span>
# 2. Metric configuration

You can configure metrics, time, and other items in the configuration area at the top.

<span id="_2-1-时间范围选择"></span>
## 2.1 Configuration time range

You can choose which period of time you want to focus on metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fc76cf056b0485ea69b70d022b4925f~tplv-goo7wpa0wc-image.image) </span>


* Configure time granularity: Support viewing 5\-minute, hour, day, week, and month\-level data.

* Configuration time range: Support selecting the time range to be analyzed in the time configuration box. The system presets some shortcut options for common time ranges for you to improve configuration efficiency.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Under different time granularities, the time range supported by the query is inconsistent. When the current manually selected time range exceeds the maximum time range supported by the query, the actual query result will automatically adjust the time range for you.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For example, when the time granularity is hourly, the time range for supporting queries is 7 days. If you choose a time range longer than 7 days, the actual query will automatically adjust to 7 days for you.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the time granularity is weekly or monthly, and the time range is less than one week or one month when you select it, the actual query results automatically complete the data for one week or one month for you.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For example, time granularity is weekly, and if you select data with a time range of 3 days, the actual query results automatically complete a week's worth of data for you.   </div>
   

* Configuration comparison time:

   * You can add "comparison time", and you can set a time interval to compare with the target time metric.

   * You can select the start and end points of the comparison period interval in the icon area. By default, the comparison period interval is the same length as the original focus period.


<span id="08368b6e"></span>
## 2.2 Configuring end points and platforms

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e3c8321c8784204ae3d991f6b236c76~tplv-goo7wpa0wc-image.image) </span>


* Select the end point type for analysis: supports mobile end, web end, Mini Program, you can also choose the end point type as "All" to analyze all types of end point data.

* Select the platform type corresponding to the end point: When selecting different end point types, support segmentation to select the platform corresponding to the end point type.

   For example, when selecting mobile end, support to select iOS, Android, OpenHarmony sub\-platform.


<span id="_2-3-选择指标"></span>
## 2.3 Selecting metrics

You can choose the metrics you follow, active users/active composition/active viscosity, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f2b2b6abcf94c80adf6a4c7cf5a1b1c~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only when the time particle size is day level, the selection of "active viscosity" metric is supported.</div>


<span id="_2-4-选择维度"></span>
## 2.4 Configuring segmentation filtering

You can configure filters for query results at the segmentation filter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/445f2f73196440d79598326200018399~tplv-goo7wpa0wc-image.image) </span>


* Currently, filtering by user attributes, event attributes, and user grouping is supported. If you enable the user tag function, you can also use the user tag to filter.

* It supports adding multiple filter conditions, and the logical relationship between multiple conditions is "AND".


<span id="_3-中部图表区"></span>
# 3. View the resulting data chart

The metric data you are concerned about will be displayed as a chart in the central chart area, as shown below:


* Mouse over the data points in the graph, you can view the data details corresponding to the data points.

* You can show/hide the polyline corresponding to the legend by clicking on the legend to light/grey out the legend.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13597c75b86845fc9c100c744fca7382~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-详细数据"></span>
# Step 4 View detailed data


* After you select the time range for the metric, the time information for the selected range, as well as the corresponding four metrics for each time period (active users, percentage of new users, DAU/last 7 days active users, DAU/last 30 days active users) will be presented in a table at the bottom of the page.

* Click "Download Data" to download the data in the form of excel to the local area, as shown below:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17e9c1cadb4d4ce7bfecdae32d556d0d~tplv-goo7wpa0wc-image.image) </span>
