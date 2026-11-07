---
title: "Event management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/event-management-for-mysql"
---

This topic describes how to visually create, edit, and delete events on the DBW data interaction platform, implementing data lifecycle management of databases.

<span id="prerequisites"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must be granted the required permissions, for example, for querying and modifying the specified database.   </div>
   

<span id="precautions"></span>
## Precautions


* We recommend that you do not create, delete, or edit events in the system database.

* Event deletion is irreversible. Proceed with caution.

* Actions such as creating or deleting objects may impact online business performance. It is recommended to perform these during off\-peak hours.


<span id="creating-an-event"></span>
## Create an event


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Event**, right\-click the target view, and select **Create event**.

3. On the **Create event@{datebase name}**  tab, set the following parameters.

   1. On the **Event options** pane, set the following parameters.

      
      |Parameter |**Description** |
      |---|---|
      |**Name** |Specify a custom event name according to the following naming rules:<br><br><br>* The event name must be unique in the database.<br><br>* The name must be 1 to 64 characters in length, and cannot be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* The name can consist of lowercase letters, digits, underscores (_), or hyphens (\-). |
      |**Scheduling method** |Select a scheduling method for the event. Valid values:<br><br><br>* **Fixed time**: Schedule the event at a fixed time.<br><br>* **Cycle time**: Schedule the event at a specified interval. |
      |**Fixed time** |Specify the fixed time to schedule the event.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is editable when you select <strong>Fixed time</strong> for <strong>Scheduling method</strong>.</div><br> |
      |**Interval** |Specify the interval at which you want to schedule the event.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is editable when you select <strong>Cycle time</strong> for <strong>Scheduling method</strong>.</div><br> |
      |**When event completes** |Specify whether to retain the event after the event is completed. |
      |**Comment** |Optional. Describe the event to help identify it. |
      

   2. In the **Event definition** area, configure the statement.

4. Click **Submit**.

5. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="editing-an-event"></span>
## Edit an event


1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Event**, right\-click the target view, and select **Edit event**.

4. On the **Edit event@target database** tab, go to the **Event definition** area and edit the event statement.

5. Click **Submit**.

6. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="deleting-an-event"></span>
## Delete an event

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Event deletion is irreversible. Proceed with caution.</div>



1. Log on to the [data interaction platform for RDS for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon next to the database and select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Event**, right\-click the target view, and select **Delete event**.

4. In the **Execute** **SQL** dialog box, make sure that the statement is correct and click **Execute**.


<span id="relevant-apis"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel the execution of an SQL command. |
