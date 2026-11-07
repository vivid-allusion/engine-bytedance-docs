---
title: "Chart Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Chart_Management"
---

<span id="_1-概述"></span>
# 1. Overview

In "Chart management", you can view charts in the current project for which you have view permissions, and perform rename and delete operations on charts for which you have management permissions.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

**Chart management**: Find saved charts and perform rename and delete operations on them.

<span id="_2-2使用过程示例"></span>
## 2.2 Example usage process

**Step 1**: Use dataset, owner, and search box to search for charts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e4d735e1f584952b3cd327cbf9e5ae6~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: View the dashboard or dataset where the chart is located. Click the dashboard or dataset name to go to the corresponding resource page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7773f5ef0e84203bfb67ccb021406e5~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Click the "Rename" button for the chart to perform the rename operation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3169ea2f6b3c486d9a6504d0433fae55~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: Click the "Delete" button for the chart to perform the delete operation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9550e698a75d4275bd60d48f517f69c3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature description

<span id="_3-1-过滤条件"></span>
## 3.1 Filter criteria

**Dataset**: The dropdown search box lists datasets for which the current user has view or higher permissions. The default is "All".

**Owner**: The dropdown search box displays project members matching the fuzzy search. The default is the current user. Click "Only mine" to set the input box to the current user.

**Search box**: Perform a fuzzy search on chart names and chart descriptions based on the entered keywords.

<span id="_3-2-图表列表"></span>
## 3.2 Chart list

<span id="_3-2-1-列表内容"></span>
### 3.2.1 List content

**The chart list displays charts created from datasets for which you have view permissions.** 

(1) In the list, chart names, dashboards, and datasets can be clicked with the mouse to open a new tab and access the respective resource page.

(2) When the current chart is used as a subquery input for other charts, an icon is displayed before the chart name.

(3) Hover the mouse over the chart name to view the full chart name and chart description.

(4) When a chart exists in multiple dashboards, click the icon to view more dashboard information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7773f5ef0e84203bfb67ccb021406e5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-操作权限"></span>
### 3.2.2 Operation permissions

**Rename & delete:**  Users can perform "Rename" and "Delete" operations on charts. If the user does not have permission, the buttons are grayed out and cannot be clicked.

**Reference validation:**  When deleting a chart, reference validation will be performed on the chart. Even if a reference relationship exists, you can still click the "Confirm" button to delete the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9db008d6e1964d39af2e62b64d0adef2~tplv-goo7wpa0wc-image.image) </span>
