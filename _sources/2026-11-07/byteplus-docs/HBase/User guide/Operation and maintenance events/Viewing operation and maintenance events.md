---
title: "Viewing operation and maintenance events"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Viewing_operation_and_maintenance_events"
---

To ensure the sustainability of the database cloud service, Table Storage for HBase initiates planned maintenance events to upgrade your instance or perform maintenance on its server. The planned event list displays all maintenance events planned to be executed within the maintenance time period in the specified region of the target account.

<span id="wBqTEKzn"></span>
## Precautions

Currently, only version upgrade and host maintenance events are displayed.

<span id="oGhFOonV"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/region:db+cn-beijing/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left\-side navigation pane, select **Operation and maintenance event**.

4. In the **Operation and maintenance event** list, you can view the details of all events for the target account.

   
   |**Column name** |**Description** |
   |---|---|
   |**Event ID** |Event ID. |
   |**Instance name/ID** |The instance name and instance ID corresponding to the event. |
   |**Event state** |The state of the event. It can be Waiting for execution, Executing, Failed, Succeeded, or Canceled. |
   |**Event type** |The type of the event displayed in the operation and maintenance event list. |
   |**Scheduled execution time** |Scheduled execution time. |
   |**Latest postponement time** |The latest time to which the target event can be postponed. |
   |**Event cause** |The reason for executing the target event. |
   |**Event details** |The impact of this event on the business. |
   |**Operation** |The following operations are supported for certain operation and maintenance events with an **Event status** of **Waiting for execution**:<br><br><br>* [Executing an operation and maintenance event in advance](https://docs.byteplus.com/en/docs/HBase/Executing_an_operation_and_maintenance_event_in_advance)<br><br>* [Modifying the execution time of operation and maintenance events](https://docs.byteplus.com/en/docs/HBase/Modifying_the_execution_time_of_operation_and_maintenance_events)<br><br>* [Canceling operation and maintenance events](https://docs.byteplus.com/en/docs/HBase/Canceling_operation_and_maintenance_events) |
