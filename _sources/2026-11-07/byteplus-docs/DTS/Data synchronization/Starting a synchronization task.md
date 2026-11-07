---
title: "Starting a synchronization task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/initiating_a_synchronization_task"
---

You can start paused synchronization tasks to continue data synchronization. This topic describes how to start a synchronization task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data synchronization task has been created, and the task status is **Paused**. Refer to [Task status instructions](https://docs.byteplus.com/en/docs/DTS/managing_synchronization_task_tags) for details about the synchronization task status.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Starting a reverse task in a bidirectional synchronization task separately is supported.

<span id=".5ZCv5Yqo5oyH5a6a5Lu75Yqh"></span>
## Start a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, click **Start** on the right of the target forward or reverse task progress.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select <strong>Unidirectional synchronization</strong> when creating the task, you can only view the forward synchronization task. If you select <strong>Bidirectional synchronization</strong>, you can view the forward and reverse synchronization tasks separately.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the task is a bidirectional synchronization task and the forward task status is suspended, starting the reverse synchronization task is supported.   </div>
   

5. In the **Start selected synchronization task?**  dialog box, click **Start**.


<span id=".5om56YeP5ZCv5Yqo5Lu75Yqh"></span>
## Batch start tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, select the tasks to be started, and click **Batch start** in the bottom menu bar.

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
