---
title: "Permission Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Permission_Overview"
---

<span id="_1-权限概述"></span>
# 1. Permission overview

Permission refers to security rules or security policies set by administrators or resource owners, which allow users to access, view, and use only the resources for which they have been authorized. Intelligent Data Insight provides you with hierarchical permission management capabilities. Permission management enables administrators and resource owners to grant permissions on resources, which can improve work efficiency and effectively ensure data security.

The following diagram illustrates the permission concept in Intelligent Data Insight:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd1698fbe6dd496e81b29df6f89f4836~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b7bdbcf1eb84154893d6c8ea28c86d5~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-各类角色权限说明"></span>
# 2. Description of permissions for each role


|**Category** |**Role name** |**Permission description** |
|---|---|---|
|**Platform roles** |System administrator |* \*\*On the console page, add users, add projects, configure roles, and other actions;<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8891a422abe34316907282670eb83998~tplv-goo7wpa0wc-image.image) </span><br><br>* **Configure office platform metadata, link office platform accounts, and more on the enterprise domain console page**<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e7281b57cc94471b7b72f4ad43b1514~tplv-goo7wpa0wc-image.image) </span><br><br>* Access the dashboard, datasets, visualization query page, and project center page<br><br>* Configure basic project information, manage project members, grant all resource permissions in the project center, and more |
||Project administrator |* Access dashboards, datasets, visual query pages, and project center pages<br><br>* Configure basic project information, manage project members, grant all resource permissions, and other actions in the project center<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aea33a60521943f5809a46cc66602c32~tplv-goo7wpa0wc-image.image) </span> |
||Project global viewer |Access dashboards, datasets, visual query pages, and project center pages |
||Resource administrator |Can grant permissions on resources such as dashboards, datasets, and data row and column access |
||Regular user |Can access dashboards, datasets, visual query pages, and certain pages in the project center |
|**Functional role** |Role administrator |Configure resource permissions for roles and set role members<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a74a463dd1b649c28d67e07d5d2be5f1~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65eeb255f33e45d5a01429f18cc67e15~tplv-goo7wpa0wc-image.image) </span> |
||User group administrator |Configure resource permissions and group members for user groups (project\-level user groups)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0880a3c0ae7d4f0a889cf8daea195569~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5598ed3357649efb53b260fa3b82524~tplv-goo7wpa0wc-image.image) </span> |
||User attribute administrator |Manage the attribute values of the xxx user attribute in the user list<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4f322f612eb4d0cb95cc96c1c9d6a2e~tplv-goo7wpa0wc-image.image) </span> |


<span id="_3-权限判定逻辑"></span>
# 3. Permission determination logic

As a user, your permissions are subject to multiple checks, which determine what content you can ultimately see. For example, if you have permission to access a dashboard but do not have permission for the dataset used by that dashboard, you will not be able to view the specific charts in the dashboard.

**The logic for permission determination** is shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/794028927e6846c9bb5ee06ae1273acc~tplv-goo7wpa0wc-image.image) </span>
