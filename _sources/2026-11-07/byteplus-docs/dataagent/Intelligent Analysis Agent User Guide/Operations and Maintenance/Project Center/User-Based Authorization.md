---
title: "User-Based Authorization"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/User-Based_Authorization"
---

<span id="ca65c493"></span>
# 1. Overview

In the system, all resources are organized by project, and resources in different projects are completely isolated from each other.

Permission management is responsible for enabling administrators to grant permissions to resources (such as datasets, visual modeling tasks, data connections, and more) for users and user groups.

**Usage scenarios:** 


* **Permission management**: Administrators can efficiently and quickly manage resource authorization for users and user groups, and can authorize resources in batches using folders.

* **Quick review of user permissions**: Administrators can view the effective permissions users have for resources, and check how these permissions were obtained, making it easy to quickly review permissions.

* **Individually authorize specific users in a user group**: Individual authorization for specific users in a user group can be achieved by excluding group authorization.


**Caution: Only project administrators can access permission management**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/479063aee3234856960b7c79b7b56674~tplv-goo7wpa0wc-image.image) </span>

<span id="9d91f5fd"></span>
# 2. Getting started

<span id="03e7a321"></span>
## 2.1 Modify user permissions

Operations for modifying user permissions include granting permissions, revoking permissions, and excluding group authorization. The operation process is the same for all.

**Step 1**: Go to the "Permission Management" page and search for the user whose permissions need to be modified

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e914f182f501403cb68d19cb7fc9e781~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Select the resource type whose permissions need to be modified

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/283ef59ad6c24e45a529b4826938b388~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Search for the resource name to be modified. If it is under a folder, click the folder name to expand

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1166ae715e34a808b0535f1927b8451~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: Adjust the user's permissions as needed

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2f3d0013195409d82256ca61b7fa29a~tplv-goo7wpa0wc-image.image) </span>

<span id="49beae75"></span>
# 3. Feature overview

<span id="5dd24e0a"></span>
## 3.1 Description of resource permissions

<span id="6e1b66fb"></span>
### Project

Project permissions include the following four types:


* **View**: Grants access to enter the project, allows viewing resources within the project for which the user has permission, and enables operations such as creating new folders.

* **Edit**: In addition to project view permissions, allows operations such as creating new datasets.

* **Global view**: Grants project edit permissions plus view permissions for all datasets within the project. If a personal dataset is linked, all data can be viewed.

* **Management**: This refers to having management permissions for resources within the project, allowing permission management, project deletion, and other operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3043ccf2bc34355824cea89fbccf522~tplv-goo7wpa0wc-image.image) </span>

<span id="f5f85c6b"></span>
### Dataset

Dataset permissions include the following four types:


* **View\-only permission**: This allows viewing data only, without permissions to download or copy data.

* **View permission**: This allows querying datasets on the visual query page, adding temporary fields, downloading, configuring monitoring, viewing dataset details, and other operations.

* **Edit permission**: In addition to having view permission for datasets, this also allows modifying dataset models, routine configurations, alias management, and other operations.

* **Management permission**: In addition to having edit permission for datasets, this also allows permission management, deletion, and other operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2f3d0013195409d82256ca61b7fa29a~tplv-goo7wpa0wc-image.image) </span>

<span id="2581c6a1"></span>
### Visual modeling task

Visual modeling task permissions include the following three types:


* **View permission**: This allows viewing the details page of visual modeling tasks, but does not support any operations.

* **Edit permission**: In addition to having view permission for visual modeling tasks, this also allows modifying the processing flow and runtime configuration of visual modeling tasks, and other operations.

* **Management permission**: In addition to having edit permission for visual modeling tasks, this also allows permission management, deletion, and other operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e823e76e592407388a1857c12155f00~tplv-goo7wpa0wc-image.image) </span>

<span id="9e74d36b"></span>
### Data connection

Data connection permissions include the following three types:


* **View permission**: This allows viewing the details page of the data connection and using the data connection to create datasets.

* **Edit permission**: In addition to having view permission, this also allows modifying configurations and other operations.

* **Management permission**: In addition to having edit permission, this also allows permission management, deletion, and other operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da891a52be0f40599c87af0eb7552008~tplv-goo7wpa0wc-image.image) </span>

<span id="74b970a3"></span>
## 3.2 View specific resource content

On the permission management page, clicking the resource name allows navigation to the resource's details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab5b8de9ca35447d9aaccb62189c22f4~tplv-goo7wpa0wc-image.image) </span>

<span id="45a45238"></span>
## 3.3 Authorization

<span id="c201f297"></span>
### Authorize a single resource

Select the resource to be authorized. You can control whether permission is granted by toggling the switch button next to the corresponding permission.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4de9f18a52c4f53929d4eec507cbee2~tplv-goo7wpa0wc-image.image) </span>

<span id="4ea2c779"></span>
### Folder authorization

When a resource is located within a folder, modifying the folder's permissions will affect the permissions of all resources under that folder.


* For example, to grant edit permissions to all resources in a folder in bulk, simply enable the edit permission for the folder. After the operation is successful, the user will obtain edit permissions for both the folder and all resources within it, and will also receive permissions for any resources added to the folder in the future. Conversely, if the permission is revoked, it will also be revoked for all resources at the same time.

* While batch authorization through the folder is supported, it is also possible to manage permissions for individual resources within the folder separately.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5da0ac7b37ee438386e5d368e9d0ec5f~tplv-goo7wpa0wc-image.image) </span>

<span id="5e7d9a7c"></span>
### View permission acquisition methods

When a user has permission for a resource, the user can view how the permission was acquired.


* If it is shown as an individual, this means the permission was either applied for by the individual or granted to the individual separately.

* If it is shown as a user group or role, this means the resource was authorized to a user group, and the user inherits the user group permissions as a member of that group.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d16a0b01773843df9446ecf297524447~tplv-goo7wpa0wc-image.image) </span>

<span id="c95a07d4"></span>
### Block group authorization

The concept of group authorization means that the current resource is authorized to a user group, department, or group, and users inherit permissions from the user group. Blocking group authorization allows control over whether a user inherits permissions from the user group.


* After enabling the "Block group authorization" feature, the user's permissions for the resource will no longer be inherited from the user group, and only permissions acquired individually will be retained.

* After disabling the "Block group authorization" feature, the user's permissions for the resource will be inherited from the user group, and the user's permissions for the resource will be the union of permissions acquired individually and those acquired from the user group.


**Batch disable group authorization**：

To batch disable group permissions for all datasets for a specific user, hover the mouse over "Block group permissions" to display the "Disable all" popup. Click it to disable group permissions for the specified resource type.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e376001fc2444189917bfcce613a0f49~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18cff9ba28214c82876c5c41b2df5a33~tplv-goo7wpa0wc-image.image) </span>
