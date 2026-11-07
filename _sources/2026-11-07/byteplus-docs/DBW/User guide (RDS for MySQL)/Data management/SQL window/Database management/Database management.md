---
title: "Database management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/database-management-for-mysql1-for-mysql"
---

This topic describes how to visually create, edit, and delete databases on the DBW data interaction platform, implementing data lifecycle management of databases.

<span id="prerequisites"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must be granted the required permissions, for example, for querying and modifying the specified database.</div>


<span id="precautions"></span>
## Precautions


* Deleting or editing the system database is not supported.

* Actions such as creating or deleting objects may impact online business performance. It is recommended to perform these during off\-peak hours.

* It is not recommended to perform create, delete, or modify operations on tables, views, triggers, stored procedures, or other objects in system databases.


<span id="creating-a-database"></span>
## Create a database


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database.

3. Click **Create database**.

4. In the **Create database** dialog box, set the following parameters.

   
   |Parameter |**Description** |
   |---|---|
   |**Database name** |Specify a custom database name according to the following naming rules:<br><br><br>* The database name must be unique in the instance.<br><br>* The name must be 2 to 64 characters in length.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* The name can consist of lowercase letters, digits, underscores (_), or hyphens (\-).<br><br>* The database name must not contain [forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords). |
   |**Character set** |Select the desired character set from the dropdown list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">RDS for MySQL 5.7 supports <code>latin1</code>, <code>ascii</code>, <code>utf8</code>, and <code>utf8mb4</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">RDS for MySQL 8.0 supports<code>latin1</code>, <code>ascii</code>, <code>utf8mb3</code>, and <code>utf8mb4</code>.</div><br> |
   |**Sorting rules** |After you select a character set, a sorting rule is displayed by default. You can set the sorting rule as required. |
   

5. Click **OK**.


<span id="editing-a-database"></span>
## Edit a database

<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">Editing the system database is not supported.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database.

3. Click **Database management**.

4. On the **Database management** tab, find the target database and click **Edit** in the **Actions** column.

5. In the **Edit database** dialog box, edit **Character set** and **Sorting rules** of the database.

6. Click ** OK**.


<span id="deleting-a-database"></span>
## Delete a database

<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">Deleting the system database is not supported.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database.

3. Click **Database management**.

4. On the **Database management** tab, find the target database and click **Delete** in the **Actions** column.

5. In the confirmation input field within the **Confirm deletion** dialog box, enter the database name.

6. Click **OK**.


<span id="relevant-apis"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel the execution of an SQL command. |
