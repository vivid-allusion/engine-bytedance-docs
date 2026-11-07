---
title: "Web Page Embedding"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Web_Page_Embedding"
---

<span id="_1-概述"></span>
# 1. Overview

In the dashboard editing interface of Intelligent Data Insight, the control area on the left supports the Web Page component. Users can embed web page content into the dashboard. Users can also export charts as web pages and then embed them again, enabling cross\-dashboard, cross\-project, and cross\-data center display of charts.

Users only need to select the Web Page component in the control area on the left. The Web Page component will appear on the editing canvas. After selecting it, users can enter the web page link on the right. Once the link is entered, the content of the linked page will be displayed in the Web Page component.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-嵌入普通网页"></span>
## 2.1 Embed a standard web page

**Step 1:**  Go to the dashboard editing page and select the Web Page component from the component bar on the left.

**Step 2:**  After selecting the Web Page component, enter the URL to be embedded in the URL field of the Web Page configuration panel on the right.

**Step 3:**  Click anywhere on the Web Page component or the Web Page configuration panel; the web page will be added.

**Caution:**  After entering the URL, do not click on a blank area of the canvas, or the URL may not be entered successfully.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/894a35e9ea7a4c8880996e1a8a7a4b8d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-仪表盘或图表跨项目展示"></span>
## 2.2 Cross\-project display of dashboards or charts

You can export the link of a dashboard or chart from another project and embed it into the current dashboard using the Web Page component.

**Caution:**  To avoid gesture conflicts, you cannot enter edit mode when embedding another dashboard.

**Operation steps**

**Step 1:**  On the dashboard viewing page, select the option to export the chart or export the dashboard from the upper right corner of the chart or dashboard to obtain the export link.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0af9642b3cd43aeb267065db9f8db10~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f17c802534944ff8cefd7611add67aa~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2073e21238a94435a2dba9622186811d~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Go to the dashboard page where you want to embed the content, select Insert Web Page, and enter the export link you just obtained on the right. This will embed the exported chart into the current dashboard (cross\-project embedding is supported).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63f0a88e34c94e1e8a3fd547f69dcb7c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-跨平台内容展示"></span>
## 2.3 Cross\-platform content display

You can embed external links from other platforms into the current dashboard using the web page widget. For example, you can embed explanatory Feishu documents into the dashboard to help readers better understand the meaning of the charts.

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-覆盖筛选器"></span>
## 3.1 Override filters

When embedding charts or entire dashboards from other dashboards into the current dashboard, you can control the filters of the embedded charts or dashboards through the global filters of the current dashboard by adding parameters.

<span id="日期类型字段传参规则"></span>
#### **Date field parameter passing rules**

The date conversion rules support both default and absolute values. When absolute value is selected, the selected date will be converted to a time range for parameter passing.

**Examples of default values for date parameter passing:** 


|op |Scope of application |Note |Example |
|---|---|---|---|
|`=` |Date \- single date |The value is a string in date format<br><br>Supports 'YYYY\-MM\-DD' (year\-month\-day) or 'YYYY\-MM' (year\-month) |`field = '2022-10-01'`<br><br>`field = '2022-06'` |
|`between value1 and value2` |Date \- fixed date<br><br>Date \- advanced date |When both value1 and value2 are strings in date format, it is a fixed date;<br><br>At the same time, either value1 or value2 can be an advanced date described by the `advancedDate` function. For details, see the function description section. |`field between '2022-10-01' and '2022-11-30'`<br><br>`field between '2022-10-01' and advancedDate(1, {unit: "day", offset: -1})` |
|`>=` |Date \- advanced date |The start time is the specified time, and the end time is not limited<br><br>The specified time can be a string in date format or an advanced date described by the `advancedDate` function |`field >= '2022-10-01'`<br><br>`field >= advancedDate(1, {unit: "day", offset: -1})` |
|`<=` |Date \- advanced date |The start time is not limited, and the end time is the specified time<br><br>The specified time can be a string in date format or an advanced date described by the `advancedDate` function |`field <= '2022-10-02'` |
|`is empty` |Date \- special date | |`field is empty` |
|`is not empty` |Date \- special date | |`field is not empty` |


**Examples of absolute values for date parameter passing:** 


|Filter type ||Rule |Example ||
|---|---|---|---|---|
||||In\-page filter |Web parameter passing |
|Year, month, day |Dynamic date |Date\-time type uses the selected time; date type fills in **hour, minute, and second** |Last 7 days (2023\-10\-16 ~ 2023\-10\-22) |btw '2023\-10\-16 00:00:00','2023\-10\-22 23:59:59' |
||Fixed date |Date\-time type uses the selected time; date type fills in **hour, minute, and second** |2023\-10\-16 ~ 2023\-10\-22 |btw '2023\-10\-16 00:00:00','2023\-10\-22 23:59:59' |
|Year and month |Dynamic date |Fill in **day, hour, minute, and second** |This month (2023\-10 ~ 2023\-10) |btw '2023\-10\-01 00:00:00','2023\-10\-31 23:59:59' |
||Fixed date |Pad **day, hour, minute, and second** |2023\-10 ~ 2023\-10 |btw '2023\-10\-01 00:00:00','2023\-10\-31 23:59:59' |
|Week of year |Dynamic date |Convert to 'yyyy\-MM\-dd HH:mm:ss' |This week (2023–week 42 (10/16–10/22)) |btw '2023\-10\-16 00:00:00','2023\-10\-22 23:59:59' |
||Fixed date |Convert to 'yyyy\-MM\-dd HH:mm:ss' |2023–week 42 (10/16–10/22) ~ 2023–week 43 (10/23–10/29) |btw '2023\-10\-16 00:00:00','2023\-10\-29 23:59:59' |
