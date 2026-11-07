---
title: "A Complete Guide to the of System Permission Framework"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/A_Complete_Guide_to_the_of_System_Permission_Framework"
---

> "Why did I apply for project permissions but still cannot view the dashboard?"

> "Why did I apply for dashboard permissions but still receive a message saying I do not have permission?"


Every day, in the admin panel of the DataWind product's help center, "permission" remains one of the most frequently searched terms.

Today, let's talk about what the various permissions in the product mean.

<span id="_1-产品的权限体系"></span>
# 1. Product permission framework

First, what are permissions?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d433011a2406406c9b287de7c84dc30d~tplv-goo7wpa0wc-image.image) </span>

Next, what does the product's permission framework look like?

Product permissions are divided into project permissions, data resource (dataset, dashboard) permissions, and data permissions, which respectively determine whether you can access a project, open a dashboard or dataset, and view specific parts of the data.

Project permissions and data resource permissions are further divided into view, edit, and manage permissions. When granting permissions, you can authorize users or user groups you create.

User and user group management, as well as permission changes, can all be performed in the project center.

> PS: Role management will be supported in the future


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/112a11a622ad47388f32e0292274a48d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-产品一共有多少种权限？"></span>
# 2. How many types of permissions does the product have?

The types of permissions in the product are divided into resource permissions and data permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3feb189170146c4bae79f0d38598d5d~tplv-goo7wpa0wc-image.image) </span>


* Resource permissions include project permissions, dashboard permissions, and dataset permissions.

* Project permissions determine whether you can open a project.

* Dashboard permissions and dataset permissions determine whether you can view the corresponding dashboard or dataset.

* When dashboard or dataset permissions are granted, project view permissions are automatically enabled.


<span id="_2-1-资源权限"></span>
## 2.1 Resource permissions

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7040f97fd5d34b128cb812a1b7f2d7c4~tplv-goo7wpa0wc-image.image) </span>

**Resource permissions**


|Permission categories |View permission |Edit permission |Global viewing permission |Management permissions |
|---|---|---|---|---|
|**Application scenarios** |This permission is generally granted to users who view resources. |This permission is generally granted to users who collaboratively edit resources. |This permission is generally granted to the leader of the business unit who does not participate in permission approval for the project. |This permission is generally granted to the resource creator or users assigned to collaboratively manage the resource.<br><br>Caution: Personal dashboard management permissions cannot be granted to others. |
|**Project** |Users have access permissions to enter the project, can view authorized resources within the project, and can also create personal dashboards or folders. |In addition to project viewing permissions, users can create new public dashboards, datasets, or folders in the root directory of the public directory. |Users have viewing permissions for all public dashboards, public dashboard folders, and datasets within the project, and can view all data. |Users have management permissions for resources within the project, can manage permissions, delete the project, and perform other operations. This is the highest level of resource permission. |
|**Dashboard** |Users can view dashboards, add to favorites, subscribe normally, download charts, and perform other operations. |In addition to having dashboard viewing permissions, users can also edit dashboards and perform other operations. |/ |In addition to having dashboard editing permissions, users can also manage permissions, delete, move dashboards, copy dashboards, and perform other operations. This is the highest level of resource permission. |
|**Dataset** |Users can query datasets, add temporary fields, download, configure monitoring, and view dataset details on the visual query page. |In addition to having dataset viewing permissions, users can also modify the dataset model, configure routines, manage aliases, and perform other operations. |/ |In addition to having dataset editing permissions, users can also manage permissions, delete, and perform other operations. This is the highest level of resource permission. |


<span id="_2-2-数据权限"></span>
## 2.2 Data permissions

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e10ad8877194451be6d424b230c606b~tplv-goo7wpa0wc-image.image) </span>

Data permissions determine whether you can view the data in charts or dashboards created using a dataset.

**Data permissions**


|Permission classification |Permission definition |
|---|---|
|**Row\-level permissions** |That is, controlling a specific user to view only certain rows of data for a particular field. For example, User A can only view data in the dataset where the "Region" field is equal to Shanghai. |
|**Column permissions** |This controls whether a user can view a specific column in the dataset, such as user A not being able to view the "Revenue" column data in the dataset. |


If data permission control (such as row\-level permissions) is set for a dataset, then all places where the dataset's data is used (such as visual queries, charts, dashboards, and more) will be subject to data permission control and remain consistent.

<span id="_3-关于权限，用户最常问的问题是"></span>
# 3. Regarding permissions, the most frequently asked questions from users are...

<span id="_3-1-访问仪表盘时，提示无权限"></span>
## 3.1 When accessing the dashboard, a message indicates insufficient permissions

Cause: The user does not have permission to view the dashboard (even if they have data permissions for the corresponding dataset, this is not sufficient).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d619ee290f694009be78a6969e59b352~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-可查看仪表盘，但某一图表提示无数据权限"></span>
## 3.2 Able to view the dashboard, but a specific chart indicates no data permissions

Cause: A chart in the dashboard references a dataset with row\-level permission control enabled. The user has not been authorized, so the message indicates no data permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c49ba58e1bc4a7fa7a2008b93e06c59~tplv-goo7wpa0wc-image.image) </span>

Similar issues include:

Data permissions for the dataset have been requested, but when performing a visualization query, a message indicates no data permissions.

<span id="_3-3-可查看仪表盘，但点击某一图表进入可视化查询时报无权限"></span>
## 3.3 Able to view the dashboard, but clicking a chart to enter visualization query reports insufficient permissions

Cause: With dashboard permissions, the user can view the dashboard and its data. However, due to lacking view permissions for the dataset referenced by the chart, the user cannot use the dataset for visualization queries.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1cc29e7f48a4d3da72c59261f24d7cb~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-可以使用数据集做可视化查询，但提示无数据权限"></span>
## 3.4 Able to use the dataset for visualization queries, but a message indicates no data permissions

Cause: With dataset view permissions, the user can access the visualization query page. However, without row\-level data permissions for the dataset, no data is visible.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd73754e8f6c4852826ce2c50ecbd4ef~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-权限设置指南"></span>
# 4. Permission settings guide

<span id="_4-1-行权限设置"></span>
## 4.1 Row\-level permission settings

(1) Go to the data permissions page and click the plus icon to add a new data permission rule.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb8e5271cb1e494e9ebbfbbe82f56b47~tplv-goo7wpa0wc-image.image) </span>

(2) Modify the name of the data permission rule for easier identification and differentiation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1d40501087944adbbcab940dc4d88c9~tplv-goo7wpa0wc-image.image) </span>

(3) In rule type, select "Row restriction" to enable row\-level permission control.

(4) Select the dataset for which row\-level permission control is required (such as datasets, projects, charts, dashboards, and so on. Users can only set data permissions for datasets they have management permissions for).

(5) Setting methods: Currently, "Fixed value" and "Dynamic value" are supported.


* Fixed value: Select the row\-level permission field in the dataset to be controlled and set a fixed value (for example, the "Project name" field belongs to "DataWind"). This is suitable for scenarios where there are few controlled users or quick authorization can be achieved through simple operations with user groups.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9625d60918644a5b598c766ebda294b~tplv-goo7wpa0wc-image.image) </span>


* Dynamic value: Select the row\-level permission field in the dataset to be controlled (such as project name), and set it to retrieve the value of a specific attribute field from the user's attributes (for example, "DataWind project", which can be added in Project Center \- User Attributes). When a user affected by this rule accesses the dataset, the value in their "DataWind project" user attribute field (such as DataWind) is used. This is suitable for scenarios where there are many controlled users and it is not convenient to manage them through user groups.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1db9b8020b5a44809e128ef412f2f025~tplv-goo7wpa0wc-image.image) </span>

(6) Permission rules: This refers to the specific configuration of permission rules.


* Permission rules can support multiple conditions. The logical relationship between multiple conditions can be "and" or "or", meaning that all of the following relationships must be satisfied, or any one of the following relationships must be satisfied.

* If the setting method is a fixed value, the logical relationship of the field supports two modes: "belongs to" and "does not belong to".

* Controlled field assignment input box: The dropdown list of options in the controlled field assignment selector randomly displays only 500 values. Values not in the list can be assigned manually by entering them. Multiple values can be assigned.


(7) Assign the configured data permission rules to the users or user groups to be affected.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ffac3ab3bbb4543b1e85f9dd03786ec~tplv-goo7wpa0wc-image.image) </span>

(8) Click the "Save" button in the upper right corner to save and activate the data permission rule, and return to the data permission rule list page.

<span id="_4-2-黑白名单机制设置"></span>
## 4.2 Allowlist and blocklist mechanism settings

Currently, for users of this dataset who have not set row\-level permissions, the system provides two strategies: "Cannot view any data" and "Can view all data".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/522c5166cb2e458089ec66d006b7f7a6~tplv-goo7wpa0wc-image.image) </span>

The default strategy is: users without row\-level permissions cannot view any data.

Users can move the mouse over the dataset name, and a strategy icon will appear on the right. Hovering over the icon displays the current strategy details, and clicking allows switching between strategies.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a66f67ad8365499c8014c80461fa5aec~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-一图总结如何查看全量信息"></span>
# 5. Summary diagram of how to view all information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47861e598fe34ef3a9e5edca6f1aacd6~tplv-goo7wpa0wc-image.image) </span>
