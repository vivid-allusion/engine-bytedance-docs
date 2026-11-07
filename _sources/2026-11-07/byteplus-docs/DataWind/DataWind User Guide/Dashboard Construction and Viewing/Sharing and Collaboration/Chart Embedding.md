---
title: "Chart Embedding"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Chart_Embedding"
---

<span id="_1-概述"></span>
# 1. Overview

Chart embedding refers to the embedding functionality for charts and dashboards provided by Intelligent Data Insights. After completing the creation of a dashboard, you can quickly embed the finished dashboard into external system applications for direct viewing.

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-图表嵌入"></span>
## 2.1 Chart embedding

(1) Enter the dashboard preview mode

(2) Click on the right side of the chart to be embedded and select "Embed chart"

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85f932abbf5e4b1f8efb575e19f7b44b~tplv-goo7wpa0wc-image.image) </span>

(3) When "Copy successful" is displayed, you can right\-click to copy or use the keyboard shortcut Ctrl+V. Paste the link into a browser window to view the chart component, which can be quickly added to any embedded address application.

<span id="_2-2-仪表盘嵌入"></span>
## 2.2 Dashboard embedding

(1) Enter the dashboard preview mode

(2) Click on the right side of the chart to be embedded and select "Embed dashboard"

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0b0bcf8c8d84a7f9c98aef962d3007e~tplv-goo7wpa0wc-image.image) </span>

(3) After configuring the embedding settings, click "Copy embed link" in the lower right corner:


* Select the page content to be embedded; you can choose "All" or "Partial sheet";

* Configure the dashboard settings. You can select whether to display the "Dashboard name", "Dashboard owner", "Dashboard action buttons", and so on.

* Configure the chart settings. You can select whether to display the "Chart name", "Tooltip icons", "Toolbar icons".

* Select dashboard filters. If the page contains filters, you can choose whether to embed the filter conditions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ca71a9d8a3043339b7dec3c0c765bd8~tplv-goo7wpa0wc-image.image) </span>

(4) When "Copy successful" is displayed, you can right\-click to copy or use the keyboard shortcut Ctrl+V. Paste the link into a browser window to view the dashboard, which can be quickly added to any embedded address application.

<span id="_2-3-权限说明"></span>
## 2.3 Permission description

After a chart or dashboard is embedded, not all users can view it. Users must be platform users of Intelligent Data Insights (that is, an authentication process is required first). Data permissions are displayed according to the platform's configuration.[Permission Overview](https://docs.byteplus.com/docs/DataWind/Permission_Overview)

In addition, embedded charts support data download, with permissions consistent with platform user permissions.

<span id="_2-4-隐藏图表标题和操作按钮效果"></span>
## 2.4 Effects of hiding chart titles and action buttons


|Chart |Show |The chart title will be displayed. If you have editing and data download permissions, you can download the data. You can integrate with more products. |
|---|---|---|
||Hide |Only the chart content is displayed, without the chart title or any other information. |
|Dashboard |Show |The dashboard title will be displayed, along with options such as refresh, fullscreen, share, bookmark, and embed dashboard. You can integrate with more products. |
||Hide |Only the dashboard viewing page is displayed. |
