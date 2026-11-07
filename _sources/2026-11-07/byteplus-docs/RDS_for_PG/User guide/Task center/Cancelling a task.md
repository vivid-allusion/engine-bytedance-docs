---
title: "Cancelling a task"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Cancelling_a_task"
---

RDS for PostgreSQL supports canceling pending tasks. This topic describes the steps to cancel a task.

<span id="BK4us9hB"></span>
## Prerequisites

The task is **Waiting for execution** or **Waiting for switch**.

<span id="6xaLntFA"></span>
## Precautions


* When the following task is initiated and selected to be executed in the **Specific time period** or **Maintenance window**, the task will enter the **Waiting for execution** state. The cancellation of the task takes effect immediately.

* When the following task is initiated and selected to be executed in the **Specific time period** or **Maintenance window**, the task will enter the **Running (before switching)**  state, and perform the corresponding resource preparation and background scheduling work. If a task is cancelled during this period, the cancellation is performed after the current phase (resource preparation and background scheduling) is completed.

   * Change specification ModifyDBInstanceSpec

* When the following task is initiated and selected to be executed **Immediately**, the task can not be cancelled.

   * Change specification ModifyDBInstanceSpec


<span id="FsYHExPX"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Task Center** to enter the **Task** list.

4. In the **Task** list, click the **Cancel** button in the **Actions** column of the target task.

5. In the pop\-up **Confirm to cancel** dialog box, click **OK**.


<span id="SoHkyghD"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyTask](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyTask) |Call the ModifyTask API to edit the task. |
