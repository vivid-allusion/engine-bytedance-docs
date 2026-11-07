---
title: "Stored procedure management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/stored-procedure-management-for-mysql"
---

This topic describes how to visually create, edit, and delete stored procedures on the DBW data interaction platform, implementing data lifecycle management of databases.

<span id="prerequisites"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must be granted the required permissions, for example, for querying and modifying the specified database.</div>


<span id="precautions"></span>
## Precautions


* We recommend that you do not create, delete, or edit stored procedures in the system database.

* The SQL statement in **Stored procedure definition** cannot contain the `return` keyword.

* No custom separators are required in **Stored procedure definition**.

* The output parameters of a stored procedure cannot be the same as table field names.

* No default parameter values are specified in the stored procedures of RDS for MySQL. Therefore, when calling a RDS for MySQL stored procedure, make sure that all parameters are specified and some can be set to **NULL**. For example, when you create the stored procedure `p(in a int, out b int)`, where `a` and `b` are parameters, you can run the `call p(1,@b)` command to call the stored procedure.

* Deletion of stored procedures is irreversible. Proceed with caution.

* Actions such as creating or deleting objects may impact online business performance. It is recommended to perform these during off\-peak hours.


<span id="creating-a-stored-procedure"></span>
## Create a stored procedure


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Stored procedure**, right\-click the target view, and select **Create stored procedure**.

3. On the **Create stored procedure@{datebase name}**  tab, set the following parameters.

   
   |Parameter |**Description** |
   |---|---|
   |**Name** |Specify a custom name for the stored procedure according to the following naming rules:<br><br><br>* The stored procedure name must be unique in the database.<br><br>* The name must be 1 to 64 characters in length, and cannot be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* The name can consist of lowercase letters, digits, underscores (_), or hyphens (\-). |
   |**Input parameter** |Optional. Click **Add field** and set the input parameters. |
   |**Output parameter** |Optional. Click **Add field** and set the output parameters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The output parameters cannot be the same as the table field names.</div><br> |
   |**Security** |Specify the security context of the stored procedure. Valid values:<br><br><br>* **Default**: When you select this option, the security context is **DEFINER** by default.<br><br>* **DEFINER**: The stored procedure is executed with the permissions of the user specified by the DEFINER. When you select **DEFINER**, the user specified by the DEFINER must exist in the database and have the required permissions. Otherwise, the execution will fail.<br><br>* **INVOKER**: The stored procedure is executed with the permissions of the user invoke this view. When you select **INVOKER**, the execution can succeed provided that the executor has permission to execute it. |
   |**Data access** |Select a data access method for the stored procedure. Valid values:<br><br><br>* **Default**: When you select **Default**, the data access method is **ContainsSQL ** by default.<br><br>* **NoSQL**: The subroutine contains no SQL statements.<br><br>* **ContainsSQL**: The subroutine does not contain statements that read or write data.<br><br>* **ReadsSQLData**: The subroutine contains statements that read data, but not statements that write data.<br><br>* **ModifiesSQLData**: The subroutine contains statements that write data. |
   |**Comment** |Optional. Describe the stored procedure to help identify it. |
   

4. Click **Next step**.

5. On the **Stored procedure definition** tab, configure a command statement and click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The SQL statement in <strong>Stored procedure definition</strong> cannot contain the <code>return</code> keyword.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">No custom separators are required in <strong>Stored procedure definition</strong>.   </div>
   

6. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="executing-a-stored-procedure"></span>
## Execute a stored procedure


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Stored procedure**, right\-click the target view, and select **Execute stored procedure**.

4. In the **Execute stored procedure** dialog box, specify **Parameter value** and click **Execute**.

5. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.

   After the execution is completed, in the **Execute stored procedure** dialog box, you can go to the **Execution result** area and click **View result** to view the execution results.


<span id="editing-a-stored-procedure"></span>
## Edit a stored procedure


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Stored procedure**, right\-click the target view, and select **Edit stored procedure**.

4. On the **Edit stored procedure@{database name}**  tab, go to the **Stored procedure definition** area and edit the statement of the stored procedure.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The SQL statement in <strong>Stored procedure definition</strong> cannot contain the <code>return</code> keyword.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">No custom separators are required in <strong>Stored procedure definition</strong>.   </div>
   

5. Click **Submit**.

6. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="deleting-a-stored-procedure"></span>
## Delete a stored procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deletion of stored procedures is irreversible. Proceed with caution.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Stored procedure**, right\-click the target view, and select **Delete stored procedure**.

4. In the **Delete stored procedure** dialog box, make sure that the statement is correct and click **Execute**.


<span id="relevant-apis"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel the execution of an SQL command. |
