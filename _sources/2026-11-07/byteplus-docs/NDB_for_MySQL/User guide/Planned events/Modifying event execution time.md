---
title: "Modifying event execution time"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_event_execution_time"
---

Planning operations events to be executed within a maintainable time period can also be modified to execute immediately. This article describes how to modify the execution time of an event.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The event status is **Waiting for execution**.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only events with the modified event type as **configuration change** and events of **parameter modification** are supported.

* You can select up to 100 operation and maintenance events to modify their execution time in batches.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left navigation bar, select **NDB for MySQL** \> **Planned events**.

4. In the Planned events list, click the **Modify execution time** in the target event **Actions** column, or you can check multiple events to modify the execution time in bulk.

5. In the dialog box that pops up, re\-select the **Execution method** and click **OK**.

   * **Execute now**: Advance the operation and maintenance events in the maintainable time period to execute immediately now.

   * **Execute during maintainable window**: Execute during the maintenance time period. For more information about maintainable time windows, see [Configuring maintenance window](https://www.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyScheduleEvents](https://www.byteplus.com/en/docs/NDB_for_MySQL/ModifyScheduleEvents) |Call the ModifyScheduleEvents to modify the execution time of the event to be executed. |
