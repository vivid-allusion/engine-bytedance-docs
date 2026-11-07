---
title: "Common Dashboard FAQs"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Common_Dashboard_FAQs"
---

<span id="_1-仪表盘-权限常见问题"></span>
# 1. Common questions about dashboards and permissions

<span id="个人仪表盘和公共仪表盘有什么区别？"></span>
## What is the difference between a personal dashboard and a public dashboard?


* **In terms of visibility**


**For dashboard owners and administrators**

Personal dashboards: Displayed under the "Personal dashboards" section

Public dashboards: Displayed in the corresponding folder under the "Public dashboards" section

**For other users with dashboard viewing permissions**

Personal dashboards: Displayed under the "Shared with me" section

Public dashboards: Displayed in the corresponding folder under the "Public dashboards" section

**For users without dashboard viewing permissions**

Personal dashboards: This dashboard is not visible in the dashboard list

Public dashboards: Displayed in the corresponding folder under the "Public dashboards" section and shown in gray

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e50a6f20393c4715b5e99b041fe73369~tplv-goo7wpa0wc-image.image" width="311px" /></div>



* **In terms of permission scope**


Personal dashboards: Can grant viewing permissions to other users

Public dashboards: Can grant viewing, editing, and management permissions to other users

<span id="个人仪表盘可以协同编辑吗？"></span>
## Can personal dashboards be collaboratively edited?

No, personal dashboards can only grant viewing permissions to others

<span id="如果我想和团队成员一起编辑仪表盘，但因为仪表盘没上线，不想展示给用户看应该怎么办？"></span>
## To collaboratively edit a dashboard with team members but avoid displaying it to users because it is not yet live, what should be done?

The dashboard can be placed in "Public dashboards" and then the following steps can be taken:

(1) Create a blank sheet and add a text widget to indicate that the dashboard is under construction

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae8b3de76d324eb9884a798e6613d6c9~tplv-goo7wpa0wc-image.image) </span>

(2) Edit on the original sheet and hide that sheet (right\-click the sheet name and select Hide)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9939240eeb02488899e75e3b820b50f7~tplv-goo7wpa0wc-image.image) </span>

(3) Save

This way, other users will only see the unhidden blank sheet and will not see the sheet that is being edited.

<span id="仪表盘仅阅览、查看、编辑、管理权限的操作范围是什么？"></span>
## What are the operational scopes of view only, view, edit, and manage permissions for dashboards?


|**Permission level** |**Scope of operations** |**Note** |
|---|---|---|
|View only |View dashboard pages |Export and download operations are not allowed. |
|View |View dashboard pages, export charts and data, and subscribe to dashboards to personal Lark or email. | |
|Edit |View dashboard pages, export charts and data, edit dashboards, and subscribe to dashboards to personal Lark or email. | |
|Management |View dashboard pages, export charts and data, edit dashboards, grant permissions, subscribe to dashboards to personal Lark or email, and subscribe to dashboards to Lark groups or email groups. |Only users with management permissions can subscribe to dashboard pushes to Lark groups or email groups. |


<span id="我有仪表盘的权限，为什么打开仪表盘时，部分图表还是会提示我缺少数据权限？"></span>
## I have dashboard permissions. Why do some charts still prompt that I lack data permissions when opening the dashboard?

To facilitate data management, the platform supports data permission features, including row\-level and column\-level permissions.

When data permissions are set for data in a dataset, users are also subject to the corresponding permission controls when viewing visualizations, charts, or dashboards created from that dataset. Data permissions are bound to datasets.

Therefore, opening a dashboard only means that you have permission for that dashboard. Charts, however, are governed by data permissions. If you do not have the corresponding data permissions, you cannot view the data within the chart.

<span id="_2-报错信息"></span>
# 2. Error messages

<span id="调整仪表盘顺序时报错共享空间目录某些资源授权失效，请刷新后再调整顺序或-共享空间目录已更新，请刷新后再调整顺序怎么办"></span>
## When adjusting the dashboard order, an error occurs: authorization for certain resources in the shared space directory has expired. Please refresh and then adjust the order again, or the shared space directory has been updated. Please refresh and then adjust the order again. What should I do?

**Cause**

Some dashboard permissions have been revoked or changed, resulting in a failure to adjust the order.

**Solution**

Refresh the page to obtain the latest status, then adjust the order.

<span id="_3-监控订阅常见问题"></span>
# 3. Frequently asked questions about monitoring subscriptions

<span id="支持订阅报表、看板定时发飞书-lark、定时发邮件吗"></span>
## Is it supported to subscribe to reports and dashboards for scheduled delivery via Lark or scheduled email delivery?

Supported.

<span id="支持哪些订阅推送方式呢"></span>
## What subscription delivery methods are supported?

The system currently supports integration with office software such as Lark, email, Webex, WeCom, and DingTalk.

<span id="_4-其他常见问题"></span>
# 4. Other frequently asked questions

<span id="可以跨项目移动看板吗"></span>
## Is it possible to move dashboards across projects?

Not supported at this time.

However, you can use iframe or SDK integration to embed existing dashboards into dashboards of other projects to achieve cross\-project viewing.

For more requirements, please contact us.

<span id="进入项目后看不到任何仪表盘"></span>
## No dashboards are visible after entering the project


1. Please check with the project owner to confirm whether you have project permissions.

2. Please check with the project owner to confirm whether there are any published public dashboards in the project.

3. Please check whether "Show only my favorites" in the lower right corner is selected. If selected, please deselect it.

    &nbsp;


<span id="no-manageable-permissions-available-when-authorizing-dashboards"></span>
## No manageable permissions available when authorizing dashboards

Personal dashboards only support granting view permissions. Public dashboards support granting view, edit, and manage permissions.

When granting permissions for a personal dashboard, it may not be possible to grant management or edit permissions to users.

<span id="如何保存仪表盘中的数据图表"></span>
## How to save data charts in a dashboard

You can click the ⋮ in the upper right corner of the chart to select Download Data, or copy the chart to another dashboard for display by using Copy to Dashboard.

<span id="如何删除仪表盘的图表"></span>
## How to delete a chart from a dashboard

Go to the target dashboard, click Edit, delete the corresponding chart, and then save.

<span id="图表支持展示多少个数据点"></span>
## How many data points can a chart display

10,000

<span id="今天看板为什么看不了数"></span>
## Why are numbers not visible on the dashboard today

Possible reason: The data in the corresponding dataset has not finished synchronizing.

Solution: Click the chart name on the dashboard to enter Visualization \-\> Click the ⋮ next to the dataset switch in the upper left corner of Visualization and select View Dataset \-\> Click the synchronization status of the dataset to check whether today's synchronization was successful. If synchronization is not successful, wait until synchronization completes.

<span id="为什么无法创建个人仪表盘了"></span>
## Why is it not possible to create a personal dashboard

**Similar questions:** 

> Why is it not possible to create a personal board

> I am the owner. Why can I not grant permissions to others


Please check with the project administrator whether the project is in strict mode.

In strict mode:


* The resource creator only has edit permissions for the resource by default,

* The project administrator is automatically added to the authorized list of the resource and assigned management permissions by default.

* Project users cannot configure personal dashboards.
