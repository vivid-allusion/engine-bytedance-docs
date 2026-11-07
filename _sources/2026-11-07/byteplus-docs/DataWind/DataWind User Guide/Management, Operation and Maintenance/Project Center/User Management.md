---
title: "User Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/User_Management"
---

<span id="_1-概述"></span>
# 1. Overview

User management refers to the ability of project administrators to add, delete, edit, and authorize users within a project. This functionality is available only to project administrators.

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-功能须知"></span>
## 2.1 Feature notes

User statuses are divided into [Enabled] and [Disabled]. By default, all users newly added to a project are enabled. Disabled users cannot access the project, but the system retains their permission configurations within the project.

<span id="_2-2-添加用户"></span>
## 2.2 Add users

Multiple users can be added at once. When adding users to a project, you can simultaneously grant project permissions: [View Permission], [Edit Permission], and [Manage Permission].

There are two main ways for users to join a project:


* When a new user (who must be a system user) applies for and successfully obtains permission for a project resource, the system automatically adds that user to the project.

* Project administrators can manually add users. See the steps below.


**Step 1**: Go to the user management page, then click the "Add User" button in the upper right corner.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/150e93e2cd904567a9c1df3fd7461c39~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: In the add user dialog, you can search for users by username or email prefix and select the type of permission to grant. To grant the same project permission to multiple users, repeat this step, **or use commas to separate multiple users for batch search and addition**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6212f9eb78d247d48172b3b098f31d24~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Click "Confirm" to complete the user addition process.

<span id="_2-3-搜索用户"></span>
## 2.3 Search users

Supports fuzzy search and real\-time queries by username, email prefix, or department.

<span id="_2-4-编辑用户"></span>
## 2.4 Edit users

(1) Status: "Enabled" is selected by default, but you can change the status.

(2) User group (system\-level/department): Displayed only; not editable.

(3) User group (project\-level): Displays the project\-level user group associated with the selected user. This field is optional. The dropdown list includes all project\-level user groups for the project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/787aa901214e41b98bd2a1c27622066a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-为用户赋权"></span>
## 2.5 Grant permissions to users

In the user list, click the "Grant Permissions" button to go to the permission management page. For specific instructions, refer to the documentation "Project Center \- Permission Management"

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/195f5aca00de4d9c816328613d5e0a19~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-删除用户"></span>
## 2.6 Delete users

In the user list, click the "Delete" button to remove users (removal is limited to the project). If a user is the sole administrator of a resource within the project, deletion will fail.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bba25bf23a8f40d39a6dffc8962696dd~tplv-goo7wpa0wc-image.image) </span>

Batch deletion of multiple users is supported. To do so, select the users to be deleted and click Delete at the bottom of the user list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21f6bc7ad2244338846d1c118ad15eaa~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-7-添加用户组"></span>
## 2.7 Add user groups

Administrators can also add users to different user groups. User groups are categorized as department, system\-level, and project\-level.


* Department user groups: Each department within the company's organizational structure

* System\-level user groups: User groups associated with the system hierarchy

* Project\-level user groups: User groups customized within a specific project.


Note: Department and system\-level user groups cannot be edited on the user management page. For user group management operations, see [User Group Management](https://docs.byteplus.com/docs/DataWind/User_Group_Management).
