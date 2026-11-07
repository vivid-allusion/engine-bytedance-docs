---
title: "Resource Authorization"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Resource_Authorization"
---

<span id="_1-概述"></span>
# 1. Overview

In the Intelligent Data Insight product, visual modeling tasks, datasets, charts, dashboards, and other items are all defined as resources. On the Project Center \-\-\> Resource Permissions page, users can view the owner and manager information for each individual resource, and perform operations such as granting permissions, transferring permissions, and other operations.

The page consists of two sections: the search bar at the top and the list section below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5c57aab58a34ba8a57b176e14e79d9d~tplv-goo7wpa0wc-image.image) </span>


* **Search bar**

   * Resource ID or name: You can search by resource ID ([How to Obtain Resource IDs](https://docs.byteplus.com/docs/undefined/69c349bf50cba904c1f625e4)) or resource name. To search for multiple items, separate resource names with a comma ",".

   * Resource owner: You can view the resource list details from the perspective of which user owns the resource, or quickly filter resources belonging to the current user by clicking "Only mine".

   * Resource manager: You can view the resource list details from the perspective of the resource manager (single user or user group).

   * Resource type: By default, all resources are shown. You can filter by dashboard, dataset, visual modeling, chart, and other types.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58db31b60ba94c83b7f730bb589c1983~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* **List section**

   * Resource ID: [How to Obtain Resource IDs](https://docs.byteplus.com/docs/undefined/69c349bf50cba904c1f625e4).

   * Name: The resource name. Click to go to the resource details page.

   * Resource type: The specific type of the resource.

   * Resource owner

   * Resource manager

   * Actions: Transfer owner allows you to transfer ownership of the resource to another user, grant permissions allows you to assign permissions for the resource, and permission management allows you to view the details of permissions granted for the resource.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>The requirements for users transferring permissions are as follows</strong></div>



* <div data-tips="true" data-tips-type="tip">Project administrators can transfer ownership of all resources under the project.</div>


* <div data-tips="true" data-tips-type="tip">Resource administrators can transfer ownership of resources they manage to others.</div>



<span id="_2-使用场景"></span>
# 2. Use cases

<span id="_2-1-权限转移"></span>
## 2.1 Permission transfer

When a resource owner leaves or changes roles, they can batch transfer resources they created to the successor.

**Procedure:** 

(1) Search for the resource to be transferred, and click "Transfer permissions".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87160bb2923d4d3ea21714d8b3cc4591~tplv-goo7wpa0wc-image.image) </span>

(2) Enter the username of the recipient, and click "OK".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0b0523cf0e3464986af1ec4f031f3af~tplv-goo7wpa0wc-image.image" width="610px" /></div>


Note: All project members can access the permission transfer page.

<span id="_2-2-快速授权"></span>
## 2.2 Quick authorization

Grant a user view, edit, or manage permissions for a specific dashboard or dataset.

**Procedure:** 

(1) Search for the resource to be authorized, and click "Grant permissions".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24a85637cf224438a8709cad4b0c7631~tplv-goo7wpa0wc-image.image) </span>

(2) Select the permission type and search for authorized users. To add multiple users at once, copy a string of users in the format "test1,test2,test3", paste it into the input box to perform batch operations, and click "OK" to save.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f2607db558940579649f942dca19951~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-3-查看资源详情"></span>
## 2.3 View resource details

Users, especially administrators, can use this page to query resources, view the owner of a specific resource or multiple resources, and see which users have been authorized for each resource.

**Operation process:** 

(1) After obtaining the resource name or resource ID, enter it in the input box to perform a fuzzy search.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fd2843ebe304a66bf9e76c161d5bd99~tplv-goo7wpa0wc-image.image) </span>

(2) Click [Permission Management] to view the details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c50ae9a756954876a6578298c2a76de0~tplv-goo7wpa0wc-image.image) </span>

(3) On the details page, view the resource's authorization status from the perspective of individual users, user groups, or roles.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e714b54e3d7147fca10735f9c8436ca0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-资源权限转移"></span>
## 3.1 Resource permission transfer

When a user creates a resource, the system records that user as the owner. The transfer includes both ownership of the resource and administrator permissions. After ownership is transferred, the original owner's permissions are cleared, and the transferee receives ownership and administrator permissions.

Users can transfer resources they own to a transferee; project administrators can transfer any resource.

<span id="_3-2-权限转移前后的表现"></span>
## 3.2 **Changes before and after permission transfer**

When resource x is transferred from A to B, the system changes the owner of x from A to B, clears A's permissions for the resource, and B receives ownership and administrator permissions.

<span id="_3-3-支持批量授权-转移"></span>
## 3.3 **Batch authorization and transfer**

When multiple resources are selected, the "Batch Authorization" and "Batch Transfer" buttons appear below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d70bd96fb3a4985b7da99238a2ede45~tplv-goo7wpa0wc-image.image) </span>

Multiple resources can be authorized or have their permissions transferred at once.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b1f7bbbbb1e452fa006dafcebca275c~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c7aaf9035424a5dadcb266f48fe5b4c~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-4-权限清单查看与下载"></span>
## 3.4 Viewing and downloading the permission list


* **Viewing a single resource**


(1) Click [Permission Management] to enter the detailed management page for the resource, where you can view the complete list of users with permissions for the resource.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7ee891bb4d5490c9ec8708d4e54c001~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da1dd07701d74269b6053a96b5a5da3f~tplv-goo7wpa0wc-image.image) </span>

(2) Although project administrators/global viewers are not displayed here, there are actual permission entries for resources. As shown in the figure above, by clicking to view, you can see the project administrator and global viewers for the project to which the resource belongs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e0e773f6be24c50af17df12e13bf4f9~tplv-goo7wpa0wc-image.image) </span>


* **Permission list download**


 **(1) Download the permission list for a single resource**

Click [Permission Management] to enter the detailed management page for the resource, then click the [Permission List] button in the upper right corner to download.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da1dd07701d74269b6053a96b5a5da3f~tplv-goo7wpa0wc-image.image) </span>

After downloading and opening the Excel file, you can view the permission list for the resource and the corresponding project permission list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/023b1c231f9941d7b33d78e0337bff52~tplv-goo7wpa0wc-image.image) </span>

 **(2) Batch download permission lists**

After selecting multiple items on the resource list page, the [Download Permission List] button will appear at the bottom. Click to download.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ace4337d846a4521828ffda15264449e~tplv-goo7wpa0wc-image.image) </span>
