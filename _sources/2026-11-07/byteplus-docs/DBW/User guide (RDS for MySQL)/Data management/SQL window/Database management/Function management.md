---
title: "Function management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/function-management-for-mysql"
---

This topic describes how to visually create, edit, and delete functions on the DBW data interaction platform, implementing data lifecycle management of databases.

<span id="prerequisites"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must be granted the required permissions, for example, for querying and modifying the specified database.</div>


<span id="precautions"></span>
## Precautions


* We recommend that you do not create, delete, or edit functions in the system database.

* Custom functions can only be used in the database connected to the current client.

* No custom separators are required in **Function definition**.

* Functions must have return values. Therefore, functions must not contain the `select` command, except when you use the `select into` command to assign values to multiple variables.

* Function deletion is irreversible. Proceed with caution.

* Actions such as creating or deleting objects may impact online business performance. It is recommended to perform these during off\-peak hours.


<span id="creating-a-function"></span>
## Create a function


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Function**, right\-click the target view, and select **Create function**.

3. On the **Create function@{datebase name}**  tab, set the following parameters.

   
   |Parameter |**Description** |
   |---|---|
   |**Name** |Specify a custom function name according to the following naming rules:<br><br><br>* The function name must be unique in the database.<br><br>* The name must be 1 to 64 characters in length, and cannot be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* The name can consist of lowercase letters, digits, underscores (_), or hyphens (\-). |
   |**Input parameter** |Optional. Click **Input parameter** to set input parameters. |
   |**Return type** |From the drop\-down list, select the type of the return parameter. |
   |**Return length** |Set the length of the return parameter. This parameter is unavailable for some types. |
   |**Security** |Specify the security context of the function. Valid values:<br><br><br>* **Default**: When you select this option, the security context is **DEFINER** by default.<br><br>* **DEFINER**: The stored procedure is executed with the permissions of the user specified by the DEFINER. When you select **DEFINER**, the user specified by the DEFINER must exist in the database and have the required permissions. Otherwise, the execution will fail.<br><br>* **INVOKER**: The function is executed by a user who has permission to call this function. When you select **INVOKER**, the execution can succeed provided that the executor has permission to execute it. |
   |**Data access** |Select a data access method for the function. Valid values:<br><br><br>* **Default**: When you select **Default**, the data access method is **CONTAINS SQL** by default.<br><br>* **NO** **SQL**: The subroutine contains no SQL statements.<br><br>* **CONTAINS** **SQL**: The subroutine does not contain statements that read or write data.<br><br>* **READS** **SQL** **DATA**: The subroutine contains statements that read data, but not statements that write data.<br><br>* **MODIFIES** **SQL** **DATA**: The subroutine contains statements that write data. |
   |**Comment** |Optional. Describe the function to help identify it. |
   

4. Click **Next step**.

5. On the **Create function@{datebase name}**  tab, go to the **Function definition** area, set a statement to execute the function, and click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">No custom separators are required in <strong>Function definition</strong>.   </div>
   

6. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="executing-a-function"></span>
## Execute a function


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Function**, right\-click the target view, and select **Execute function**.

4. In the **Execution function** dialog box, set **Parameter value** and click **Execute**.

5. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.

   After the execution is completed, in the **Execution function** dialog box, you can go to the **Execution result** area and click **View result** to view the execution results.


<span id="editing-a-function"></span>
## Edit a function


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Function**, right\-click the target view, and select **Edit function**.

4. On the **Edit function@{database name}**  tab, go to the **Function definition** area and edit the function statement.

5. Click **Submit**.

6. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="deleting-a-function"></span>
## Delete a function

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Function deletion is irreversible. Proceed with caution.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Function**, right\-click the target view, and select **Delete function**.

4. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="relevant-apis"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel the execution of an SQL command. |
