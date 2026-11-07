---
title: "Resource-Based Authorization"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Resource-Based_Authorization"
---

<span id="c8a9b9dc"></span>
# 1. Overview

On the resource\-based authorization page, users can view information about resource owners and managers, and perform operations such as authorization, transferring ownership, and downloading the permission list.


* Ordinary users can perform operations such as transferring ownership, granting authorization, and adding approvers on this page.

* Project administrators can manage all resources under the project.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67926fb2eade44148d5cd0b4d7f4119e~tplv-goo7wpa0wc-image.image) </span>

<span id="d0085aff"></span>
# 2. Quick start

<span id="bd35135e"></span>
## 2.1 Transfer ownership

**Step 1**: Go to the resource\-based authorization page in the project center and search for the resource whose ownership needs to be transferred.


* Ordinary users can filter resources by selecting "Mine" as the resource owner.

* Project administrators can transfer ownership of all resources under the project.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0ce1ab9c40d455293d2fd847bf34a85~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: You can select multiple resources from the list to transfer ownership in bulk, or click the Transfer Ownership button in the action bar after selecting a single resource.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0559e4ece7b44cd9ff065ba05eeb0a0~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Search for the recipient of the resource, then click Confirm to transfer ownership.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ff9c698b24941c38e5204194f6686df~tplv-goo7wpa0wc-image.image) </span>

<span id="df13826f"></span>
## 2.2 Authorization

**Step 1**: Go to the resource\-based authorization page in the project center and search for the resource to be authorized.


* Ordinary users can filter resources by selecting "Mine" as the resource owner, or filter resources where they are listed as a resource manager.

* Project administrators can grant authorization for all resources under the project.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86bf3bef8baf46818541d55c7f743c14~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: You can select multiple resources from the list to grant authorization in bulk, or click the Authorize button in the action bar after selecting a single resource.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c13b0e524d754b20b7e4488b6eaea716~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Search for the permission type and user to be authorized, then click Confirm.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d0c5deb9b8a425ca4d091f03ba497f3~tplv-goo7wpa0wc-image.image) </span>

<span id="1a72d011"></span>
## 2.3 Permission management (view resource\-based authorization details)

**Step 1**: Go to the resource\-based authorization page in the project center and click the "Permission Management" page in the action bar after selecting a resource.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf19f88a5724420895ff4ac19f4cfd82~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: After clicking, you will enter the permission management page for that resource, where you can view users and user groups that currently have resource\-based authorization. You can also modify their permissions, grant permissions, and download the permission list on this page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1605a35fee5544a0a87cc0f6af2604ba~tplv-goo7wpa0wc-image.image) </span>

<span id="52b8a260"></span>
## 2.4 Download the permission list

The permissions management page supports downloading a permissions list, allowing you to download all individuals, user groups, and permission details currently authorized for a specific resource.

There are two ways to download the permissions list:


* After selecting one or more resources, click the "Download permissions list" button below to download in bulk.

* Click the "Permissions list download link" in the upper right corner to download the permissions list for all resources under the current filter conditions  **(this option is only visible to project administrators).** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb108b1411164413bcdb48deca04ebd8~tplv-goo7wpa0wc-image.image) </span>

<span id="26cfa2ef"></span>
# 3. Feature overview

<span id="555f746d"></span>
## 3.1 Permissions list content


* Resource type

   * app: Project

   * data_set: Dataset

* Resource name

* Resource ID

* Authorized entity: Includes name and email prefix

* Authorized entity type

   * User: Authorized individually

   * User group: Authorized collectively

* Department

* Group type: When the authorized entity type is user group, the group type will be indicated

* Permissions granted: Includes view, edit, and manage permissions

* Permission source: Indicates who performed the authorization operation for the user


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/faf79451c23540f18c6adabbc9978eb8~tplv-goo7wpa0wc-image.image) </span>
