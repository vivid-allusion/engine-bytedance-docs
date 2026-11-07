---
title: "Trigger management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/trigger-management-for-mysql"
---

This topic describes how to visually create, edit, and delete triggers on the DBW data interaction platform, implementing data lifecycle management of databases.

<span id="prerequisites"></span>
## Prerequisites


* A table is created. For more information, refer to [Table management](https://docs.byteplus.com/en/docs/DBW/table-management-for-mysql).

* You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must be granted the required permissions, for example, for querying and modifying the specified database.   </div>
   

<span id="precautions"></span>
## Precautions


* We recommend that you do not create, delete, or edit triggers in the system database.

* Trigger deletion is irreversible. Proceed with caution.

* Actions such as creating or deleting objects may impact online business performance. It is recommended to perform these during off\-peak hours.


<span id="creating-a-trigger"></span>
## Create a trigger


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Trigger**, right\-click the target view, and select **Create trigger**.

3. On the **Create trigger@{datebase name}**  page, set the parameters for the trigger.

   1. Configure the basic information of the trigger.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Specify a custom trigger name according to the following naming rules:<br><br><br>* The trigger name must be unique in the database.<br><br>* The name must be 1 to 64 characters in length, and cannot be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* The name can consist of lowercase letters, digits, underscores (_), or hyphens (\-). |
      |**Trigger timing** |Select a trigger time to specify whether to trigger an event before or after the execution of another event. Valid values:<br><br><br>* **BEFORE**: The trigger activates after the recorded action. In other words, the statement is triggered after data insertion, deletion, or update is completed, having no impact on the insertion, deletion, or update.<br><br>* **AFTER**: The trigger activates before the recorded action. In other words, the statement is triggered first, and then the data is inserted, deleted, or updated. You can observe the operation that occurs after the insertion, deletion, or update and interrupt the operation as needed. |
      |**Event** |Select the type of the event that triggers the trigger. Valid values:<br><br><br>* **INSERT**: Data is inserted into the database.<br><br>* **UPDATE**: Data in the database is updated.<br><br>* **DELETE**: Data is deleted from the database. |
      |**Trigger table** |Enter the name of a triggering table. An update to this table will trigger an action to be performed before or after the update. |
      

   2. In the **Trigger statement** area, configure the statement to execute when the trigger activates.

4. Click **Submit**.

5. In the **Execute** **SQL** dialog box, make sure that the statement is correct, and click **OK**.


<span id="editing-a-trigger"></span>
## Edit a trigger


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Trigger**, right\-click the target view, and select **Edit trigger**.

4. On the **Edit trigger@{database name}**  tab, go to the **Trigger statement** area and edit the triggering statement.

5. Click **Submit**.

6. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="deleting-a-trigger"></span>
## Delete a trigger

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Trigger deletion is irreversible. Proceed with caution.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Trigger**, right\-click the target view, and select **Delete trigger**.

4. In the **Execute** **SQL** dialog box, make sure that the statement is correct, and click **Execute**.


<span id="relevant-apis"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel the execution of an SQL command. |
