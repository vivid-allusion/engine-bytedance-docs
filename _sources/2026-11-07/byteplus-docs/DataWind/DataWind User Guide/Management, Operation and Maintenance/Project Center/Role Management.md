---
title: "Role Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Role_Management"
---

<span id="_1-概述"></span>
# 1. Overview

A role is a collection of permissions. Role management enables batch authorization of users for a specific role within a project, reducing repetitive and complex authorization operations. A role can include multiple users. This feature is available only to system administrators and certain users with role management permissions. Users without the required permissions will not see the entry point for this feature. ((This feature is a value\-added module, currently available only for on\-premises deployments, and supported in V2.62.0 and later versions. To use this feature, please contact your company's sales representative or customer success manager for purchase information.))

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d5421ca0d8043d5ae8cd4d54305245c~tplv-goo7wpa0wc-image.image) </span>

<span id="cfcc27e4"></span>
# 2. Specific operations

<span id="_3-1-新建角色"></span>
## 2.1 Create a role

System administrators or users with "role management" permissions can go to "Project Center" \- "Permission Control" \- "Role Management" and click Create Role. You can configure the basic information for the role.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14d5190a7219442f8b5abd542725b891~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-资源权限"></span>
## 2.2 Resource permissions

Click a role to view the resource permissions for that role within the product space, including view permissions, edit permissions, and global view permissions.


|Permission categories |Resources |View permission |Edit permission |Global view permission |Manage permission |
|---|---|---|---|---|---|
|Resource permission |Project |This grants permission to access and enter the project, view resources within the project for which you have permission, and create personal dashboards or folders. |In addition to project view permission, you can also create public dashboards, datasets, or folders in the root of the public directory. |With project edit permission plus view permission for all public dashboards, public dashboard folders, and datasets within the project, you can view all data. |This grants manage permission for resources within the project, allowing permission management, project deletion, and other operations. This is the highest level of resource permission. |
||Dashboard |This allows you to view dashboards, add to favorites, subscribe to standard subscriptions, and download charts. |In addition to having permission to view dashboards, users can also edit dashboards and perform other operations. |/ |In addition to having permission to edit dashboards, users can also manage permissions, delete, move dashboards, copy dashboards, and perform other operations. This is the highest level of resource permission. |
||Dataset |On the visual query page, users can query datasets, add temporary fields, download, configure monitoring, view dataset details, and perform other operations. |In addition to having permission to view datasets, users can also modify dataset models, configure routines, manage aliases, and perform other operations. |/ |In addition to having permission to edit datasets, users can also manage permissions, delete, and perform other operations. This is the highest level of resource permission. |
|Note | |This permission is generally granted to resource viewers. |This permission is generally granted to resource collaborative editors. |This permission is generally granted to the leader of the business to which the project belongs, provided they do not participate in permission approval. |This permission is generally for the resource creator or users who are granted collaborative management of the resource.<br><br>Caution: It is not possible to grant others management permission for personal dashboards. |


<span id="_3-3-行列权限"></span>
## 2.3 Row and column permissions

As shown in the figure, click Row and Column Permissions to view the permission name, type, associated dataset name, and permission rule details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5de8e820ef74340a54bc7e24e2f2c4f~tplv-goo7wpa0wc-image.image) </span>

You can click to add row and column permissions, or delete existing row and column permissions.

For more details, see: [DataRow and Column Permissions](https://docs.byteplus.com/docs/DataWind/109982).

<span id="_3-4-成员详情"></span>
## 2.4 Member details

<span id="_3-4-1-非空状态"></span>
### 2.4.1 Non\-empty state

As shown in the figure, click Member Details. When the Member Details page is not empty, you can view the list of members and add members.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a74a463dd1b649c28d67e07d5d2be5f1~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-2-空状态"></span>
### 2.4.2 Empty state

As shown in the figure, click Member Details. When the Member Details page is empty, clicking Add Member will open a new page and redirect to the Volcano Engine Console (Portal) Edit Role page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1723c65615a4fcd8b950341a6a8bc56~tplv-goo7wpa0wc-image.image) </span>

When redirected to the Volcano Engine Console (Portal) Edit Role page, you need to complete the following:

 **(1) Basic information**

You can enter the role name and a description for the role, and assign a role owner (who can view, edit, or delete the current role).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65eeb255f33e45d5a01429f18cc67e15~tplv-goo7wpa0wc-image.image) </span>

 **(2) Permission settings**


* **Select accessible projects**: You can choose to make this role available to all projects, or specify certain project spaces.

* **Select accessible products**: If you have purchased multiple data platform products, you can select which products this role will have access to (multiple selections allowed). If you have only purchased Intelligent Data Insights (DataWind), simply select Intelligent Data Insights.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/467a2ee1354a4fce93203f584f772e24~tplv-goo7wpa0wc-image.image) </span>

 **(3) Role members**


* Member scope: You can restrict members to specific departments.

* Member maintainer: You can modify role members within the defined member scope.

* Members \- fully open: This role is available to all users, and new users are automatically granted access.

* Members \- partially open: This role is available to some users, and new users must be granted access manually.

   * Authorization scheme \- fixed value: You can add users directly or add users by department.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83121a7d9d9e42cd979c3796a9722aed~tplv-goo7wpa0wc-image.image) </span>


* Authorization method \- dynamic value: You can add users based on rule conditions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a104d3e8e174995b8783605ef78b417~tplv-goo7wpa0wc-image.image) </span>
