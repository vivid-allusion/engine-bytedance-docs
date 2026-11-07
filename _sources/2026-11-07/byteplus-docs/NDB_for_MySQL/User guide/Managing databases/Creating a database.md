---
title: "Creating a database"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_database"
---

To use NDB for MySQL, you need to create a database in your instance. This article describes how to create a database for an instance.

<span id="前提条件"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id="操作步骤"></span>
## Procedure


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


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[CreateDatabase](https://www.byteplus.com/en/docs/NDB_for_MySQL/CreateDatabase) |Call the CreateDatabase to create the database. |
|[DescribeDatabases](https://www.byteplus.com/en/docs/NDB_for_MySQL/DescribeDatabases) |Call the DescribeDatabases to query the database list. |
