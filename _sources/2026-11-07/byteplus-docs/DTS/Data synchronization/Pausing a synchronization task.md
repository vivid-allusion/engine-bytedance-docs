---
title: "Pausing a synchronization task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/suspending_a_synchronization_task"
---

During data synchronization, if you encounter peak business hours and measures such as modifying the link specifications or adjusting the full synchronization rate still can not meet the requirements, you may choose to suspend the synchronization task. This topic describes how to pause a synchronization task through the DTS console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data synchronization task is **In progress**. Refer to [Task status instructions](https://docs.byteplus.com/en/docs/DTS/managing_synchronization_task_tags) for details about the synchronization task status.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can independently suspend reverse tasks in bidirectional synchronization tasks.

* After you suspend the task, the Sync status changes to Suspended. You can resume synchronization by starting the synchronization task. For the instructions on how to Start a synchronization task, refer to [Start a sync task](https://docs.byteplus.com/en/docs/DTS/initiating_a_synchronization_task).

* When a task is suspended for more than 7 days, the task can not be resumed due to expired logs required by the source database. To avoid potential irrecoverable task issues, it is recommended that the pause duration does not exceed 24 hours.

* When a normally running synchronization task is paused, the current session (i.e., the database session between the DTS server and the target database) is not immediately terminated. Simultaneously, if the transactions being executed by the current session are not committed, the resources occupied by these transactions \- such as row locks and table locks \- will not be released. As a result, other sessions may be blocked when requesting these resources, which could potentially impact the existing performance of the database. Therefore, it may cause the SQL statements of other sessions to be blocked. If a task remains suspended for an extended period (exceeding the inactive session timeout parameter), the session will be terminated and transactions will be rolled back. When suspending a task, it is recommended to confirm that DTS is not migrating large transactions, as this may otherwise lead to degraded database performance.


<span id=".5pqC5YGc5oyH5a6a5Lu75Yqh"></span>
## Pause a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, to the right of the target forward or reverse task progress, select  **...**  \> **Suspend**.

5. In the **whether to suspend the selected synchronization task** dialog box, click **Suspend**.


<span id=".5om56YeP5pqC5YGc5Lu75Yqh"></span>
## Batch pause tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, select the tasks you want to suspend, and in the bottom menu bar, click **Batch suspend**.

5. In the **Suspend task** dialog box, click **OK**.

   Confirm the tasks to be paused in the **Pause task** dialog box. To exclude any tasks, click **Remove** in the **Actions** column to delete them.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[SuspendTransmissionTask](https://docs.byteplus.com/en/docs/DTS/SuspendTransmissionTask) |Call the SuspendTransmissionTask API to pause the transmission task. |
|[SuspendTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/SuspendTransmissionTasks) |Call the SuspendTransmissionTasks API to batch pause transmission tasks. |
