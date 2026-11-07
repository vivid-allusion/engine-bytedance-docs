---
title: "Manage database user"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/manage-database-account"
---

ByteHouse separates IAM users and database users, allows independent creation of database users, and grants resource and data privileges to these accounts. You can access the ByteHouse database through CLI, BI Tools, ELT Tools, IDE Tools, API, and others. This document explains how to create and use database users.

<span id="e0ddfb21"></span>
# **Prerequisites**

Only the main account or the sub\-account with the SystemAdmin or AccountAdmin role and the privilege to access the ByteHouse console can manage database users.

<span id="8dd43d89"></span>
# Cautions

Database users are sub\-users and cannot access the BytePlus Console. They are only granted the maximum USE privilege for virtual warehouse resources, and granting ALL privilege will not activate.

<span id="2434d04c"></span>
# Create database user


1. Log in to the ByteHouse Console, in the **Access Control** \> **User** page, click **Create User \> Create Database User**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f821876ccdbc49a0ae45bb2fc502651d~tplv-goo7wpa0wc-image.image) </span>

2. On the Create Database User page, configure the user information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8754780c7794958955b56fd3b7bb5d3~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration Description |
   |---|---|
   |Username |Fill in a custom username, with the following naming rules:<br><br><br>* Supports Chinese and English letters, digits, strikethrough "\-" and underline "_";<br><br>* A maximum of 64 characters can be set.<br><br>* Usernames must not be repeated. |
   |Password |The password for the database user connection must be customized by the user, with the following naming rules:<br><br><br>* The length must be between 8 and 30 characters.<br><br>* Passwords must not start with "/" or "$6$".<br><br>* Must include uppercase letters A–Z.<br><br>* Must include lowercase letters a–z. |
   |Parameter Settings |Configure the default virtual warehouse and default write virtual warehouse for the user. After assigning a virtual warehouse to users, the system will also grant USE privileges of that virtual warehouse to the user. Subsequent modifications can be made in the **Access control \> Resource privileges** module, as detailed in [Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management).<br><br><br>* Default virtual warehouse: The default virtual warehouse for the current user, used default virtual warehouse to process SQL.<br><br>* Write virtual warehouse: The default virtual warehouse for writing in the current environment, used as the default virtual warehouse for writing data into the underlying database storage. If the default write virtual warehouse is configured in the current environment, the system will automatically use this group. You do not need to configure it, as the user's default write virtual warehouse will automatically update to follow the environment’s default group. If no default write virtual warehouse has been configured in the current environment, please first visit \*\*\*\* the **Tenant management** \> **Parameter setting** page to configure it, as detailed in [Set the default write virtual warehouse](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters#e4ec3478). |
   |Description |Add a detailed description to the user, supporting up to 200 characters. |
   

3. After configuring the user information, click **create**. Once created, you can view user\-related information in the user list.


<span id="859d6d8d"></span>
# Assign user privileges

<span id="a777e5b2"></span>
## Step 1: Grant environmental privileges to the database user


1. Log in to the ByteHouse Console, on the **Access control** \> **User** page, click to authorize the environment.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66888565bf2f4062a7eb6cd8cc661be0~tplv-goo7wpa0wc-image.image) </span>

2. Select the current environment from the environment list, and click **User assignment**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68ae1f5c0b764f82aea2be79480d7784~tplv-goo7wpa0wc-image.image) </span>

3. On the User assignment page, search by username to grant the user environment usage rights.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc1af7f2d9bb4ac899e41c0b61cb9a02~tplv-goo7wpa0wc-image.image) </span>

4. Click **OK** to complete the environment authorization.


<span id="bc626d32"></span>
## Step 2: Grant resource and data privileges to the database user

You can grant resources and data privileges to the user through **assigning roles** and **direct authorization** methods.

<span id="86d140f7"></span>
### Prerequisites

If you need to grant privileges to a user by assigning roles, please first create the roles and prepare the roles to be granted to the user.

In the ByteHouse Console, navigate through **Access Control \> Roles** path, click on **Create role**. For details, refer to [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration).

<span id="f6085d9b"></span>
### Steps


1. Log in to the ByteHouse Console, on the **Access Control** \> **User** page, click on the user name to access the user authorization page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fd4d041bab34662ac4e3ac7459521d4~tplv-goo7wpa0wc-image.image) </span>

2. You can grant resource and data privileges to users either **by assigning roles** or **by direct authorization** as required.

   
   |Authorization Method |Steps |
   |---|---|
   |Grant Roles |1. On the **User Details** Page, switch to the **Granted roles** tab and click **Grant roles.** <br><br>2. In the role granting page, select the roles to be granted to the user.<br><br>3. Click **Confirm** to complete the authorization. |
   |Authorize directly |1. In the **Resource privileges** or **Data Privileges** page, switch to the **Directly granted** tab and click **Directly granted.** <br><br>2. On the privilege management page, assign the appropriate virtual warehouse resource privileges or data privileges to the user.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can grant the database user the default virtual warehouse and default write virtual warehouse USE and VIEW privileges; it is suggested to configure default virtual warehouse and default write virtual warehouse USE privileges for the user. If only the VIEW privilege is granted, the user will not be able to execute SQL queries after connecting to ByteHouse.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the user is used to access/read and write to databases in the future, grant the necessary data privileges to the user as needed.</div><br><br><br>3. Click **OK** to complete the authorization. |
   

   After completing the user authorization, you can view the details of the privileges granted to the user under the **Resources privileges** and **Data privileges** tabs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72f8b375972d4fffba622714c9793a8c~tplv-goo7wpa0wc-image.image) </span>

   You can view the roles granted authorization to the user in the **Granted Roles** tab. You can revoke a role's privilege from the user using the **Revoke**button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cb6108618974f519dc4e61fc1345ec8~tplv-goo7wpa0wc-image.image) </span>


<span id="b35a0886"></span>
# Edit database user

After creating the database user, you can reset the password and adjust the user settings.

<span id="a6a3e043"></span>
## Reset password

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Resetting the password may cause interruptions in connections using this user, please proceed with caution.</div>



1. In the user list, click the **Reset Password** button in the action column corresponding to the username.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/978ee6428cc64bab85f23badf4cb4928~tplv-goo7wpa0wc-image.image) </span>

2. In the sidebar popup, enter and confirm the new password.

3. Click **Confirm Reset** to complete the password reset.


<span id="0cf4ad6a"></span>
## Adjust user parameter settings


1. In the user list, click the **Parameter setting** button in the operation column corresponding to the username.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40d9d062d1b940cbab2636f0bbdb667b~tplv-goo7wpa0wc-image.image) </span>

2. In the popup window, select the default virtual warehouse.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/def4941794684321b5793410a82ba758~tplv-goo7wpa0wc-image.image) </span>

3. Click **Confirm Change** to complete the parameter settings.


<span id="9571630a"></span>
# Delete database user


1. In the user list, click the **Delete** button in the operation column corresponding to the username.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5df94f74011d424386ec458f8e29b07c~tplv-goo7wpa0wc-image.image) </span>

2. In the popup window, input the user name to be deleted.

3. Click **Confirm Delete**.


<span id="6eaf400c"></span>
# Next steps: Connect to ByteHouse using a database user

You can connect to the ByteHouse database through CLI, BI tools, ELT tools, IDE tools, API, and others using the database user and API Key. For operation details, please refer to the following documents:


|Connection Methods |Operation Document |
|---|---|
|CLI |[ByteHouse CLI](https://docs.byteplus.com/docs/bytehouse/docs-gateway-client) |
|BI Tools |[BI Tools Connect to ByteHouse](https://docs.byteplus.com/en/docs/bytehouse/docs-bi) |
|ELT Tools |[ELT Tools Connect to ByteHouse](https://docs.byteplus.com/en/docs/bytehouse/docs-elt-and-orchestration) |
|IDE Tools |[IDE Tools Connect to ByteHouse](https://docs.byteplus.com/en/docs/bytehouse/docs-ide-and-db-admin) |
|API Access |[Usage Example](https://docs.byteplus.com/docs/bytehouse/calling-method#6b230cc5) |
