---
title: "View management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/View_management"
---

This topic explains how to visually create, delete, and manage views within the SQL window of the Database Workshop (DBW), enabling full lifecycle management of views.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You must have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you created must have corresponding permissions such as querying and modifying the database.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Editing query results after querying a view is not supported.

* It is recommended not to create, edit, or delete views in the system database.

* Deleted views cannot be restored. Proceed with caution.

* Your operations such as creation and deletion may impact online business operations. It is recommended to perform them during off\-peak hours.


<span id=".5Yib5bu66KeG5Zu-"></span>
## Create view


1. Log on to [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand the **View**, right\-click on the target view, and select **Create view**.

4. On the **Create view @{Database Name}**  page, configure the database parameters.

   1. Configure view options as shown in the table below:

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Custom view name. Naming rules:<br><br><br>* The view name is unique within the database.<br><br>* Length must be between 1 and 64 characters and cannot be empty.<br><br>* Must start with a letter and end with a letter or number.<br><br>* Can consist of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Definer** |(Optional) Specify the definer to indicate the use of that definer's permissions for execution. |
      |**Check options** |Select the check options as needed. When creating a view with the `WITH CHECK OPTION` clause, MySQL checks each row being modified through the view. The check option supports the following selections:<br><br><br>* **Default**: When selecting the default, the check option defaults to CASCADED.<br><br>* **LOCAL**: When operating on the current view, the LOCAL check option recursively checks if the views the current view depends on have a check option. If there is one, it checks; if not, it does not check.<br><br>* **CASCADED**: When operating on the current view, if the current view has a check option, the inserted data must satisfy the conditions of both the current view and the views it depends on; if the current view does not have a check option, the inserted data must satisfy the conditions of the views it depends on that have a check option and their dependent views. |
      |**Algorithm** |Select the view processing algorithm as needed, with the following options:<br><br><br>* **UNDEFINED**: Indicates that MySQL automatically selects the algorithm.<br><br>* **MERGE**: Indicates that the text of the statement referencing the view and the view definition is merged, replacing the corresponding part of the statement with the view definition.<br><br>* **TEMPTABLE**: Indicates that the result of the view is stored in a temporary table, which is then used to execute the statement. |
      |**Security** |Select the security as needed, indicating whose permissions to use during execution. Supports the following options:<br><br><br>* **Default**: When selecting default, the security defaults to DEFINER.<br><br>* **DEFINER**: Executes with the permissions of the user specified by the definer (DEFINER). When selecting DEFINER, the user specified by DEFINER must exist in the database and have the corresponding operation permissions to execute successfully.<br><br>* **INVOKER**: Executes with the permissions of the user invoking the view. When selecting INVOKER, the executor only needs to have execution permissions to succeed. |
      

   2. In the **View definition** section, configure the statement as needed.

5. Click **Submit**.

6. In **Execution** **SQL** dialog box, confirm the execution statement and click **Execute**.


<span id=".5p-l6K-i6KeG5Zu-"></span>
## Query view

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Editing operations on query results are not supported.</div>



1. Log on to the [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand the **View**, right\-click on the target view, and select **Query view**.

4. In the **SQL query_target database** command execution area, click **Execute (F8)**  or press the **F8** key.

   After successful execution, you can view the execution result in the **Execution result** section.


<span id=".57yW6L6R6KeG5Zu-"></span>
## Edit view


1. Log on to the [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand **View**, right\-click the target view, and select **Edit view**.

4. In the **Edit view@{Database Name}**  tab, edit the view statement as needed in the **View definition** section.

5. Click **Submit**.

6. In the **Execute** **SQL** dialog box, confirm the execution statement, and then click **Execute**.


<span id=".5Yig6Zmk6KeG5Zu-"></span>
## Delete view

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleted views cannot be restored. Proceed with caution.</div>



1. Log on to [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand **View**, right\-click the target view, and select **Delete view**.

4. In **Execute** **SQL** dialog box, confirm the delete statement, then click **Execute**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute command statements. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to maintain the SQL session window. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to exit the SQL session window. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Cancel SQL execution by calling the DataCancelExec interface. |
