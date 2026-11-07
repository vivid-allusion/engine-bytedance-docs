---
title: "Manage IAM user"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-user-management"
---

This tutorial mainly explains how to execute access control in ByteHouse, how BytePlus's main account can create new users, set user privileges, and configure access control strategies by assigning roles to users.

<span id="056f5fdc"></span>
# Prerequisite

The BytePlus main account is required to manage operations such as creating, editing, disabling, and authorizing IAM users.

<span id="102f13f4"></span>
# Cautions

After activating ByteHouse Cloud Data Warehouse, you can log in to the BytePlus Console with your main account. Based on business needs, you can create multiple sub\-users and grant them the minimum privileges required for different personnel.


* The main account has all operation privileges for all BytePlus products. In ByteHouse products, the main account is equivalent to the privilege of the **AccountAdmin** role in ByteHouse.

* To create sub\-users for ByteHouse, go to the access control page on the BytePlus console, create IAM users and grant them ByteHouse products\-related privilege policies. ByteHouse has presented two types of IAM privilege policies and also supports customizing your privilege policies.

   * **ByteHouseFullAccess**: Has all operation privileges for ByteHouse (excluding unsubscribing), equivalent to the privileges of the **SystemAdmin** role in ByteHouse.

   * **ByteHouseReadOnlyAccess**: Can access the ByteHouse console. Upon entering the ByteHouse console, you can view the computation group page but are unable to view databases, tables, or any data and resources. Users with such IAM privileges need to carry out fine\-grained privilege control through the ByteHouse console afterwards, granting **resource access** and **data privileges** to access specific database tables.

   * Custom privilege policy: You can create a custom policy based on your requirements to grant IAM users the privileges corresponding to the ByteHouse AccountAdmin or SystemAdmin role, with support for granular privilege definition.

* It is suggested that administrators maintain main accounts and subaccounts with ByteHouseFullAccess privileges and custom privilege policy, and subsequently, only the main account, sub\-accounts with ByteHouseFullAccess privilege, or other sub\-accounts assigned the AccountAdmin or SystemAdmin role can perform resource and data privilege management operations for users in the ByteHouse console.


<span id="652fb36b"></span>
# Prerequisites:

<span id="862777a5"></span>
## (Optional) Create custom privilege policies

You can create a custom policy on the BytePlus [Access control - Privilege policy](https://console.byteplus.com/iam/policymanage) page, and configure the detailed privileges of the policy by setting the policy Action.


1. Go to the BytePlus [Access control - Privilege policy](https://console.byteplus.com/iam/policymanage) page and click **Create Custom Policy**.

2. Enter a policy name and use the JSON editor to define the `Action` of the policy.

   You can refer to the following code example to configure Action as needed:

   ```JSON
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "bytehouse:AccountAdmin",
           "bytehouse:Read",
           "bytehouse:Update",
           "bytehouse:Delete",
           "bytehouse:Create"
         ],
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```
   

   **Parameter description**

   
   |Parameter |Configuration description |
   |---|---|
   |bytehouse:AccountAdmin |This parameter is used to assign a role to the user. Supported values: AccountAdmin, SystemAdmin, or `*`. `*` indicates the highest privilege (i.e., AccountAdmin). |
   |bytehouse:Read |This parameter controls whether the user has privileges to log in to the console. Configure this privilege if the user needs to access the console. |
   |bytehouse:Update |Use the current value; no additional configuration is required. |
   |bytehouse:Delete |Use the current value; no additional configuration is required. |
   |bytehouse:Create |Use the current value; no additional configuration is required. |
   


<span id="81ede19b"></span>
## Create IAM users

You can create new users on the BytePlus [Access Control-User](https://console.byteplus.com/iam/identitymanage/user) Page, set up console access privileges, and initialize passwords, as illustrated by the method "Create by Username".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36f3b87218434f62854ace0b604e03fb~tplv-goo7wpa0wc-image.image) </span>

In the second step's privilege settings page, the main account can associate corresponding IAM policies to the newly created users to add privileges, achieving fine\-grained access control.

For ByteHouse services, you can:


* Configure minimal privileges **ByteHouse read\-only access** for the created users\*\*.\*\* For details, refer to \*\*\*\* [ByteHouseReadOnlyAccess](https://console.byteplus.com/iam/policymanage/System/ByteHouseReadOnlyAccess).

* If you need to grant users **ByteHouse full management privileges**, then set it to [ByteHouseFullAccess](https://console.byteplus.com/iam/policymanage/System/ByteHouseFullAccess). Note that ByteHouseFullAccess is the maximum privilege for ByteHouse, users granted this privilege are equivalent to holding ByteHouse's **SystemAdmin** role privileges, it's advisable to use this with caution.

* Custom privilege policy: The privileges corresponding to this policy are determined by the role you assign when creating the policy.


<span id="0d0076bb"></span>
# Grant privileges

Typically, after an IAM user is created and the BytePlus main account has granted IAM privilege policies to the IAM user, for IAM users who only have the **ByteHouseReadOnlyAccess** privilege, the main account needs to go to the ByteHouse console to perform authorization operations for the user regarding detailed privileges on resources and data.

IAM users who already have the **ByteHouse SystemAdmin role** can also, after other IAM users with lower privileges are created, grant privileges to the corresponding users within ByteHouse.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When authorizing in the ByteHouse Console, it supports direct authorization to IAM users as well as creating User Roles, authorizing Roles, and then granting Role privileges to users. Here is a guide to directly authorizing IAM users. For operations that authorize through roles, refer to <a href="https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration">Role management</a>.</div>



1. After logging in and entering the ByteHouse console, on the "**Access Control \> Users**" Page, view the current user list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab396a6dcfb84cb795cc18bd01513512~tplv-goo7wpa0wc-image.image) </span>

2. Click on the username you want to manage to enter the User privilege Management Page.

3. On the "Resources privilege" and "Data privilege" tabs, we can grant corresponding privileges to users as needed.

   * Resources privileges

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9957f5cb890461bbded2cbbc052d605~tplv-goo7wpa0wc-image.image) </span>

   * Data privileges

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7aeae808f9e4e4caae69c2f96d60e83~tplv-goo7wpa0wc-image.image) </span>

   * Meanwhile, we can also grant a role to a user under the "Granted Roles" tab, thereby inheriting the role's privileges. For settings regarding roles, please refer to [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3100fac8fb37433a8b3e47077d208941~tplv-goo7wpa0wc-image.image) </span>

      The roles granted can be viewed in "Granted Roles", and the privileges of a certain role can be revoked by clicking the "Revoke" button.


<span id="8b178cd7"></span>
# Edit a user

<span id="0610dc94"></span>
## Adjust user parameter settings


1. In the user list, click the Parameter settings button in the Actions column corresponding to the username.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f61497afd0ba4c468332a1d74711196f~tplv-goo7wpa0wc-image.image) </span>

2. In the pop\-up window, select the default virtual warehouse.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef2aab123310468ba2e5155ca5b17734~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After assigning a user with a virtual warehouse USE privilege, you can modify the privilege in the resource management module. For details, refer to <a href="https://docs.byteplus.com/docs/bytehouse/resource-privilege-management">Resource privilege management</a>.   </div>
   

3. Click **Confiem Change** to complete the parameter settings.


<span id="b257e493"></span>
# Inactivate user

On the "Access Control \> Users" page, you can revoke all privileges of each user by clicking the "Inactivate" button on the right side of each user.

<span id="2ccb2a5f"></span>
# IAM user login

After assigning roles and relevant privileges to IAM users, they can log in to the account via the IAM login link provided on the console, switch to the corresponding role, and view and operate the resources, thereby achieving fine\-grained access control over data objects.

<span id="111a1d1c"></span>
# Related documents


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Best practices for access control](https://docs.byteplus.com/docs/bytehouse/best-practice-for-access-control)
