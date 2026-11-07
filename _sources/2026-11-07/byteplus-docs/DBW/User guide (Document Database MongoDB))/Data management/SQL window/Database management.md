---
title: "Database management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/database-management-for-mongodb"
---

This topic describes how to visually create, edit, and delete databases on the Database Workshop (DBW) console to manage the entire lifecycle of databases.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance for Document Database for MongoDB has been created and its `root` account password has been set. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Deleting and editing system databases is not supported.

* It is not recommended to perform operations such as adding, deleting, or modifying collections and indexes within the collection in the system database.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id=".5Yib5bu65pWw5o2u5bqT"></span>
## Create a database


1. Log on to the [data interaction platform for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb).

2. On the top menu bar of the **Data interaction platform** page, click the drop\-down icon next to the database.

3. Click **Create database**.

4. In the **Create database** dialog box, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Database name** |Custom database name. Naming rules are as follows:<br><br><br>* The database name must be unique within the instance.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* The length can not exceed 64 characters and can not be empty.<br><br>* It can only contain lowercase letters, numbers, underscores (_), or hyphens (\-). |
   |**Collection name** |Optional. Custom collection name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not set a collection name, <code>_default_</code> collection will be generated in this database by default.</div><br> |
   

5. Click **OK**.


<span id=".5Yig6Zmk5pWw5o2u5bqT"></span>
## Delete a database

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deleting system databases is not supported.</div>



1. Log on to the [data interaction platform for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-documentdb-for-mongodb).

2. On the top menu bar of the **Data interaction platform** page, click the drop\-down icon next to the database.

3. Click **Database management**.

4. On the **Database management** tab, click **Delete** in the **Actions** column of the target database.

5. In the **Confirm deletion** dialog box, enter the database name in the **Confirm deletion** input box.

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
