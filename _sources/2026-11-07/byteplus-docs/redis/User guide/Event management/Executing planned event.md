---
title: "Executing planned event"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/execute-planned-event"
---

Cache for Redis supports advancing the execution time of a planned event waiting to be executed to the current time for immediate execution. This topic describes how to execute scheduled events in advance on the console.

## Prerequisites

* The status of scheduled events must be **Waiting for execution**.

* When the event type to be executed immediately is **System maintenance**, the status of the corresponding instance must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the planned event belongs.

3. In the left navigation pane, select **NoSQL Database \> Redis \> Events**.

4. On the **Planned event** tab, find the target event in the list of planned events and click **Execute now** in the right\-hand **Actions** column.

   > **tip**

   > Only events with the event status of **Waiting for execution** support immediate execution.

5. In the pop\-up dialog box, click **OK**.

   > **tip**

   > After clicking **OK**, the current event will start executing immediately and cannot be cancelled.

## Relevant APIs

|API |Description |
|---|---|
|[ExecutePlannedEvent](https://docs.byteplus.com/en/docs/redis/executeplannedevent) |Call the ExecutePlannedEvent API to immediately execute the scheduled event. |
