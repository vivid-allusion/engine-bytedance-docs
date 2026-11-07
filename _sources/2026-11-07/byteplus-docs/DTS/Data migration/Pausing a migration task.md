---
title: "Pausing a migration task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/suspending_a_migration_task"
---

During data migration, if you encounter peak business hours and measures such as modifying the link specification or adjusting the full migration rate still can not meet the requirements, you may choose to pause the migration task and resume it during off\-peak business hours. This topic describes how to pause a migration task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data migration task has been created, and the task status is **In progress**. For details about migration task status, refer to [Instructions on migration task status](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions#.5Lu75Yqh54q25oCB6K-05piO).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If source and target instances are in different regions, you need to pause the task at the destination.

* After pausing, the migration status changes to “Paused”. You can continue the migration by starting the migration task. For details, refer to [Starting a migration task](https://docs.byteplus.com/en/docs/DTS/initiating_a_migration_task).

* When a task is paused for more than 7 days, the task can not be resumed due to expired logs required by the source database. To avoid potential irrecoverable task issues, it is recommended that the pause duration does not exceed 24 hours.

* When a normally running migration task is paused, the current session (i.e., the database session between the DTS server and the target database) is not immediately terminated. Simultaneously, if the transactions being executed by the current session are not committed, the resources occupied by these transactions \- such as row locks and table locks \- will not be released. As a result, other sessions may be blocked when requesting these resources, which could potentially impact the existing performance of the database. If a task remains paused for an extended period (exceeding the inactive session timeout parameter), the session will be terminated and transactions will be rolled back. When pausing a task, it is recommended to confirm that DTS is not migrating large transactions, as this may otherwise lead to degraded database performance.


<span id=".5pqC5YGc5oyH5a6a5Lu75Yqh"></span>
## Pause a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the Migration task list page, select **More operations** \> **Pause** in the upper\-right corner of the target task in **Migration task list**.

5. In the **Pause selected migration task?**  dialog box, click **Pause**.


<span id=".5om56YeP5pqC5YGc5Lu75Yqh"></span>
## Batch pause tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, select the migration tasks to pause, then click **Batch pause** in the bottom menu bar.

5. In the **Pause task** dialog box, click **OK**.

   Confirm the tasks to be paused in the **Pause task** dialog box. To exclude any tasks, click **Remove** in the **Actions** column to delete them.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[SuspendTransmissionTask](https://docs.byteplus.com/en/docs/DTS/SuspendTransmissionTask) |Call the SuspendTransmissionTask API to pause the transmission task. |
|[SuspendTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/SuspendTransmissionTasks) |Call the SuspendTransmissionTasks API to batch pause transmission tasks. |
