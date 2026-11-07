---
title: "View management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/view-management-for-mysql"
---

This topic describes how to visually create, edit, and delete views on the DBW data interaction platform, implementing data lifecycle management of databases.

<span id="prerequisites"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must be granted the required permissions, for example, for querying and modifying the specified database.</div>


<span id="precautions"></span>
## Precautions


* Editing query results returned by a view query is not supported.

* We recommend that you do not create, delete, or edit views in the system database.

* View deletion is irreversible. Proceed with caution.

* Actions such as creating or deleting objects may impact online business performance. It is recommended to perform these during off\-peak hours.


<span id="creating-a-view"></span>
## Create a view


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **View**, right\-click the target view, and select **Create view**.

3. On the **Create view@{datebase name}**  page, configure the parameter information.

   1. Set the view parameters.

      
      |Parameter |**Description** |
      |---|---|
      |**Name** |Specify a custom view name according to the following naming rules:<br><br><br>* The view name must be unique in the database.<br><br>* The name must be 1 to 64 characters in length, and cannot be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* The name can consist of lowercase letters, digits, underscores (_), or hyphens (\-). |
      |**Definer** |Optional. Specify a definer, so that the statement is executed with the permissions of the definer. |
      |**Check options** |Select a check option. When you use the `WITH CHECK OPTION` clause to create a view, RDS for MySQL checks every updating row through the view. Valid values:<br><br><br>* **Default**: When you select this option, the check option is **CASCADED** by default.<br><br>* **LOCAL**: When you are managing the current view, the LOCAL check option is to recursively check the underlying views of the current view for check options. If a check option is found, the system checks the view data. If no check options are found, the system skips checking the view data.<br><br>* **CASCADED**: If a check option is found in the current view, the data you want to insert must meet the conditions of the current view and its underlying views. If no check options are found in the current view, you can insert data only when a check option is found in the underlying views of the current view and the conditions of the underlying views are met. |
      |**Algorithm** |Select a view processing algorithm. Valid values:<br><br><br>* **UNDEFINED**: RDS for MySQL automatically chooses an algorithm to use.<br><br>* **MERGE**: The text of a statement that refers to the view and the view definition are merged, so that parts of the view definition replace corresponding parts of the statement.<br><br>* **TEMPTABLE**: The results from the view are retrieved into a temporary table, which is then used to execute the statement. |
      |**Security** |Select a security context to specify whose permissions are used to execute the statement. Valid values:<br><br><br>* **Default**: When you select this option, the security context is **DEFINER** by default.<br><br>* **DEFINER**: The stored procedure is executed with the permissions of the user specified by the DEFINER. When you select **DEFINER**, the user specified by the DEFINER must exist in the database and have the required permissions. Otherwise, the execution will fail.<br><br>* **INVOKER**: The stored procedure is executed with the permissions of the user invoke this view. When you select **INVOKER**, the execution can succeed provided that the executor has permission to execute it. |
      

   2. On the **View definition** pane, configure the statement.

4. Click **Submit**.

5. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="querying-a-view"></span>
## Query a view

<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">Editing query results is not supported.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **View**, right\-click the target view, and select **Query view**.

4. On the **SQL query_target database** tab, go to the command execution area and click **Execute (F8)**  or press **F8**.

   After the execution is completed, you can view the execution results in the **Execution result** area.


<span id="editing-a-view"></span>
## Edit a view


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **View**, right\-click the target view, and select **Edit view**.

4. On the **Edit view@{database name}**  tab, go to the **View definition** area and edit the view statement.

5. Click **Submit**.

6. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="deleting-a-view"></span>
## Delete a view

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">View deletion is irreversible. Proceed with caution.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **View**, right\-click the target view, and select **Delete view**.

4. In the **Execute** **SQL** dialog box, make sure that the statement is correct, and click **Execute**.


<span id="relevant-apis"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel the execution of an SQL command. |
