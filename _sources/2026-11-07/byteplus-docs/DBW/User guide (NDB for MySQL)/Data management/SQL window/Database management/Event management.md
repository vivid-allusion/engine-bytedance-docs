---
title: "Event management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Event_management"
---

This topic explains how to create, delete, and edit events in the data interaction platform of Database Workshop (DBW), enabling full lifecycle management of events.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account#.5Yib5bu66LSm5Y-3).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you created must have corresponding permissions such as querying and modifying the database.   </div>
   

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* It is recommended not to create, edit, or delete events in the system database.

* Deleted events cannot be recovered, so proceed with caution.

* Operations such as creating or deleting events may impact online business operations. It is recommended to perform these during off\-peak hours.


<span id=".5Yib5bu65LqL5Lu2"></span>
## Create event


1. Log on to the [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand **Event**, right\-click on the target event, and select **Create event**.

4. In the **Create event @{Database Name}**  tab, configure the following parameters.

   1. In the **Event options** section, configure the relevant parameters as shown in the table below.

      
      |**Parameters** |||**Description** |
      |---|---|---|---|
      |**Name** |||Customize the event name. Naming rules:<br><br><br>* The event name is unique within the database.<br><br>* The length must be between 1 and 64 characters and cannot be empty.<br><br>* It must start with a letter and end with a letter or number.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Scheduling method** |**Fixed time** |**Fixed time** |Set the event creation time point on demand. |
      ||**Cycle time** |**Start time** |Set the time point for loop event creation as needed. |
      |||**End time** |(Optional) Set the end time for executing cyclic event creation as needed.<br><br><br>* Set end time: If the end time is earlier than the last execution creation time plus the cycle, the creation event will expire.<br><br>* No end time set: If the execution time of a creation event exceeds the set cycle, the next execution time will be the end time of this creation event plus the cycle. |
      |||**Execution interval** |Set the execution interval for creating events as needed, supporting intervals by **Seconds**, **Minutes**, **Hours**, and **Days**. Additionally, it supports setting the execution cycle. |
      |**When the event is completed** |||Whether to retain the event upon completion. |
      |**Comment** |||(Optional) Event notes to help you identify the event. |
      

   2. In the **Event definition** section, configure statements as needed.

5. Click **Submit**.

6. In **Execute** **SQL** dialog box, confirm the execution statement, click **Execute**.


<span id=".57yW6L6R5LqL5Lu2"></span>
## Edit event


1. Log on to [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand the **Event**, right\-click on the target event, and select **Edit event**.

4. In the **Edit event@Target Database** tab, edit the event statement in the **Event definition** section.

5. Click **Submit**.

6. In **Execute SQL** dialog box, confirm the execution statement, then click **Execute**.


<span id=".5Yig6Zmk5LqL5Lu2"></span>
## Delete event

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deletion cannot be undone, proceed with caution.</div>



1. Log on to [NDB](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql)[ for MySQL data interaction platform](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span> icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, expand the **Event**, right\-click on the target event, and select **Delete event**.

4. In **Execute** **SQL** dialog box, confirm the execution statement and click **Execute**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interface to execute command statements. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive interface to maintain the SQL session window. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession interface to exit the SQL session window. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
