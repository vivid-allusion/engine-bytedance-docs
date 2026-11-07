---
title: "Modifying execution time"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/postpone-execution-time"
---

Cache for Redis provides events function, supporting software, hardware, or network upgrades on the physical machines that run instances. These operations are performed as planned events to ensure the stability and sustainability of database cloud services. This topic describes how to modify event execution time.

## Prerequisites

Only events that meet all the following requirements support changing execution time:

* The event type is **System maintenance**.

* The event status is **Waiting for execution**.

* The event's **The latest deferred time** indicates a specific time point, rather than **Cannot be postponed**.

* The time until the event's scheduled execution must be greater than 1 day.

## Precautions

* The status of a scheduled maintenance event changes to **In progress** once execution starts. Instance node switchover may occur during the maintenance event execution process, which may result in second\-long non\-writability or temporary disconnections. Please ensure that your services operate with an automatic reconnection mechanism. For more information on supported event operations and their impact on your services, refer to [Event types and operation impact](https://docs.byteplus.com/en/docs/redis/event-center).

* Before the scheduled maintenance event is executed, its status is shown as **Waiting for execution**. Normal data access to the database will not be affected.

* After the scheduled maintenance event is completed, the instance's address and access method remain the same as the source instance. The instance's network configuration will not change, and migration tasks will not be affected by maintenance events.

* Redis does not limit the number of operations to change the execution time, but the planned execution time after each change must be later than the end time of the previous planned execution time and earlier than the latest deferred time.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the planned event belongs.

3. In the left navigation pane, select **NoSQL Database \> Redis \> Events**.

4. On the **Planned event** tab, find the target event in the list of planned events and click **Modify execution time** in the right\-hand **Actions** column.

   > **tip**

   > Only events that meet all the following requirements support changing execution time:

   * > The event type is **System maintenance**.

   * > The event status is **Waiting for execution**.

   * > The event's **The latest deferred time** indicates a specific time point, rather than **Cannot be postponed**.

   * > The time until the event's scheduled execution must be greater than 1 day.

5. In the pop\-up dialog box, set the modified **Scheduled execution time**, including the execution date, start and end time.

   > **tip**

   > Redis does not limit the number of operations to change the execution time, but the planned execution time after each change must be later than the end time of the previous planned execution time and earlier than the latest deferred time.

6. Click **OK**.

   After clicking **OK**, the **Scheduled execution time** column of the target event will display the time you've modified.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/redis/modifyplannedeventexecutetime) |Call the ModifyPlannedEventExecuteTime API to modify the execution time of planned system maintenance events. |
