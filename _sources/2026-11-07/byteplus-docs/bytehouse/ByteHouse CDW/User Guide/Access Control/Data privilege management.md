---
title: "Data privilege management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-permission"
---

This tutorial primarily explains how to set data privileges in ByteHouse. The scope of authorization includes global, database, table, view, materialized view, dictionary, external catalog, UDF, and more, while the authorized objects include roles and users.

<span id="b4ca9bfc"></span>
# Background information

Under the AccountAdmin role, you can click on the “Access Control \- Data Privileges” page in the top navigation bar to view all database tables of the account.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77da80794b834f6ab225c2e038f4faa8~tplv-goo7wpa0wc-image.image) </span>

<span id="834ef886"></span>
# Caution

Only the main account or the sub\-account with the SystemAdmin or AccountAdmin role and the privilege to access the ByteHouse console can perform data privilege management actions in the ByteHouse console.

<span id="bf1180a4"></span>
# Prerequisites


1. The logged\-in account is **Administrator role (AccountAdmin)** , or has management privileges for global, corresponding databases, tables, views, materialized views, dictionaries, external catalogs, or UDF.

2. Confirm that the **user/role** to be authorized exists. For details, refer to [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management) and [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration).


<span id="0802e002"></span>
# Manage privileges settings


1. (Optional) Select the data object on the left side of the data privilege tab.

2. Click the "Grant privilege" button at the top right corner, the system will display the "Grant data privilege" page. Select the type of data object to set, the specific data object, the privileges, and the roles or users. If the corresponding data object was selected in the first step, the tab will automatically select and fill some options.

   <div style="text-align: right">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e4fe17818004b54984dc62d0e432ba4~tplv-goo7wpa0wc-image.image" width="2930px" />   </div>
   

   Authorization details for different data types are as follows:

   
   |Data privileges |Privilege description |
   |---|---|
   |Global |Select the privileges to grant. After granting global privileges, all data objects in the environment will be granted the selected privileges. |
   |Database |Select the database to authorize, and grant database privileges. |
   |Table |Select the databases to be authorized and their subordinate tables, and grant privileges for tables. |
   |View |Select the databases to authorize and their subordinate views, and grant view privileges. |
   |Materialized view |Select the databases to be authorized and their subordinate materialized views, and grant privileges to the materialized views. |
   |Dictionary |Select the database and its subordinate dictionaries to be granted privileges, and grant privileges for the dictionaries. |
   |UDF |Select the UDF privileges that need to be granted. |
   |External catalog |Select the external catalog that needs authorization, and grant the corresponding privileges. |
   

3. After confirming that privileges have been granted correctly, click **Confirm**.

4. After privileges are granted, you can view the authorizations you have received on the Data privileges page. You can click a data object to view the roles or users that have been granted access to the data object, as well as the privileges acquired by those roles or users.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5489c15cc5b4a1181579e632f7f1968~tplv-goo7wpa0wc-image.image) </span>


<span id="b4e48ccb"></span>
# Edit data privilege


1. Select the data object on the left side of the data privilege tab. The right panel will automatically display the users or roles that have been set for this data object, along with their corresponding privileges. Click the **Edit** button to enter the privilege settings page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ceb5e6926adf4fbfa8c8ceb8f07f6996~tplv-goo7wpa0wc-image.image) </span>

2. In the "Edit Data Privilege" tab, select the type of privilege and click confirm to save. If saved successfully, the system will prompt "Updated privileges successfully".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df944df5bd2547cfac93cc7336e05743~tplv-goo7wpa0wc-image.image) </span>


<span id="d54933b0"></span>
# Delete data privilege


1. Select the data object on the left side of the privilege tab. The page on the right will automatically display the users/roles assigned to the data object, along with the corresponding privileges. Click the delete button on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fc5fced2edf47dd9cb8aa6c932b602a~tplv-goo7wpa0wc-image.image) </span>

2. The system will prompt with a dialog for confirmation, click the "Delete" button to confirm the action. A system prompt "Revocation successful" message indicates that the operation is complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e9c8519daaf41deab5b5e353c0e61e6~tplv-goo7wpa0wc-image.image) </span>
