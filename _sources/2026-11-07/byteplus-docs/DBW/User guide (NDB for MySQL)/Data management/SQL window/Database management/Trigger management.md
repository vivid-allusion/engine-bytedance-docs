---
title: "Trigger management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Trigger_management"
---

This topic describes how to visually create, delete, and edit triggers on the Database Workshop (DBW) console to manage the entire lifecycle of triggers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services in regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* A table has been created. For more information, refer to [Table management](https://docs.byteplus.com/en/docs/DBW/Table_management#.5Yib5bu66KGo).

* You have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account#.5Yib5bu66LSm5Y-3).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must have the corresponding permissions for querying and modifying the corresponding database.   </div>
   

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* We recommend that you do not create, edit, or delete triggers in the system database.

* It can not be restored after deletion. Proceed with caution.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id=".5Yib5bu66Kem5Y-R5Zmo"></span>
## Create a trigger


1. Log on to the [data interaction platform for veDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Trigger**, right\-click the target trigger, and select **Create trigger**.

4. On the **Create trigger@{database name}**  page, configure the parameter information of the trigger.

   1. Configure trigger options, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Custom trigger name. Naming rules:<br><br><br>* The trigger name is unique within the database.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Triggering timing** |Select a trigger timing as required to trigger another trigger when a trigger is executed. The following options are supported:<br><br><br>* **BEFORE**: After the operation is recorded, it is triggered after the data addition, deletion, or modification is completed. The triggered statement occurs after the data addition, deletion, or modification operations are monitored and can not affect the preceding operations.<br><br>* **AFTER**: Triggered before the operation is recorded, it triggers first and then completes the data addition, deletion, or modification. The trigger statement precedes the monitored data operations, allowing you to determine subsequent actions after the changes and intervene as required. |
      |**Trigger** |Select the trigger type to trigger as needed. The following options are supported:<br><br><br>* **INSERT**: Inserts data into the database.<br><br>* **UPDATE**: Updates data in the database.<br><br>* **DELETE**: Deletes data from the database. |
      |**Trigger table** |Enter the table name. When the table changes, you can trigger your behavior before and after the table changes. |
      

   2. On the **Trigger statement** pane, configure the statement as required.

5. Click **Submit**.

6. In the **Execute**  **SQL** dialog box, confirm the new statement, and then click **OK**.


<span id=".57yW6L6R6Kem5Y-R5Zmo"></span>
## Edit a trigger


1. Log on to the [data interaction platform for veDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Trigger**, right\-click the target trigger, and select **Edit trigger**.

4. On the **Edit trigger@{database name}**  tab, locate the **Trigger statement** pane, edit the trigger statement as required.

5. Click **Submit**.

6. In the **Execute**  **SQL** dialog box, confirm the execution statement and click **Execute**.


<span id=".5Yig6Zmk6Kem5Y-R5Zmo"></span>
## Delete a trigger

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It can not be restored after deletion. Proceed with caution.</div>



1. Log on to the [data interaction platform for veDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Trigger**, right\-click the target trigger, and select **Delete trigger**.

4. In the **Execute**  **SQL** dialog box, confirm the deletion statement, and then click **Execute**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
