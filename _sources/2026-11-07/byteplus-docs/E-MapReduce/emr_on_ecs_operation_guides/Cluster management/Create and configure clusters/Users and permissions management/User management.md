---
title: "User management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_user_management"
---

Users in Volcano Engine E\-MapReduce (EMR) clusters are divided into two categories: **regular users** and **system users**. Specifically:


* Regular users are those added to the cluster manually via import or creation operations in the user management module.

* System users are built\-in management users for each component, created during cluster initialization. Editing and deletion operations are not supported for system users.


The user management module provides operations for importing, creating, resetting passwords, and removing regular users, and also supports viewing the system user list. Additionally, group management for users is supported, allowing you to create, edit, and delete user groups. On the **Cluster details** page, click the **User management** tab in the navigation bar to access the cluster user management interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">EMR uses the OpenLDAP component internally to manage user and user group data within the cluster.</div>


<span id="_1-用户管理"></span>
## 1 User management

The user management page displays the list of imported and created regular users by default. The Admin user is the default user created when the cluster is created and is automatically added to all component permission groups. The password for this user can be found in the /root/.emr/secret file on the Master node after the cluster is created.

<span id="_1-1-导入-iam-用户"></span>
### 1.1 **Import IAM users**

You can use the user management module to import IAM users (including primary and sub\-accounts) into the cluster, enabling these users to use EMR cluster components. Procedure:


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. In the left navigation bar of the console, click **Resource management \> on ECS \> Cluster name** to enter the cluster overview.

3. In the left navigation bar, click **User management** to enter the user management page.

4. Click the **Add user \> Import IAM user** button in the upper right corner of the interface.

5. In the pop\-up window, select the IAM user list to import from the dropdown and complete the user information (see the table below).

   
   |Field |Required |Default value |Note |
   |---|---|---|---|
   |IAM user |Yes |None |The IAM user name(s) to import. You can select and import multiple users at once and search by keyword. |
   |Password |Yes |None |The password must be 8 to 20 characters long, may contain numbers, letters, '\-' and '_', and must include at least one number and one letter. |
   |Confirm password |Yes |None |Must match the password entered the first time. |
   |User group |No |None |Use the dropdown to select the user groups associated with the IAM users being imported. You can associate zero or more user groups and search by keyword. |
   |Note |No |None |Note details |
   

6. Click the **Confirm** button to submit the import request.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When importing multiple IAM users at once, the password you set will apply to all users, meaning all users in this batch will use the same password.</div>


* <div data-tips="true" data-tips-type="tip">If the primary account contains Chinese characters, the account will be stored using the corresponding Pinyin after import. Users must use the Pinyin account when operating components.</div>


* <div data-tips="true" data-tips-type="tip">If a sub\-account contains Chinese characters, import is not allowed.</div>


* <div data-tips="true" data-tips-type="tip">For system users (you can view them in the <strong>system users</strong> section), if there is an IAM account with the same name, import is not allowed. These accounts are built\-in and can be used directly.</div>


* <div data-tips="true" data-tips-type="tip">You can view the details and failure reasons for this operation on the <strong>operation log</strong> page.</div>



<span id="_1-2-手动添加用户"></span>
### 1.2 **Add users manually**

You can use the user management module to create and add custom users to the cluster, enabling these users to use EMR cluster components. Procedure:


1. On the **User management** page, click the **Add user \> Manual add** button in the upper right corner.

2. Enter the user information in the pop\-up dialog as prompted.

   
   |Field |Required |Default value |Note |
   |---|---|---|---|
   |User |Yes |None |Custom user name.<br><br>The name must not exceed 64 characters and may only contain numbers, letters, underscores (_), hyphens (\-), and periods (.). It must start with a letter, number, or underscore. |
   |Password |Yes |None |The password must be between 8 and 20 characters in length, can contain numbers, letters, hyphens (\-), and underscores (_), and must contain at least one number and one letter. |
   |Confirm password |Yes |None |Must match the password entered the first time. |
   |User group |No |None |Use the dropdown to select the user groups associated with the IAM users being imported. You can associate zero or more user groups and search by keyword. |
   |Note |No |None |Note details |
   

3. Click the **Confirm** button to submit the request to add.


<span id="_1-3-重置密码"></span>
### 1.3 **Reset password**

You can reset the password for a specific imported or created user by clicking the **Action** column's **Reset password** button.

Resetting the password requires entering the original password for verification. If you forget the original password, please contact the primary account holder to reset the password.

<span id="_1-4-移除用户"></span>
### 1.4 **Remove user**

You can delete a specific imported or created user from the corresponding cluster by clicking the **Action** column's **Remove** button.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Removal is an irreversible operation. To remove an imported user, transfer the user's job and data permissions to another user in advance. If certain jobs and data are accessible only by that user, removing the user will prevent related jobs from being performed.</div>


<div data-tips="true" data-tips-type="warning"><strong>Please carefully assess the impact of removing users to ensure that your business is not adversely affected.</strong></div>


<span id="_2-用户组管理"></span>
## 2 User group management

EMR introduced support for user groups in version 1.3, allowing you to manage imported or created users in groups.

<span id="_2-1-添加用户组"></span>
### 2.1 Add a user group

You can customize and add user groups. Procedure:


1. On the **User management** page, click the **User group** button to enter the user group management interface.

2. Click the **Add user group** button in the upper right corner of the interface.

3. Enter the relevant user group information in the pop\-up dialog as prompted (see the table below).

   
   |Field |Required |Default value |Note |
   |---|---|---|---|
   |User group name |Yes |None |The user group name to be added may only contain numbers, letters, and _.\-, and must begin with a letter, number, or underscore. The maximum length of the name must not exceed 64 characters. |
   |Member |No |None |Select from the dropdown to associate imported or created users with the current user group. You may associate zero or more users and search by keyword. |
   |Description |No |None |Description |
   

4. Click the **Confirm** button to submit the request to add.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Custom user groups cannot be associated with system users.</div>


* <div data-tips="true" data-tips-type="tip">All system users are by default members of the admin user group. You cannot add a user group named admin or associate regular users with the admin user group.</div>



<span id="_2-2-编辑用户组"></span>
### 2.2 Edit a user group

For a created user group, you can edit its members and description by clicking the **Action** column's **Edit** button.

<span id="_2-3-删除用户组"></span>
### 2.3 Delete a user group

For an existing user group, you can delete it by clicking the **Action** column's **Delete** button.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deletion, the user group will become unavailable, and all users in the group will be automatically removed from the group.</div>
