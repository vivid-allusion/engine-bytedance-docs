---
title: "User Group Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/User_Group_Management"
---

<span id="_1-概述"></span>
# 1. Overview

User group management refers to the functionality for grouping and maintaining users. Project administrators can configure and manage user groups based on departments and functions. Supports departments, system\-level user groups, and project\-level user groups. This feature is available only to project administrators.


* Department: All levels of departments within the company's organizational structure

* System\-level user group: User groups associated with the system level

* Project\-level user group: User groups defined within a specific project.


<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-功能须知"></span>
## 2.1 Feature notes

(1) Departments and system\-level user groups cannot be edited on the user management page.

(2) A user can belong to multiple system\-level and project\-level user groups, but can belong to only one department\-level user group.

(3) Members of project\-level user groups can be managed by project administrators in the project center's user group management interface, while members of system\-level user groups must be managed in the relevant system management interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04b45e7f7bad41f9b56ceeca9b738f7f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-用户组查看"></span>
## 2.2 Viewing user groups

User group list: In the user group list, departments and project\-level user groups are expanded by default, while system\-level user groups are collapsed by default.

Search user groups: Supports fuzzy search and real\-time queries by user group name and description.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2ce9e6ea96c44b6ad196bc43058987b~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-用户组编辑"></span>
## 2.3 Editing user groups

 **(1) Create a new user group**

Supports creating project\-level user groups, setting the user group name, display name, remarks, and more. Clicking [Submit] creates a new project\-level user group in the project and generates a user group ID (serving as the unique identifier for the user group).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0880a3c0ae7d4f0a889cf8daea195569~tplv-goo7wpa0wc-image.image) </span>

After creating a user group, you can immediately proceed to the authorization step.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5598ed3357649efb53b260fa3b82524~tplv-goo7wpa0wc-image.image) </span>

 **(2) Authorize a user group**

Supports authorizing departments, system\-level user groups, and project\-level user groups. Click [Add Authorization] to go to the permission management page and authorize project resources for the user group. For details, refer to the documentation "Project Center \- Permission Management". Project permissions support setting scopes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47824fb82fde42b2a51810cb86889c96~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-用户组管理"></span>
## 2.4 User group management

Support management of project\-level user groups, including adding users, adding subgroups, and removing users/subgroups.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddb0439e92fb45019e1cfcd6874fb570~tplv-goo7wpa0wc-image.image) </span>

After clicking the group name, the following page appears.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1da32950ba0d46aabc6f46484265b45d~tplv-goo7wpa0wc-image.image) </span>

(1)**Add user**

Add users from the current project's users to this user group. Supports fuzzy search by username or email. The dropdown search scope is limited to users in the project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0a09ee9c0014fb3a9c5aca092b9744f~tplv-goo7wpa0wc-image.image) </span>

(2)**Add subgroup**

Add user groups or departments from the project\-level user groups or department options included in the current project to this user group as its subgroups. Supports fuzzy search by user group name or department name.

(3)**Remove user/subgroup**

Remove users or subgroups from the user group, supporting single or batch removal.

(4)**Delete user group**

Click Delete to remove the user group.

(5)**Permission management**

The permission interface is basically consistent with the one used when creating a new user group.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a51f493e57834a5eabb3a17c92fc9e1e~tplv-goo7wpa0wc-image.image) </span>
