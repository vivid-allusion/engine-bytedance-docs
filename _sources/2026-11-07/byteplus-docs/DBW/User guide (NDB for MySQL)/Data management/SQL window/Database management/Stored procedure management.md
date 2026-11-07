---
title: "Stored procedure management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Stored_procedure_management"
---

This topic explains how to visually create, delete, and edit stored procedures in the data interaction platform of Database Workshop (DBW), enabling full lifecycle management of stored procedures.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you created must have corresponding permissions such as query and modification for the database.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* It is not recommended to create, edit, or delete stored procedures in system databases.

* SQL statements in **Stored procedure definition** cannot use the `return` keyword.

* **Stored procedure definition** do not require custom delimiters.

* The output parameters of a stored procedure cannot be the same as the field names of a table.

* Since NDB for MySQL stored procedures do not have default parameter values, parameters cannot be omitted when calling NDB for MySQL stored procedures. Use NULL as a substitute. For example, when creating a stored procedure as `p(in a int, out b int)`, its`a`,`b`are parameters. You can use the `call p(1,@b)` command to call the stored procedure.

* Once a stored procedure is deleted, it cannot be recovered. Proceed with caution.

* The creation, deletion, and other operations you perform may impact online business operations. It is recommended to carry out these operations during off\-peak business hours.


<span id=".5Yib5bu65a2Y5YKo6L-H56iL"></span>
## Create a stored procedure


1. Log on to the [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand **Stored procedure**, right\-click the target stored procedure, and select 2. In the visualization operation area of the **Data interaction platform** page, hover over **Stored procedure** and select  **...**  < **Create stored procedure**.

4. On the **Create stored procedure@{Database Name}**  tab, configure the following parameter information.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Name** |Custom name for the stored procedure. Naming Rules:<br><br><br>* The name must be unique within the database.<br><br>* Length must be between 1 and 64 characters and cannot be empty.<br><br>* Start with a letter and end with a letter or number.<br><br>* Consist of lowercase letters, numbers, underscores (_), or hyphens (\-). |
   |**Input parameter** |(Optional) Click **Add field** to configure input parameters. |
   |**Output parameter** |(Optional) Click **Add field** to configure output parameters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Output parameters cannot have the same name as table fields.</div><br> |
   |**Security** |Select the security type for the stored procedure, supporting the following types:<br><br><br>* **Default**: When default is selected, the default value for security is DEFINER.<br><br>* **DEFINER**: Executed with the privileges of the user specified by the definer (DEFINER). When selecting DEFINER, the user specified by DEFINER must exist in the database and have the corresponding operation permissions for successful execution.<br><br>* **INVOKER**: Executed with the permissions of the user who invokes this view. When selecting INVOKER, the executor only needs to have execution permissions for successful execution. |
   |**Data access** |Select the data access method for the stored procedure, supporting the following types:<br><br><br>* **Default**: When Default is selected, the default value for data access is ContainsSQL.<br><br>* **NoSQL**: Indicates that the subroutine does not contain SQL statements.<br><br>* **ContainsSQL**: Indicates that the subroutine does not contain statements for reading or writing data.<br><br>* **ReadsSQLData**: Indicates that the subroutine contains statements for reading data but not for writing data.<br><br>* **ModifiesSQLData**: Indicates that the subroutine contains statements for writing data. |
   |**Note** |(Optional) Remarks for the stored procedure to help you identify it. |
   

5. Click **Next**.

6. On the **Stored procedure definition** tab, configure the command statement and then click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The SQL statement in the <strong>Stored procedure definition</strong> cannot use the <code>return</code> keyword.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You do not need to customize a delimiter in the <strong>Stored procedure definition</strong>.   </div>
   

7. In the **Execute SQL** dialog box, confirm the execution statement and click **Execute**.


<span id=".5omn6KGM5a2Y5YKo6L-H56iL"></span>
## Execute stored procedure


1. Log on to the [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand **Stored procedure**, right\-click the target stored procedure, and select **Execute stored procedure**.

4. In the **Execute stored procedure** dialog box, configure the **parameter values**, then click **Execute**.

5. In the **Execute** **SQL** dialog box, confirm the execution statement and click **Execute**.

   After successful execution, you can click **View results** in the **Execution results** area of the **Execute stored procedure** dialog box to view the results of the stored procedure execution.


<span id=".57yW6L6R5a2Y5YKo6L-H56iL"></span>
## Edit Stored Procedure


1. Log on to [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand the **Stored procedure**, right\-click the target stored procedure, and select **Edit stored procedure**.

4. In the **Edit stored procedure @{Database Name}**  tab, edit the stored procedure statement as needed in the **Stored procedure definition** section.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Stored procedure definition</strong> cannot use the <code>return</code> keyword in SQL statements.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Stored procedure definition</strong> do not require custom delimiters.   </div>
   

5. Click **Submit**.

6. In **Execute SQL** dialog box, confirm the execution statement, then click **Execute**.


<span id=".5Yig6Zmk5a2Y5YKo6L-H56iL"></span>
## Delete stored procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once deleted, it cannot be recovered. Proceed with caution.</div>



1. Log on to [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand **Stored procedure**, right\-click the target stored procedure, and select **Delete stored procedure**.

4. In the **Delete stored procedure** dialog box, confirm the deletion statement and click **Execute**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute command statements. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to maintain the SQL session window. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to exit the SQL session window. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
