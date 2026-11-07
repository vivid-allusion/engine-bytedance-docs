---
title: "Date Filter"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Date_Filter"
---

<span id="_1-概述"></span>
# 1. Overview

Filtering is a fundamental step in data analysis. This document describes various methods for filtering chart data by date, as well as the display options for date filter controls.

<span id="_2-快速入门"></span>
# 2. Quick start

How to filter charts by date?

**Step 1**: Drag the date field into the "Filter" area and click the field name to open the settings panel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21e1755f209d42a9aafff35f6184430e~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Select a filter mode from the left sidebar. The default mode is "Dynamic date".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/225e76c52c9e424e8155b2045382efd6~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Select the filter criteria.

If the filter control does not need to be displayed on the chart, simply click "OK" after completing the settings. To display the date filter on the page, check the "As filter" checkbox in the lower left corner of the panel during setup, then click "OK".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/981ffb3925ad4eefab871a9390a9f480~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature description

<span id="_3-1-在图表上显示日期筛选框"></span>
## 3.1 Displaying the date filter box on the chart

The filter can be configured to display the filter control on the chart, allowing quick switching of filter criteria during queries. To display the date filter on the page, check the "As time range filter" checkbox in the lower left corner of the panel when configuring date filtering.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce22d1d3414640db9a206f12cc0b7d4c~tplv-goo7wpa0wc-image.image) </span>

The display effect is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/925bbe7cf3de48f38f1808c3e97e16cc~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-切换日期粒度"></span>
## 3.2 Switching date granularity

The granularity of date filtering can be switched in the upper left corner of the date filter popup. Supported granularities are: year\-month\-day, year\-month, and year\-week.


* **Year\-month\-day:**  View filtered data by day granularity.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/919e0ce7d4be4878bd0773b49bc97a69~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d8b94ef084046fbb9d95d527393a080~tplv-goo7wpa0wc-image.image) </span>


* **Year\-month:**  View filtered data by month granularity.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2593e2fcd5e54442897f58900084655c~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e6de5e47b9d4dc497b411aeb5a42c16~tplv-goo7wpa0wc-image.image) </span>


* **Year\-week:**  View filtered data by week granularity, and support custom "week calculation logic".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54fd31c7190c40c08fe873b4039d6212~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86399339a0f54e48a8fd8bde0961348f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-动态日期筛选"></span>
## 3.3 Dynamic date filtering

The date range generated based on user\-defined anchor points will continuously change over time. For example, view the order volume for "the past 30 days".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/021faca2bb4b4ebbb7d0622c1608adc4~tplv-goo7wpa0wc-image.image) </span>

The product provides several preset quick options based on business scenarios, allowing users to quickly specify filter criteria.


|Quick options |Definition |Example |Note |
|---|---|---|---|
|Last N hours |Count back 1 hour from now | |This option is only available for partition fields of hour\-level synchronized datasets. |
|Last N days |Top 1 partition date |*  |This option is only available for partition date fields. |
|Last 7 days |Top 7 partition dates |*  |This option is only available for partition date fields. |
|Last 14 days |Top 14 partition dates |*  |This option is only available for partition date fields. |
|Last 30 days |Top 30 partition dates |*  |This option is only available for partition date fields. |
|Last 1 day |Yesterday |If today is 2020\-02\-13, then last 1 day = 2020\-02\-12 | |
|Last 7 days |From 6 days before yesterday to yesterday |If today is 2020\-02\-13, then last 7 days = 2020\-02\-06~2020\-02\-12 | |
|This week |This week |If today is 2023\-06\-21, then this week = 2023\-06\-19~2023\-06\-20 | |
|Last week |Last week |If today is 2023\-06\-21, then last week = 2023\-06\-12~2023\-06\-18 | |
|Last 14 days |From 13 days before yesterday to yesterday |If today is 2020\-02\-13, then last 14 days = 2020\-01\-30~2020\-02\-12 | |
|Last 30 days |From 29 days before yesterday to yesterday |If today is 2020\-02\-13, then last 30 days = 2020\-01\-14~2020\-02\-12 | |
|This month |First day of this month to yesterday |If today is 2020\-02\-13, then this month = 2020\-02\-01~2020\-02\-12 | |
|This bimonth |First day of this bimonth to yesterday |If today is 2020\-02\-13, then this bimonth = 2020\-01\-01~2020\-02\-12 | |
|Last 3 months |From the first day of the month two months ago to yesterday |If today is 2020\-02\-13, then last 3 months = 2019\-12\-01~2020\-02\-12 | |
|Last 6 months |From the first day of the month five months ago to yesterday |If today is 2020\-02\-13, then last 6 months = 2019\-09\-01~2020\-02\-12 | |
|Last 1 year / This year |First day of this year to yesterday |If today is 2020\-02\-13, then last 1 year = 2020\-01\-01~2020\-02\-12 | |
|Last 2 years |First day of last year to yesterday |If today is 2020\-02\-13, then last 2 years = 2019\-01\-01~2020\-02\-12 | |
|Last 365 days |From 364 days before yesterday to yesterday |If today is 2020\-02\-13, then last 365 days = 2019\-02\-13~2020\-02\-12 | |
|Last month |First day of last month to last day of last month |If today is 2020\-02\-13, then last month = 2020\-01\-01~2020\-01\-31 | |
|Last bimonth |First day of last bimonth to last day of last bimonth |If today is 2020\-02\-13, then last bimonth = 2019\-11\-01~2019\-12\-31 | |
|Last year |First day of last year to last day of last year |If today is 2020\-02\-13, then last year = 2019\-01\-01~2019\-12\-31 | |


If the preset quick options do not meet requirements, users can also customize dynamic dates.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2a5b53511554f2da251b077363dbcd8~tplv-goo7wpa0wc-image.image) </span>

Note: If "workdays" are set in "Advanced settings", when filtering for the most recent days, the time preview may display preview information that includes non\-working days. However, in the actual chart, non\-working days will not appear in the chart. The time preview is for reference only.

In custom scenarios, if the operator is "recent", the product additionally provides checkboxes to offset the date range according to the granularity of the time window. Taking a date with hour, minute, and second as an example, when the granularity is set to "hour", two checkboxes will appear:


* Include this hour: Includes the hour in which the current time falls. For example, if the current time is 19:13:23, selecting "Include this hour" will display data from 19:00:00 to 19:59:59.

* On the hour: Represents a complete hour. For example, if the current time is 19:13:23, selecting "On the hour" will display data from 19:00:00 to 19:59:59. If "On the hour" is not selected, data from 19:13:23 to 20:13:23 will be displayed.


<span id="_3-4-固定日期筛选"></span>
## 3.4 Fixed date filtering

In contrast to dynamic dates, a fixed date range does not change over time. For example, if today is 2020\-02\-13, set the date filter condition to a fixed date: 2020\-02\-08 to 2020\-02\-12. Ten days later, the filter condition will still be 2020\-02\-08 to 2020\-02\-12. When the date field includes hour, minute, and second, you can select an exact time.

**For partitioned date fields, some dates in the calendar will be unselectable, indicating that this date partition does not exist in the dataset.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4edcdbdee7dc436d9ac2aa204bfcbcc4~tplv-goo7wpa0wc-image.image) </span>


* The time range selected in "dynamic date" can be directly transferred to the target filter's "fixed date" for filtering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc497f6d3eab478c8d036f6586b39212~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/760356cf921248b19fc5908e69f94fdb~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-高级筛选"></span>
## 3.5 Advanced filtering

Configure the start and end times of the date filter separately to flexibly define the date range for filtering. After selection, you can preview it in the time preview.

For example, if today is 2020\-02\-13, set the date filter condition as follows:

Start time: Fixed 2020\-01\-04

End time: Dynamic 1 day ago

The date will then be selected as 2020\-01\-04 to 2020\-02\-12. One day later, the date selection will be 2020\-01\-04 to 2020\-02\-13, and so on.

**Fixed (filter type)** 

Select a fixed date as the start or end time for the filter. If the date field is p_date (the dataset partition field), only dates with data present in the partition can be selected.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/261a3d8b747e40b48feb2de15c286625~tplv-goo7wpa0wc-image.image) </span>

**Dynamic**

Dynamically select a time point before or after the current time as the start or end time for the filter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a776216bc82474bb604728be2461ffc~tplv-goo7wpa0wc-image.image) </span>

**Unrestricted**

When used as the start time, the start time is not restricted, and all time points less than or equal to the end time are selected.

When used as the end time, the end time is not restricted, and all time points greater than or equal to the start time are selected. An unrestricted end time allows the end time to be dynamically set to the most recent time point with available data.

Caution: The start time and end time cannot both be set as unrestricted simultaneously. At least one time must be specified.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ac4388a27cf4901969f6cb77b1b6703~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-常用场景"></span>
## 3.6 Common scenarios

For example, if an event goes live on June 14, and you need to dynamically view event data during the event period (after June 14), you can configure the date filter as follows to achieve the filtering effect of "2023\-06\-14 ~ present".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87fd04a3ed1c4d0f8b6ddd7edeb21666~tplv-goo7wpa0wc-image.image) </span>

For example, to view event data for the first day of each month and the first day of each quarter from June 11, 2024 to June 11, 2025, you can configure the date filter as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56681894dfc548fcb24779435b7e8e6d~tplv-goo7wpa0wc-image.image" width="2938px" /></div>


<span id="_3-7-特殊值"></span>
## 3.7 Special values

Three types of special values can be filtered: empty dates, non\-empty dates, and all dates. The default is all dates.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a46d3ca555c848069921d04c4e7eef66~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-单个日期筛选"></span>
## 3.8 Single date filter

Definition of "single date": Only one day can be selected at a time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf717d82171b4816a4793c8d5d5eed68~tplv-goo7wpa0wc-image.image) </span>

**Caution: When the partition date field is used, a "most recent day with data/trading day" checkbox is provided below the calendar. This is mutually exclusive to the calendar above.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3c99735c38749af8fbf8e45b290a301~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-9-作为时间范围筛选器"></span>
## 3.9 As a time range filter

When the date filter page remains in dynamic date, advanced, special value, or fixed date mode, select the checkbox at the bottom of the panel and click Confirm.

The filter will provide all four modes simultaneously, making it convenient to switch between them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91b3bdab2d81492eb51f1864d84e22f3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-10-作为单个日期筛选器"></span>
## 3.10 As a single date filter

When the date filter page remains in single date mode, select the checkbox at the lower left of the panel, then click OK. The filter will provide single date mode.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf717d82171b4816a4793c8d5d5eed68~tplv-goo7wpa0wc-image.image) </span>
