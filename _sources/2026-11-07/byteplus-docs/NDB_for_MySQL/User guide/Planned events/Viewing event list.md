---
title: "Viewing event list"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list"
---

To ensure the sustainability of database cloud services, NDB for MySQL will initiate planned maintenance events to upgrade the software, hardware, and network of the machines where some of your instances are located. The planned event list displays all maintenance events planned to be executed within the maintenance time period in the specified region of the target account.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After the planned operation and maintenance event starts to execute, it will enter the execution state. Instance node switching may occur during the execution of operation and maintenance events. During the node switching process, there may be second\-level unwritable or connection flash disconnection. Ensure that your business has an automatic reconnection mechanism.

* Two types of scheduled events, **system maintenance** and **user actions**, are currently supported, including:

   * **System maintenance**: Mainly to upgrade the hardware and software and network of the machine where the instance is located.

   * **User Actions**: Currently only configuration changes and parameter modifications are supported within maintainable time windows.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left navigation bar, select **NDB for MySQL** \> **Planned events**.

4. Details of all events under the target account can be viewed in the list of **Planned events**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports searching for target events by instance ID, event ID, and start/end time.   </div>
   

   
   |Column name |Description |
   |---|---|
   |**Event ID** |Event ID. |
   |**Instance name/ID** |The instance name and instance ID corresponding to the event. |
   |**Event state** |The status of a scheduled event, including **Waiting for execution**, **Executing**, **Execution failed**, **Completed**, and **Cancelled**.<br><br>Support for filtering events by event status. |
   |**Event type** |Shows the types of events in the **Planned events** list, including **Configuration change**, **Modify parameters**, and **Version upgrade**.<br><br>Support for filtering events by event type. |
   |**Scheduled execution time** |Scheduled execution time. |
   |**Start time/End time** |Start time/End time. |
   |**Affiliated project** |The project to which the event corresponds to the instance. |
   |**Event details** |If the event execution fails, you can view the failure information here. |
   |**Actions** |The following actions are supported for events with **Event status** as ** Waiting for execution**:<br><br><br>* [Modifying event execution time](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_event_execution_time)<br><br>* [Cancelling the scheduled events](https://www.byteplus.com/en/docs/NDB_for_MySQL/Cancelling_the_scheduled_events) |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeScheduleEvents](https://www.byteplus.com/en/docs/NDB_for_MySQL/DescribeScheduleEvents) |Call the DescribeScheduleEvents API to view the scheduled events of the current account. |
