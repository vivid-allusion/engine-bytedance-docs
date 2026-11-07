---
title: "Role management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/role-management"
---

ByteHouse supports customizing roles, authorizing roles, and assigning roles to users. This document introduces how to create roles as well as how to manage roles and user privileges.

<span id="eb78d783"></span>
# Background

ByteHouse by default has created four roles: Query User, Data Engineer, Cluster Admin, System Admin. Privileges differ among roles, and the pages that can be viewed on the console also vary. For details on role definition and privileges, refer to [Default roles and custom roles](https://docs.byteplus.com/docs/bytehouse/privilege-model#f9f33e4c).

<span id="默认角色说明"></span>
# View role

Log in to ByteHouse Console, click on the **Access control** tab at the top, and click on **Role** in the left navigation bar to view the list of roles.

Below are the details of some role parameters shown in the list:


|Parameter item |Parameter description |
|---|---|
|Role name |The character name is unique within the cluster. Click on the **role name** to view the role details. |
|Cluster |The cluster and scope of roles. Granted upon role creation and cannot be modified thereafter. |
|Role type |* Default: Indicates that the role is created by the system by default. For details on the default roles, refer to<br><br>* Custom: Refers to user\-created custom roles. |
|Authorized users |This role has been authorized for user access. Hover the mouse over the display information to view the authorized usernames. |


<span id="新建角色"></span>
# Create new role


1. Log in to ByteHouse Console, click on the **Access control** tab at the top, click on **Roles** in the left navigation bar, then click on **Create new role**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b12a196a24a74a49a33c5de44fc425d6~tplv-goo7wpa0wc-image.image) </span>

2. Enter or select the following information in the popup window:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cd261a0c1c54c04bfc8372c9460d769~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Parameter description |
   |---|---|
   |Privilege scope |Select a cluster applicable to the role. |
   |Role name |Customize the role name. Role names within the same cluster cannot be repeated. Naming rules are as follows:<br><br><br>* Supports a combination of strings or numbers, including an underline.<br><br>* Supports up to 128 characters. |
   |Description |You can customize the role description for easier management and use in the future. |
   

3. Click **OK**. After the role is created, follow the system prompts to grant [Row privilege](https://docs.byteplus.com/docs/bytehouse/row-privilege) for the role.


<span id="角色详情"></span>
# Manage database and table privileges for roles

<span id="24c12606"></span>
## Caution

ByteHouse's default roles cannot grant additional privileges. If a user is a Query User but you want to grant additional privileges, you can assign other roles to the user, and the privileges of the roles will accumulate.

<span id="4b5502e1"></span>
## Grant privileges


1. In the **Role list**, click on **Role name** to enter the role details page.

2. Click on the **Database & Table Permissions** tab, then click**Grant privileges**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59dcf5c313a144eca10448c3e93fc508~tplv-goo7wpa0wc-image.image) </span>

3. In the popup window, select the type of assignment and choose the corresponding data resources. If you need to add multiple data resources, click **Add**. For details on privilege specifications, please refer to [Description of grantable database and table privileges](https://docs.byteplus.com/docs/bytehouse/privilege-model#e75a2c67).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When a user has any other privileges for a specific database table, they will be automatically granted SHOW privilege.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1eccd24d11b04e1d8566eb9116c3fe82~tplv-goo7wpa0wc-image.image) </span>

4. After the authorization information is complete, click **Confirm**.


<span id="f2dcb1e1"></span>
## Revoke privileges


1. In the **Role list**, click **role name** to enter the role details page.

2. Click on the **Database & Table Permissions** tab, then click **Revoke privileges**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d37e7e9bc69b42ae89a30797236b41da~tplv-goo7wpa0wc-image.image) </span>

3. In the popup window, select the data type to be revoked and choose the corresponding data resources. If multiple data resources need to be revoked, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4e819bf8d0a404b9c71908cad312edd~tplv-goo7wpa0wc-image.image) </span>

4. Once the revocation authorization information is complete, click **Confirm**.


<span id="2cf30140"></span>
## Regrant previously revoked privileges

If you have granted a role privilege for the entire database and then revoked single table privileges, ByteHouse will display the revoked table privileges in the database table privileges interface. You can click the **Delete** button of the row where the table is located to regrant the revoked table privileges.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96ee79d2e9404fd48ed795fb98d90ebe~tplv-goo7wpa0wc-image.image) </span>

<span id="240df71d"></span>
# Manage user's role privileges

<span id="32c541f5"></span>
## Caution

Please note that authorization can only be granted to sub\-users and cannot be granted to system users or main users.

<span id="f6352f8a"></span>
## Grant privileges

Users can be granted role privileges in two ways:

<span id="c67ba8e0"></span>
### Option 1: Grant via the role interface


1. In the **Role list**, click the **role name** to enter the role details page.

2. Click on the **Authorized Users** tab, then click **Grant** **to users**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7349999b8f31411ea7e9495056a83b35~tplv-goo7wpa0wc-image.image) </span>

3. In the popup window, select the users to be authorized and adjust the Admin Option settings. The Admin Option privilege determines whether a user can grant the privileges they have been granted to other users.

   To grant role privileges to multiple users simultaneously, click **Add** and continue adding users.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2359de47f5d24a9f83c7ccac71c88d7a~tplv-goo7wpa0wc-image.image) </span>

4. Click **Confirm** to complete the authorization.


<span id="0b808d05"></span>
### Option 2: Grant via the user interface


1. On the **Access control** page, click the **User** tab in the sidebar to view the user list, click on the **User name to be authorized** to enter the user's privilege details page.

2. In the **Grant roles** module, click **Edit**.

3. Select the scope of privileges, roles, and adjust the Admin Option settings. Admin Option privileges refer to whether users are allowed to delegate their granted privileges to other users.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4830afe4dc2b435c9d1a3e7584260d61~tplv-goo7wpa0wc-image.image) </span>

4. Click **Submit**.


<span id="9b86f2bc"></span>
## Revoke privileges


1. On the **Access control** page, click the **Role** tab on the sidebar, then click a **role name** to enter the role details interface.

2. In the list of **Authorized Users**, click the **Revoke privileges** button in the Action column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/212366950ba2450d8540cdc8b2021673~tplv-goo7wpa0wc-image.image) </span>

3. Click **Revoke** to revoke the current user's role authorization.


<span id="3fdad43e"></span>
# Delete role

<span id="c19d3a01"></span>
## Usage restrictions


* Roles already assigned to users cannot be deleted. Please revoke the roles from authorized users first. Refer to [Revoke privileges](https://docs.byteplus.com/docs/bytehouse/role-management#f2dcb1e1) for details.

* Roles created by default in ByteHouse cannot be deleted.


<span id="678ee9c6"></span>
## **Steps**


1. In the role list, click the **Delete** button in the Action column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34b0ad0d15b14ee3a8b67e6f42009b5e~tplv-goo7wpa0wc-image.image) </span>

2. Click **OK** to delete the current role.
