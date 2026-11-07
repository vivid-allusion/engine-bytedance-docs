---
title: "Starting a migration task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/initiating_a_migration_task"
---

You can start paused migration tasks to continue data migration. This topic describes how to start a migration task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The data migration task is created, and the task state is **Paused** or **To be started**. For details about migration task status, refer to [Instructions on migration task status](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions#.5Lu75Yqh54q25oCB6K-05piO).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If source and target instances are in different regions, you need to start the task in the target region.

<span id=".5ZCv5Yqo5oyH5a6a5Lu75Yqh"></span>
## Start a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, click **Start** at the top right of the target task.

5. In the **Start selected migration task?**  dialog box, click **Start**.


<span id=".5om56YeP5ZCv5Yqo5Lu75Yqh"></span>
## Batch start tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, check the migration tasks to start and click **Batch start**.

5. In the **Start task** dialog box, click **OK**.

   Confirm the tasks to be started in the **Start task** dialog box. To exclude any tasks, click **Remove** in the **Actions** column to delete them.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[StartTransmissionTask](https://docs.byteplus.com/en/docs/DTS/StartTransmissionTask) |Call StartTransmissionTask to start transmission tasks to be started. |
|[StartTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/StartTransmissionTasks) |Call StartTransmissionTasks to batch start transmission tasks to be started. |
|[ResumeTransmissionTask](https://docs.byteplus.com/en/docs/DTS/ResumeTransmissionTask) |Call the ResumeTransmissionTask API to recover failed transmission tasks. |
|[ResumeTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/ResumeTransmissionTasks) |Call the ResumeTransmissionTasks API to batch recover failed transmission tasks. |
