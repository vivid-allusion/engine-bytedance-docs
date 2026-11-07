---
title: "Permission Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Permission_Management"
---

<span id="_1-概述"></span>
# 1. Overview

Permission refers to security rules or security policies set by administrators or resource owners, which allow users to access, view, and use only the resources for which they have been authorized. Intelligent Data Insight provides you with hierarchical permission management capabilities. Permission management enables administrators and resource owners to grant permissions on resources, which improves work efficiency and effectively ensures data security. In the Intelligent Data Insight system, all resources are organized by project, and resources in different projects are isolated from each other. Permission management is responsible for allowing administrators to grant permissions on resources (such as datasets, charts, and dashboards) to these users or user groups. This feature module is accessible only to project administrators.

Permission management is a relatively complex module for an enterprise\-level platform. Therefore, we have prepared a **Permission Guide** for your reference. This document only introduces the functional operations of the permission management module in the project center. To learn more about the permission system, please refer to the **Permission Guide** in the following documentation:


* Permission system feature introduction: see [Permission Overview](https://docs.byteplus.com/docs/DataWind/Permission_Overview).

* Documentation describing various feature permissions: see [Authorization Operation Manual](https://docs.byteplus.com/docs/DataWind/Permission_Operation_Manual).


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios


* **Permission management**: Administrators can efficiently and quickly manage resource authorization for users or user groups, and can use folders to perform batch authorization of resources.

* **Quickly view user permissions**: View the final permissions a user has on resources, and check how the permissions are obtained, making it easy for administrators to quickly review permissions.

* **Individually authorize specific users in a user group**: By using the [Group Authorization Exclusion] method, it is possible to individually authorize specific users within a user group. To facilitate authorization and management, the project administrator grants view permissions for 10 dashboards, such as dashboards A, B, and C, to department M. However, there is an intern in department M who should not view the data of dashboard A. In this case, the administrator can enable the [Block Group Authorization] feature for the intern on dashboard A and revoke the individual's view permission to meet the management requirements.


<span id="_2-2-使用过程示例"></span>
## 2.2 Example of the usage process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/097f49c151e944f190a7333446a24e61~tplv-goo7wpa0wc-image.image) </span>

(1) Click Project Center;

(2) Go to the Permission Management page;

(3) Search for or directly select the user to be authorized (as shown in the figure above, select the user);

(4) In the resource authorization module, switch to the type of resource to be authorized (such as Dashboard). The system currently supports five types of resources: Project, Dashboard, Dataset, Visual Modeling Task, and Data Connection (Note: Data Connection is supported in version V2.50.0 and later);

(5) Search for and select the specific resource to be authorized. Click the lock icon under the permission to be granted (such as View/Edit). After successful authorization, the lock will change from closed to open;

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da4527d42c0243ec96b490196f15f572~tplv-goo7wpa0wc-image.image) </span>

(6) After successful authorization, the user (for example, yoyo) will have edit permission for the resource (Dashboard Test (Standard)), can view the data of the dashboard, and can edit the content of the dashboard.

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-选择授权对象"></span>
## 3.1 Select the authorization target

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8248c4f5205441c9a353a9626fa98ba6~tplv-goo7wpa0wc-image.image) </span>

In the Permission Management \- User List, you can browse or enter **usernames and more** to perform a fuzzy search to find the specific user to be authorized.

<span id="_3-2-选择要授权资源类型"></span>
## 3.2 Select the type of resource to authorize

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19080366619e42beb0f636f5e3421f60~tplv-goo7wpa0wc-image.image) </span>

You can click to switch and select the type of resource to be authorized. The system currently supports five types of resources: Project, Dashboard, Dataset, Visual Modeling Task, and Data Connection

**Note:** 


* Only public dashboards can be managed and authorized on the Permission Management page; personal dashboards are not included

* Data Connection is supported in version V2.50.0 and later


<span id="_3-3-搜索资源"></span>
## 3.3 Search for resources

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cb1e2776a5a43978ccf9698f140f19d~tplv-goo7wpa0wc-image.image) </span>

You can enter the resource name keyword in the input box and press the Enter key to search for and find the resource to be authorized.

<span id="_3-4-资源权限说明"></span>
## 3.4 Description of resource permissions

Resource permissions include four types: view only, view, edit, and manage. For details on the permission types corresponding to each resource, see [Detailed Explanation of Permission Features](https://docs.byteplus.com/docs/DataWind/Detailed_Explanation_of_Permission_Features).

<span id="_3-5-查看具体资源内容"></span>
## 3.5 View specific resource content

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3c93fd8c0a34f52aa57f3d4ab77855f~tplv-goo7wpa0wc-image.image) </span>

Move the mouse over the resource name and click to navigate to the resource details page for viewing, which helps the person granting the permission confirm the information.

<span id="_3-6-进行单个资源授权"></span>
## 3.6 Grant permission to an individual resource

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f792a0dfeab4817baf329e2860cf799~tplv-goo7wpa0wc-image.image) </span>

Select the resource to be authorized, then click the lock icon below the permission to be granted (such as Edit). To revoke a granted permission, click the blue lock icon corresponding to that permission.

<span id="_3-7-进行批量资源授权"></span>
## 3.7 Grant permissions to multiple resources in bulk

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5b989bc0e684f7eafcbe01d0c197186~tplv-goo7wpa0wc-image.image) </span>

Select the folder to be authorized and grant the corresponding permission (such as Edit). After the operation is successful, both the folder and all resources it contains are granted that permission (such as Edit), and the user will also obtain permissions for resources added to the folder later. Conversely, when revoking the permission, it will also be revoked for all associated resources.

Currently, when granting permissions in bulk to a folder, it is also possible to manage permissions for individual resources within the folder separately. As shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a1f58f9b4754d46a676a2182a178da8~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-屏蔽组授权"></span>
## 3.8 Block group authorization

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27f2b7cb038c45e69e3c7a7939d5fe96~tplv-goo7wpa0wc-image.image) </span>

After enabling the "block group authorization" feature, the user's permissions for the resource will no longer inherit permissions from the user group. After disabling this feature, the user's permissions for the resource will inherit permissions from the user group. The user's permissions for the resource are the union of permissions obtained individually and those obtained through the user group.

The following is an example scenario for this feature: To facilitate authorization and management, a project administrator grants view permissions for dashboards A, B, C, and seven other dashboards (ten in total) to department M. However, there is an intern in department M who should not view the data of dashboard A. In this case, the administrator can enable the "block group authorization" feature for the intern on dashboard A and revoke the individually granted view permission, thus achieving the desired effect.
