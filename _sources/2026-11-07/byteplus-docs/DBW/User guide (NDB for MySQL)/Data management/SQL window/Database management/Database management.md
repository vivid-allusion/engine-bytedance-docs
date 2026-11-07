---
title: "Database management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/database-management"
---

This topic describes how to visually create, edit, and delete databases on the Database Workshop (DBW) console to manage the entire lifecycle of databases.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Deleting and editing system databases is not supported.

* It is not recommended to perform operations such as adding, deleting, or modifying tables, views, triggers, and stored procedures in the system database.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id=".5Yib5bu65pWw5o2u5bqT"></span>
## Create a database


1. Log on to the [data interaction platform for veDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. Click **Create database**.

4. In the Create database dialog box, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Database name** |Custom database name. Naming rules are as follows:<br><br><br>* The database name must be unique within the instance.<br><br>* The length is 2 to 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-).<br><br>* Database names[ can not be keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords). |
   |**Character set** |From the drop\-down list, select the character set.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">MySQL 5.7 supports <code>latin1</code>, <code>ascii</code>, <code>utf8</code>, and <code>utf8mb4</code> formats.</div><br><br><br>* <div data-tips="true" data-tips-type="default">MySQL 8.0 supports <code>latin1</code>, <code>ascii</code>, <code>utf8mb3</code>, and <code>utf8mb4</code> formats.</div><br> |
   |**Sorting rules** |After you select a character set, the default sorting rule is displayed. If you have other requirements, you can configure it as needed. |
   

5. Click **OK**.


<span id=".57yW6L6R5pWw5o2u5bqT"></span>
## Edit a database

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Editing system databases is not supported.</div>



1. Log on to the [data interaction platform for veDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. Click **Database management**.

4. On the **Database management** tab, click **Edit** in the **Actions** column of the target database.

5. In the **Edit database** dialog box, edit the database **Character set** and **Sorting rules**.

6. Click **OK**.


<span id=".5Yig6Zmk5pWw5o2u5bqT"></span>
## Delete a database

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deleting system databases is not supported.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. Click **Database management**.

4. On the **Database management** tab, click **Delete** in the **Actions** column of the target database.

5. In the **Confirm deletion** dialog box, enter the database name in the deletion confirmation input box.

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
