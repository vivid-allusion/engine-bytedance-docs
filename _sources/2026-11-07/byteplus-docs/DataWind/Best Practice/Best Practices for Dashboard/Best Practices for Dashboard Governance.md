---
title: "Best Practices for Dashboard Governance"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Best_Practices_for_Dashboard_Governance"
---

<span id="_1-为什么要进行仪表盘治理？"></span>
# 1. Why conduct dashboard governance?

Users with dashboard editing permissions can create public dashboards (for more details: see [2. Dashboard module](https://docs.byteplus.com/docs/DataWind/Permission_Operation_Manual#_2-%E4%BB%AA%E8%A1%A8%E7%9B%98%E6%A8%A1%E5%9D%97)). As the number of users gradually increases, the public dashboards section in some projects contains a large number of dashboards that are actually invalid, abandoned, or have duplicate or unclear content. When team members review numbers, it is difficult to identify which dashboards are effective and accurate, greatly reducing the efficiency of checking metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a43dde8811af4146b63193d6c460753f~tplv-goo7wpa0wc-image.image) </span>

At this point, dashboard governance is needed. The main steps include the following:

(1) Cleaning redundant and abandoned dashboards

(2) Archiving some historical dashboards (dashboards that are not checked regularly but may be needed for future reviews, such as dashboards for certain events)

(3) Categorizing effective dashboards

This article will introduce dashboard governance solutions step by step through these three steps.

Effect comparison:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/087e44c71c614ed88d84af704a73a858~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-冗余、废弃仪表盘清理"></span>
# 2. Cleaning redundant and abandoned dashboards

<span id="_2-1-长期无人访问仪表盘清理"></span>
## 2.1 Cleaning dashboards with no visits for an extended period

Go to Project Center \- Access Statistics, select "Last 30 days", "Dashboards I am responsible for", and add the filter condition "pv=0" in the usage summary.

View dashboard information, select the dashboards, and perform batch cleaning. You can also select all dashboards on the current page for cleaning.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9d11384dfca436cbcafdf7c0c7c9c6b~tplv-goo7wpa0wc-image.image) </span>

If you select "Delete", the dashboards will be moved to the recycle bin and can be restored from Project Center \- Recycle Bin within 15 days.

If you select "Permanently Delete", the dashboards will be permanently deleted and cannot be restored.

<span id="_2-2-根据特定条件清理"></span>
## 2.2 Cleaning based on specific conditions

You can filter out obviously useless dashboards by keywords and clean them up. For example, search for dashboards with names containing "test"

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fecfa9fb0431420f86ec6dcd43e4de9c~tplv-goo7wpa0wc-image.image) </span>

Filter by dashboard owner, such as process dashboards in batch that belong to team members who are about to leave or transfer positions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eac0259ce1e84eb0b502398be10209fb~tplv-goo7wpa0wc-image.image) </span>

In PV/UV statistics, exclude visits from certain users or user groups to obtain PV/UV statistics for dashboards excluding these users, which helps us determine whether they can be deleted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb6ef308dfd844bea365412d7a23436a~tplv-goo7wpa0wc-image.image) </span>

Then handle the dashboards found as appropriate.

<span id="_3-部分历史仪表盘归档"></span>
# 3. Archiving some historical dashboards

There are some dashboards that are no longer frequently viewed, but may still be needed for future review, and it is unclear which folder they should be placed in.

At this point, you can create a "Dashboard Archive" folder in the dashboard interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8f4f67f316b44e9aaa198c4c58dd6a4~tplv-goo7wpa0wc-image.image) </span>

Go to Project Center \- Access Statistics, select the dashboards to be archived in bulk, click Move, and move them to the archive folder.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a86c5014a454d8ab473e9b5a2e8bac0~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-有效仪表盘归类"></span>
# 4. Effective dashboard categorization

<span id="_4-1-归类"></span>
## 4.1 Categorization

After cleaning up and archiving redundant and obsolete dashboards, the remaining dashboards are the useful ones. However, as there is no categorization, it still appears quite disorganized, making it difficult to quickly locate the desired content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4eab5d7978d47b5b158eadcc9198ac6~tplv-goo7wpa0wc-image.image) </span>

It is recommended to create folders based on different business parties or business domains. This way, each business party only needs to focus on one or a few folders when viewing dashboards. (This step is recommended to be performed by the project's data administrator for overall data management.)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a76ee3a0ba7c410fb054ea762245f185~tplv-goo7wpa0wc-image.image) </span>

Next, drag and drop dashboards into the corresponding folders, and you can also drag to sort them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e3f5bbdcaa044f5b745eaaf5c3ef968~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-权限收敛"></span>
## 4.2 Permission convergence

To prevent users from continuing to create dashboards in the root directory and causing the dashboard list to become disorganized again, it is recommended that the project administrator converge user permissions after dashboard management is completed.

First, for business users who do not need to create datasets or public dashboard folders, change their project editing permissions to view\-only permissions to prevent them from creating dashboards in the public dashboard root directory.

In Project Center \- Permission Management, select the user or user group to [Permission Management](https://docs.byteplus.com/docs/DataWind/Permission_Management).

For users who need to create dashboards within their own business area, enable editing permissions for the dashboard folder.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48bb2839b4484a4a9ccc947198870b9b~tplv-goo7wpa0wc-image.image) </span>

After this adjustment, users will not be able to create dashboards in the public dashboard root directory, but can create and modify dashboards within the corresponding folders.
