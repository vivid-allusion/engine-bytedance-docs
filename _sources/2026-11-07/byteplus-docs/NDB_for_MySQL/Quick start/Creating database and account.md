---
title: "Creating database and account"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account"
---

You can create relevant databases and accounts according to your business needs, and configure account permissions. This article describes how to create a database and account for an instance.

<span id="前提条件"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.volcengine.com/docs/6357/92773).

<span id="创建数据库"></span>
## Creating database


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Databases**.

5. On the **Databases** tab, click **Create database**, and in the dialog box that pops up, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Database name |Fill in the database name. This parameter is required, and the naming rules are as follows:<br><br><br>* The database name is unique under the current instance.<br><br>* The name length is limited to 2–32 characters. It starts with a letter and ends with a letter or a digit.<br><br>* Consists of letters, digits, underscores (_) and hyphens (\-).<br><br>* Database names cannot use certain reserved words, see [List of forbidden keywords](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_forbidden_keywords). |
   |Description |Fill in the description information of the database, with a length of 0 to 256 characters. It can contain numbers, Chinese characters, English characters, underscores (_) and hyphens (\-). |
   |Character set support |Character sets supported by the database. Can be set to `utf8`, `latin1`, `utf8mb4` or `ascii`. |
   |Authorized account |Grants permissions to the current database for the normal account. Currently supported permission types include: **Read/Write (DDL+DML)** , **Read\-only**, **DDL only**, **DML only**, **Custom permissions (multiple choices)** . For the specific SQL operation permissions included in each permission type, see the [Account permission list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description).<br><br><br>* **Setting permissions for a single account**<br><br>   1. Select the permission type from the drop\-down list in the **Permission** column of the target account.<br><br>      If you choose **Custom permissions**, you need to manually tick one or more SQL action permissions for them.<br><br>   2. When the selection is complete, click **OK** in the lower right corner of the drop\-down list.<br><br>* **Bulk setting permissions**<br><br>   1. Check multiple target account names and click **Bulk settings permissions**.<br><br>   2. Select the permission type in the drop\-down list.<br><br>      If you choose **Custom permissions**, you need to manually tick one or more SQL action permissions for them.<br><br>   3. When the selection is complete, click **OK** in the lower right corner of the drop\-down list.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Super account Default has all permissions for all databases without manual authorization.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is no suitable account for the time being, you can set the database permissions for the new account when creating the account.</div><br> |
   

6. After all account authorization settings are completed, click **OK** to complete the creation of the database.


<span id="创建账号"></span>
## Create account


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Accounts**.

5. On the **Accounts** tab, click **Create account**, and in the dialog box that pops up, set the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Database account |The name of the account. This parameter is required, and the naming rules are as follows:<br><br><br>* The account name is unique under the current instance.<br><br>* It starts with a letter and ends with a letter or a digit.<br><br>* It must consist of letters, numbers, underscores (_) and hyphens (\-). The name length is limited to 2–32 characters.<br><br>* Account names cannot use certain reserved words, see [List of forbidden keywords](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_forbidden_keywords). |
   |Account type |Type of database account, support the creation of the following two types of accounts, account permissions detailed description please refer to [Account permission description](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description).<br><br><br>* **Super account**: An instance can only create one super account, and has all the permissions of all databases under the instance, and can manage all normal accounts and databases.<br><br>* **Normal account**: An instance can create multiple normal accounts, and it is necessary to manually grant the permissions of a specific database to the normal account. |
   |Description |Fill in the description information of the account, with a length of 0 to 256 characters. It can contain numbers, Chinese characters, English characters, underscores (_) and hyphens (\-). |
   |Password |The password of the account. The password rules are as follows:<br><br><br>* The length is 8~32 characters.<br><br>* It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters are `~!@#$%^&*_-+=`\|\(){}[]:;'<>,.?/`. |
   |Confirm password |Enter the password again, it must be the same as the password entered in the previous step. |
   |Authorized database |* **Super account**: By default, it has all permissions for all databases under this instance, and no separate authorization is required.<br><br>* **Normal account**: You need to grant the specified permissions for the specified database for the normal account. When permissions are not set, this account does not have any permissions for any database. You can also modify the database authorized by the account after creation is complete. Currently supported permission types include: **Read/Write (DDL+DML)** , **Read\-only**, **DDL only**, **DML only**, **Custom permissions (multiple choices)** . For the specific SQL operation permissions included in each permission type, see the [Account permission list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description).<br><br>   * **Setting permissions for a single database**<br><br>      1. Reselect the permission type from the drop\-down list in the **Permission** column of the target database.<br><br>         If you choose **Custom permissions**, you need to manually tick one or more SQL action permissions for them.<br><br>      2. When the selection is complete, click **OK** in the lower right corner of the drop\-down list.<br><br>   * **Bulk setting permissions**<br><br>      1. Check multiple target database names and click **Bulk settings permissions**.<br><br>      2. Select the permission type in the drop\-down list.<br><br>         If you choose **Custom permissions**, you need to manually tick one or more SQL action permissions for them.<br><br>      3. When the selection is complete, click **OK** in the lower right corner of the drop\-down list. |
   

6. After all database authorization settings are completed, click **OK** to complete the creation of the account.
