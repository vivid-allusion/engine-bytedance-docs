---
title: "Component permission management: users and roles"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/si_component_permission_management"
---

Through the user management page provided by the control console, you can efficiently manage StarRocks and Doris engine\-related resources with fine\-grained control.

<span id="414ee35d"></span>
# Users and roles note

<span id="6f8f5c8d"></span>
## Permission management design

The permission control system for engines within the EMR Serverless instance (OLAP) product is designed based on role\-based access control (RBAC). Permissions are indirectly granted to users by associating users with roles and roles with permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0451f133f3714311b903e8c0445e36a7~tplv-goo7wpa0wc-image.image) </span>

For example, after the administrator (usually the primary account) purchases the EMR Serverless instance (OLAP) product, they can create internal EMR users and roles for different data development teams based on the actual situation of the business team, and authorize roles to achieve engine permission control.

EMR provides you with default roles and users. You can also create custom users and roles as needed. After associating users with roles, you can control permissions by configuring the engine permission details for the roles.

<span id="f3c52244"></span>
## Default roles

The system default roles are as follows:


|Engine |Role |Note |
|---|---|---|
|StarRocks |db_admin |System administrator responsible for database management tasks, such as creating and modifying database objects. |
||user_admin |User administrator responsible for user account management tasks, such as creating and modifying users, as well as creating, granting, revoking, and deleting roles. |
||public |Global role. All users are assigned to this role by default, and no separate authorization is required.<br><br>Provides only basic permissions to ensure users can access public resources in the system. |
|Doris |admin |This role has Admin_priv, which grants all permissions except node changes. |


<span id="24d8176b"></span>
## Default users

The system default users are as follows:


|Engine |User |Note |
|---|---|---|
|StarRocks |None |None |
|Doris |admin |The role is admin and has admin\-related permissions. |


<span id="b0dcbb1f"></span>
# Engine permission configuration

By creating custom roles, you can achieve more granular permission control to meet security requirements or complex scenarios such as dynamic permission adjustments. The role/user management operations in the control console are essentially the same for StarRocks and Doris instances. The following uses Doris as an example to demonstrate the general procedure for creating custom users and configuring permission control.

<span id="ee93bea0"></span>
## Step 1: Create a custom user


1. Log in and go to the EMR Serverless instance (OLAP) details page.

2. In the control console, click User management sidebar , select User in the upper left corner of the page, then click New user **in the upper right corner.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e23d995111540deb4f472b788aca12b~tplv-goo7wpa0wc-image.image) </span>

   * Set the username and password for the custom user according to the prompts on the interface.

   * You can also select the user role to associate with the current user here. If you have not yet created the corresponding user's role, you can skip setting it for now. After you create and configure the role later, grant the role's permissions to the user.


<span id="d2f47ba2"></span>
## Step 2: Create a custom role


1. Log in and go to the EMR Serverless instance (OLAP) details page.

2. In the console, click User managementsidebar, select Role in the upper left corner of the page, then click Create role **in the upper right corner.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f680cc54e2c42508fb11a8bafca4112~tplv-goo7wpa0wc-image.image) </span>


<span id="43a5b673"></span>
## Step 2: Configure the role permission scope


1. After the role is created, click the role name in the role list to enter the role details page.

2. On the role details page, click the "Granted permissions" tab and configure the permission scope for the current role according to actual permission control requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c213e9d0b8a34209a09037bfe2e5ad5d~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For details on the currently supported engine permission scopes, see:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">StarRocks：<a href="https://docs.byteplus.com/docs/E-MapReduce/109102#%E5%88%9B%E5%BB%BA%E8%A7%92%E8%89%B2">StarRocks 权限管控细则</a>   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Doris: <a href="https://doris.apache.org/zh-CN/docs/2.1/admin-manual/auth/authentication-and-authorization">Doris permission control details</a>   </div>
   


<span id="cb5220b6"></span>
## Step 3: Grant role permissions to users

After configuring the role permissions, you can click the "Granted users" tab on the role details page to add users to the current role.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eecdf7e431ab4c66a4f5f846696fa76d~tplv-goo7wpa0wc-image.image) </span>

Once added, the corresponding user will have engine operation permissions for the current role.
