---
title: "User Group Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/User_Group_Management"
---

<span id="_1-概述"></span>
# 1. Overview

User group management refers to the functionality for grouping and maintaining users. You can create user groups within a project, add members to user groups, and grant permissions to user groups. This allows you to manage user permissions in bulk or allow members of a user group to obtain permissions in bulk. Creating a user group requires project or other management permissions.

<span id="20d91fdc"></span>
# 2. Quick start

<span id="87527485"></span>
## 2.1 Create a user group


1. Go to the user group management page in the project center, click the “+” icon in the user group list, and you will be taken to the BytePlus access control interface to configure the user group.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a25b2c772ad4a77b78a4f3b2998f1d2~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a656a8df64f84a16bd9f8d1c1a5f1d6b~tplv-goo7wpa0wc-image.image) </span>


2. Click “Create user group”, enter the user group name and other information, and click “Submit”. Click [Submit] to create a project\-level user group in the project and generate a user group ID (which uniquely identifies the user group).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8fbb1c0abff4888899e727d6030f794~tplv-goo7wpa0wc-image.image) </span>


3. After the user group is created successfully, click “Authorize now” to grant permissions to the user group.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53692af69e5e44209c1b51b0ae15c153~tplv-goo7wpa0wc-image.image) </span>


4. To add users to a user group, you can select from existing users or create new users. Three methods are supported: create by username, create by phone number, and invite via Ocean Engine.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01630283b9054eba9511c0ad1cf89047~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/931da395012c406383e9d51cdca192dc~tplv-goo7wpa0wc-image.image) </span>


5. To set permissions for the user group, click “Add permission” to configure the relevant settings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/677c26c79c6343319f8d97e64cc48a65~tplv-goo7wpa0wc-image.image) </span>

<span id="ab95961f"></span>
## 2.2 Edit a user group


1. Move the mouse over the user group name in the user group list, then move to the option icon after the user group name, and select “Edit”.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ae313a62cd74b959743e16b974682a8~tplv-goo7wpa0wc-image.image) </span>


2. An Edit User Group pop\-up window will appear, where you can make modifications.


<span id="fdd2989d"></span>
## 2.3 Add users to a user group

There are two ways to add users to a user group:


* You can add users manually.

* Alternatively, members from other user groups can be added to the current user group.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c483d7e30a44008b1c70f15c0e9966c~tplv-goo7wpa0wc-image.image) </span>

<span id="88c7a2ea"></span>
## 2.4 Associate user groups from other projects with this project

The user group association feature allows you to add existing system user groups to the current project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5638ef061204747a74c9817d565636e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
# 3. Feature introduction

<span id="_2-3-用户组编辑"></span>
## 3.1 User group categories

User groups are divided into system\-level and project\-level.


* System\-level user group: user group associated with the system level

* Project\-level user group: A user group customized within a specific project.


You can view the details of the user groups a user belongs to on the user management page. The user's groups include the system\-level and project\-level user groups they have joined.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ea0133c1cef4473880a15081883e01a~tplv-goo7wpa0wc-image.image) </span>

Each user can belong to multiple system\-level and project\-level user groups; **project\-level user groups can add members, while system\-level user groups cannot be modified.** 

<span id="aa17f866"></span>
## 3.2 User group authorization

Resources within a project support authorization for system\-level and project\-level user groups. After authorization, all users in the user group will have permissions for the resource.

On the user group details page, click "Permission management", search for resources, and authorize them. You can authorize permissions for projects and datasets.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e70e9c72e32643358d28c6a70e0df83c~tplv-goo7wpa0wc-image.image) </span>

<span id="cde36634"></span>
## 3.3 Batch deletion

The member management page of the user group supports selecting members for batch deletion.
