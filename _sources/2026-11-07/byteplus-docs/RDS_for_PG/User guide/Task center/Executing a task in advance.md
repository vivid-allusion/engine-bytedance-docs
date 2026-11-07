---
title: "Executing a task in advance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Executing_a_task_in_advance"
---

RDS for PostgreSQL supports executing tasks in advance that are in the Waiting for execution or Waiting for switch state. This topic introduces the procedure for executing a task in advance.

<span id="ESCOdB20"></span>
## Prerequisites

The task is in the **Waiting for switch** state.

<span id="xXypalg3"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Task Center** to enter the **Task** list.

4. In the **task** list, click **execute immediately** in the **Actions** column of the target task.

5. In the popped\-up **Confirm to execute immediately?**  dialog box, click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Once the execution is confirmed, the entire task, including the preparation phase and switch phase, will start immediately.   </div>
   

<span id="xWKpLsQf"></span>
## Related APIs


|API |Note |
|---|---|
|[ModifyTask](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyTask) |Call the ModifyTask API to edit the task. |
