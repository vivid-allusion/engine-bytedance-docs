---
title: "Canceling planned event"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/cancel-planned-event"
---

Cache for Redis provides events function, supporting software, hardware, or network upgrades on the physical machines that run instances. These operations are performed as planned events to ensure the stability and sustainability of database cloud services. This topic describes how to cancel planned events.

## Prerequisites

Only events that meet all the following requirements can be canceled:

* The event type is **User action**.

* The event status is **Waiting for execution**.

* The time until the event's scheduled execution must be greater than 30 minutes.

## Precautions

* The status of a scheduled maintenance event changes to **In progress** once execution starts. Instance node switchover may occur during the maintenance event execution process, which may result in second\-long non\-writability or temporary disconnections. Please ensure that your services operate with an automatic reconnection mechanism. For more information on supported event operations and their impact on your services, refer to [Event types and operation impact](https://docs.byteplus.com/en/docs/redis/event-center).

* Before the scheduled maintenance event is executed, its status is shown as **Waiting for execution**. Normal data access to the database will not be affected.

* After the scheduled maintenance event is completed, the instance's address and access method remain the same as the source instance. The instance's network configuration will not change, and migration tasks will not be affected by maintenance events.

* For system maintenance events, if special circumstances prevent maintenance events from being completed within the execution time, the system automatically cancels the current maintenance event and notifies you via email or in\-site messages. Please pay attention to relevant notifications. You can configure message reception settings in **Message center** page of the BytePlus console. For specific procedures, refer to [Message subscription and notification methods](https://docs.byteplus.com/en/docs/message_center/Message-Subscription-and-Notification-Methods).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the planned event belongs.

3. In the left navigation pane, select **NoSQL Database \> Redis \> Events**.

4. On the **Planned event** tab, find the target event in the list of planned events and click **Cancel** in the right\-hand **Actions** column.

   > **tip**

   > Only events that meet all the following requirements can be canceled:

   * > The event type is **User action**.

   * > The event status is **Waiting for execution**.

   * > The time until the event's scheduled execution must be greater than 30 minutes.

5. In the pop\-up dialog box, click **OK**.

   > **tip**

   > After cancelling the planned event, the status of the instance will be restored to **Running**.
