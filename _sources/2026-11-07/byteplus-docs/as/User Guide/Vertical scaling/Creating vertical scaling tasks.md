---
title: "Creating vertical scaling tasks"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Creating-a-vertical-scaling-task"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

This topic describes how to create a vertical scaling task. Based on your needs, you can configure the task to run immediately, at a specified time, or periodically.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You can change the instance type only for [pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) instances (excluding [spot instances](https://docs.byteplus.com/en/docs/ecs/Spot_Instance)).

* The allowed target instance types vary based on the original instance type. Refer to [Instance type modification overview](https://docs.byteplus.com/en/docs/ecs/Overview-2) to select a supported instance type.

* Vertical scaling tasks only support upgrade or downgrade operations. Only one instance type can be selected for one task. You can create multiple vertical scaling tasks to meet different adjustment needs.


<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* When vertical scaling tasks are executed, instances are handled differently based on [instance states](https://docs.byteplus.com/en/docs/as/Instance-lifecycle#.5a6e5L6L54q25oCB), with details as follows:

   * An instance in the "Running" state is automatically restarted when the task is executed.

   * An instance in the "Stopped" state is automatically started and incurs fees when the task is executed.

   * For an instance in the "Under protection" status, the vertical scaling task can be executed normally.

* [States of scaling groups](https://docs.byteplus.com/en/docs/as/Lifecycle#.5Ly457yp57uE54q25oCB) to which instances belong do not impact executions of vertical scaling tasks.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the region of your target resource.

3. Click the "Create Vertical Scaling" button to configure the task.

   
   |Parameters |Description |Sample value |
   |---|---|---|
   |**Task settings** |||
   |Task name |Enter the name of the vertical scaling task. |as01 |
   |Task type |Select the type of change to the instance type.<br><br><br>* Upgrade: Upgrades the instance type of the target instance to enhance computing capability.<br><br>* Downgrade: Downgrades the instance type of the target instance to reduce computing capability. |Upgrade |
   |Trigger type |Currently, tasks can be triggered only on a time basis. |Timed trigger |
   |Timing type |Specify the time and frequency for triggering the task.<br><br><br>* Execute immediately: The task runs once immediately after creation and ends upon completion.<br><br>* Execute at the specified time: The task runs once at the time you specified and ends upon completion. After the task is created, the task state changes to "Waiting". The task runs once at the specified time and ends after the execution is completed.<br><br>* Periodic execution: You need to select the recurrence cycle, execution time, and recurrence end time. Tasks of the periodic execution type run repeatedly. After the task is created, the task state changes to "Waiting". The task runs when the execution time is reached. After task execution is complete, the task state changes back to "Waiting". When the recurrence end time is reached, the task ends. |Execute immediately |
   |Recurrence |This parameter needs to be configured only when the timing type is "Periodic execution".<br><br>Specify that scaling actions repeat by day, week, or month. The [Cron expression](https://docs.byteplus.com/en/docs/as/Cron-expressions) feature is supported. |By day |
   |Select time/week/date/Cron expression |This parameter needs to be configured only when the timing type is "Periodic execution".<br><br>Select a time to repeatedly trigger scaling actions.<br><br><br>* If the recurrence cycle is set to "By month" and a date later than the 28th is selected, the scaling operation will not be executed for that month if the selected date does not exist.<br><br>* The exact time of repeated execution is the hour and minute specified in the execution time. If you use a Cron expression to specify the hour and minute, the Cron expression takes precedence.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The interval between periodic tasks must not be less than 30 minutes. Otherwise, the instance type may be changed frequently, impacting the high availability of your business.</div><br> |Run every four days |
   |Time zone |This parameter needs to be configured only when the timing type is "Periodic execution".<br><br>Currently, only "UTC +08:00" (corresponding to Beijing time) is supported. |UTC +08:00 |
   |Executed at |This parameter needs to be configured only when the timing type is "Periodic execution".<br><br>Select the time to start executing the scaling operation. You can choose a specific time for a given date (year, month, day), accurate to the minute.<br><br><br>* If no specific time point is selected, this parameter defaults to the current time point. |2022\-11\-10 23:00 |
   |Expired at |This parameter needs to be configured only when the timing type is "Periodic execution".<br><br>Select the time to end executing the scaling operation. You can choose a specific time for a given date (year, month, day), accurate to the minute.<br><br><br>* If no exact time is specified, the parameter defaults to the time one day/week/month from the current time, based on the selected recurrence cycle. |2022\-11\-11 23:00 |
   |**Instance type selection** |||
   |Select instances |Select the instance whose type you want to change. The list only displays pay\-as\-you\-go instances in the region you selected. |ecs01 |
   |Instance Type |Select the target instance type. Only an instance type that supports the type change feature can be selected. For details, refer to [Instance type modification overview](https://docs.byteplus.com/en/docs/ecs/Overview-2).<br><br><br>* For a task of the "Upgrade" type, you can only select an instance type with both vCPU and memory larger than the current specifications.<br><br>* For a task of the "Downgrade" type, you can only select an instance type with both vCPU and memory smaller than the current specifications. |\-\- |
   

6. Click the "OK" button to complete the operation. 

   At this point, the vertical scaling task is successfully created and is in the **Waiting** or **Running** status.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Refer to [Viewing vertical scaling task details](https://docs.byteplus.com/en/docs/as/Viewing-the-details-of-a-vertical-scaling-task) to check the detailed execution status of the task.
