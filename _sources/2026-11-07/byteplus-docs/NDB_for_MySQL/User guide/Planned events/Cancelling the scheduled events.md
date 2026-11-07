---
title: "Cancelling the scheduled events"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Cancelling_the_scheduled_events"
---

Operations events scheduled to be executed within a maintainable time period can also be cancelled. This article describes how to cancel a planned event.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The event status is **Waiting for execution**.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Cancel event types of **configuration changes** and **modify parameters** are supported only.

* A maximum of 100 events can be selected for batch cancellation.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left navigation bar, select **NDB for MySQL** \> **Planned events**.

4. In the list of planned events, click **Cancel** in the **Actions** column of the target event, or select multiple events to cancel them in batches.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Once a planned event is canceled, it cannot be executed again and you need to re\-initiate the change task. Please operate with caution.   </div>
   

5. Click **OK** in the pop\-up dialog box.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[CancelScheduleEvents](https://www.byteplus.com/en/docs/NDB_for_MySQL/CancelScheduleEvents) |Call the CancelScheduleEvents to cancel pending scheduled events. |
