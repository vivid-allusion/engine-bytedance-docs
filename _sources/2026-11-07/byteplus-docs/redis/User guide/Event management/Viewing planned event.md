---
title: "Viewing planned event"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/manage-planned-event"
---

Cache for Redis provides events function, supporting software, hardware, or network upgrades on the physical machines that run instances. These operations are performed as planned events to ensure the stability and sustainability of database cloud services. This topic describes how to view event details (e.g., specific event actions, involved instances, planned execution time, latest deferrable time, and scope of impact).

## Prerequisites

You have received system notifications for maintenance events or have tasks scheduled during the maintenance period.

## Precautions

* The status of a scheduled maintenance event changes to **In progress** once execution starts. Instance node switchover may occur during the maintenance event execution process, which may result in second\-long non\-writability or temporary disconnections. Please ensure that your services operate with an automatic reconnection mechanism. For more information on supported event operations and their impact on your services, refer to [Event types and operation impact](https://docs.byteplus.com/en/docs/redis/event-center).

* Before the scheduled maintenance event is executed, its status is shown as **Waiting for execution**. Normal data access to the database will not be affected.

* After the scheduled maintenance event is completed, the instance's address and access method remain the same as the source instance. The instance's network configuration will not change, and migration tasks will not be affected by maintenance events.

* For system maintenance events, if special circumstances prevent maintenance events from being completed within the execution time, the system automatically cancels the current maintenance event and notifies you via email or in\-site messages. Please pay attention to relevant notifications. You can configure message reception settings in **Message center** page of the BytePlus console. For specific procedures, refer to [Message subscription and notification methods](https://docs.byteplus.com/en/docs/message_center/Message-Subscription-and-Notification-Methods).

* Redis does not limit the number of operations to change the execution time, but the planned execution time after each change must be later than the end time of the previous planned execution time and earlier than the latest deferred time. For more details, refer to [Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time).

* The Events displays impact scope information at different stages for "system maintenance" events, allowing you to determine if business avoidance actions are necessary. The impact scope is typically organized and displayed by shard and node role, including primary nodes, secondary nodes, and proxy nodes. If the page displays "Impact assessment is being generated," it means that impact assessment results have not yet been generated.

   * Pending execution stage: Displays "estimated impact scope" (which may be dynamically updated with changes in instance topology).

   * In progress/Completed stage: Displays "impact scope snapshot" (which reflects the actual impact scope locked during the execution stage).

* All times displayed in the Events are UTC+8 (Beijing Time).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the planned event belongs.

3. In the left navigation pane, select **NoSQL Database \> Redis \> Events**.

4. On the **Planned event** tab, you can view information about target events in the scheduled events list, including event ID, instance name and ID, event status, event actions, event type, planned execution time, and latest deferral time.

   > **tip**

   * > For eligible planned events, you can modify the execution time of the event, you can also advance or cancel the execution of an event. For specific procedure, refer to [Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time), [Executing planned event](https://docs.byteplus.com/en/docs/redis/execute-planned-event), and [Canceling planned event](https://docs.byteplus.com/en/docs/redis/cancel-planned-event).

   * > Click **Task details** in the **Impact scope** column of the target event to view detailed information about the event in the pop\-up **Event impact details** page, including event ID, instance name and ID, event status, event actions, event type, scheduled execution time, actual execution time, impact scope, event impact details, and overall impact description.

## Relevant APIs

|API |Description |
|---|---|
|[DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) |Call the DescribePlannedEvents API to query scheduled events of the target Redis instance within a specified time range. |
|[DescribePlannedEventImpactDetail](https://docs.byteplus.com/en/docs/redis/DescribePlannedEventImpactDetail?lang=en) |Call the DescribePlannedEventImpactDetail API to query impact information about planned events. |
