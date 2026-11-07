---
title: "User Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/User_Management"
---

<span id="_1-概述"></span>
# 1. Overview

User management refers to the ability of project administrators to add, delete, edit, and authorize users within a project. This functionality is available only to project administrators.

<span id="_2-功能介绍"></span>
# 2. Feature overview

<span id="_2-1-功能须知"></span>
## 2.1 Important notes

User status is divided into "Enabled" and "Disabled". By default, the status of newly added users in a project is "Enabled". Disabled users cannot access the project, but the system retains their permission configuration within the project.

<span id="_2-2-添加用户"></span>
## 2.2 Add users

Multiple users can be added at once. When adding users to a project, you can simultaneously grant project permissions: "View permission", "Edit permission", "Global view permission", and "Manage permission".

There are two main ways for users to join a project:


* When a new user (who must be a system user) applies for and successfully obtains permission to access a project resource, the system automatically adds the user to the project.

* Project administrators can manually add users. See the steps below.


**Step 1**: Go to the user management page and click the "Add user" button in the upper right corner.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e096b90eb4047919f137408b297e1a0~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: In the add user pop\-up window, you can search for users by username or email prefix and select the permission type to grant. To grant the same project permission to multiple users, repeat this step, **or use English commas to separate multiple users for search and addition.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a966abee16494f9d8aab3b78b96eabec~tplv-goo7wpa0wc-image.image" width="610px" /></div>


Description of project permissions:


* View permission: Grants access to enter the project, allows viewing resources for which the user has permission within the project, and enables actions such as creating personal folders.

* Edit permission: In addition to view permission, allows actions such as creating datasets or folders in the root of the public directory.

* Global view permission: Grants edit permission plus view access to all datasets within the project, allowing the user to view all data.

* Management permissions: This refers to having management permissions for all resources within the project, allowing actions such as permission management and project deletion. It is the highest level of resource permission.


**Step 3**: Click "Confirm completion" to add the user.

<span id="_2-3-搜索用户"></span>
## 2.3 Search for users

Supports fuzzy search by username, email prefix, or department, with real\-time results.

<span id="_2-4-编辑用户"></span>
## 2.4 Edit users

(1) Status: "Enabled" is selected by default. You can modify the status. After disabling, the user will be prohibited from accessing the current project, but their previous permission configuration in the project will be retained.

(2) Associated user group (project level): Displays the project\-level user group associated with the currently selected user. This is not a required field. The dropdown options are limited to project\-level user groups belonging to this project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8799c5bef8741f18ec7981968f9f2b0~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-为用户赋权"></span>
## 2.5 Grant permissions to users

In the user list, click the "Grant permissions" button to go to the permission management page. For detailed instructions, refer to the documentation [User-Based Authorization](https://docs.byteplus.com/docs/dataagent/User-Based_Authorization).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c73290b5123f4859a9b401f605668f06~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-删除用户"></span>
## 2.6 Delete users

In the user list, click the "Delete" button to remove the user (removal is limited to the project). If the user is the sole administrator of a resource within the project, deletion will fail.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef8ec947c63d4ac7a16aaae4699106fb~tplv-goo7wpa0wc-image.image) </span>

Supports batch deletion of multiple users. To do so, select the users to be deleted and click "Delete all" at the bottom of the user list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf228006af254c9ba6ff510a578fb167~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-7-添加用户组"></span>
## 2.7 Add user groups

Administrators can also add users to different user groups. User groups are categorized as department, system\-level, and project\-level.


* Department user groups: Various departments within the company's organizational structure

* System\-level user groups: User groups associated with the system level

* Project\-level user groups: User groups customized within a specific project.


Note: Department and system\-level user groups cannot be edited on the user management page. For user group management operations, see [User Group Management](https://docs.byteplus.com/docs/dataagent/User_Group_Management).
