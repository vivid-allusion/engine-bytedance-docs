---
title: "Function management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Function_management"
---

This topic explains how to visually create, delete, and edit functions within the data interaction platform of Database Workshop (DBW) to manage the entire lifecycle of functions.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You must have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must have the necessary permissions, such as querying and modifying the corresponding database.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* It is recommended not to create, edit, or delete functions in the system database.

* Custom functions are only supported for use in the database associated with the current client.

* **Function definition** does not require custom delimiters.

* Since a function must have a return value, the `select` statement cannot be used inside the function, except when using the `select into` command to assign values to multiple field variables.

* Deleted functions cannot be restored; proceed with caution.

* The operations you perform, such as creating or deleting, may impact online business operations. It is recommended to carry out these actions during off\-peak business hours.


<span id=".5Yib5bu65Ye95pWw"></span>
## Create function


1. Log on to [the ](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand the **Function**, right\-click on the target function, and select **Create function**.

4. On the **Create function @{Database Name}**  tab, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Name** |Custom function name. Naming rules:<br><br><br>* The function name must be unique within the database.<br><br>* The length must be between 1 and 64 characters and cannot be empty.<br><br>* It must start with a letter and end with a letter or number.<br><br>* It can consist of lowercase letters, numbers, underscores (_), or hyphens (\-). |
   |**Input parameter** |(Optional) Click **Input parameter** to configure input parameters. |
   |**Return type** |Select the type of return parameter from the dropdown list. |
   |**Return length** |Set the length of the return parameter. Some types do not support setting this parameter. |
   |**Security** |Select the security of the function, supported formats include:<br><br><br>* **Default**: When selecting default, the default security value is DEFINER.<br><br>* **DEFINER**: Executed with the permissions of the user specified by the definer (DEFINER). When selecting DEFINER, the user specified by DEFINER must exist in the database and have the corresponding operation permissions for successful execution.<br><br>* **INVOKER**: Executed with the permissions of the user invoking the function. When selecting INVOKER, the executor only needs execution permissions for successful execution. |
   |**Data access** |Select the data access method for the function, supporting the following formats:<br><br><br>* **Default**: When selecting Default, the default value for data access is CONTAINS SQL.<br><br>* **NO** **SQL**: Indicates that the subroutine does not contain SQL statements.<br><br>* **CONTAINS** **SQL**: Indicates that the subroutine does not contain statements that read or write data.<br><br>* **READS** **SQL** **DATA**: Indicates that the subroutine contains statements that read data but does not contain statements that write data.<br><br>* **MODIFIES** **SQL** **DATA**: Indicates that the subroutine contains statements that write data. |
   |**Comment** |(Optional) Comment information for the function to help you identify it. |
   

5. Click **Next**.

6. On the **Create function @{Database Name}**  tab, set the function execution statement in the **Function definition** section, then click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You do not need to customize the delimiter in <strong>Function definition</strong>.   </div>
   

7. In **Execute** **SQL** dialog box, confirm the execution statement and click **Execute**.


<span id=".5omn6KGM5Ye95pWw"></span>
## Execute Function


1. Log on to the [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand **Function**, right\-click the target function, and select **Execute function**.

4. In the **Execute function** dialog box, configure the **Parameter value**, then click **Execute**.

5. In **Execute** **SQL** dialog box, confirm the execution statement, then click **Execute**.

   After successful execution, you can click **View results** in the **Execution results** section of the **Execute function** dialog box to view the function's execution results.


<span id=".57yW6L6R5Ye95pWw"></span>
## Edit Function


1. Log on to the [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand the ** Function**, right\-click on the target function, and select **Edit function**.

4. In the function definition area of the **Edit function @{Database Name}**  tab, edit the function statements as needed.

5. Click **Submit**.

6. In execution In the **SQL** dialog box, confirm the execution statement and click **Execute**.


<span id=".5Yig6Zmk5Ye95pWw"></span>
## Delete function

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deletion is irreversible, proceed with caution.</div>



1. Log on to [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand the **Function**, right\-click the target function, and select **Delete function**.

4. In ** Execute SQL** dialog box, confirm the execution statement, then click **Execute**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute command statements. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to keep the SQL session window active. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to exit the SQL session window. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
