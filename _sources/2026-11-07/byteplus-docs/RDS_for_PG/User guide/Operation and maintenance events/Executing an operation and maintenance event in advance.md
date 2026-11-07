---
title: "Executing an operation and maintenance event in advance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Executing_an_operation_and_maintenance_event_in_advance"
---

RDS for PostgreSQL allows you to execute an operation and maintenance event in advance. This topic describes how to execute an operation and maintenance event in advance.

<span id="ryGZF1wh"></span>
## Prerequisites

The operation and maintenance event is in the **Waiting for execution** state.

<span id="VJU4iMuP"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left\-side navigation pane, click ** Operation and maintenance event** to go to the **Operation and maintenance event** list.

4. In the **Operation and maintenance events** list, click **Execute now** or **Switch now** in the **Actions** column of the target operation and maintenance event.

5. In the popped\-up **Confirm to execute now?**  or **Confirm to switch now?**  In the dialog box, click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Operation and maintenance events for host offline do not support canceling bindings for Execute now and Switch now.   </div>
   

<span id="lizWzNe6"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyPlannedEventExecuteTime) |Call the ModifyPlannedEventExecuteTime API to change the execution of scheduled operations events. |
