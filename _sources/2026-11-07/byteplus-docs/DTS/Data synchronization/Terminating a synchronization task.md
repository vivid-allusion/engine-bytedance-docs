---
title: "Terminating a synchronization task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/terminating_a_synchronization_task"
---

You can terminate the tasks that must be stopped or have been paused to avoid overwriting the source data into the target database. This topic describes how to terminate a synchronization task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data synchronization task is created, and the task status is ** In progress** or **Paused**. Refer to [Task status instructions](https://docs.byteplus.com/en/docs/DTS/managing_synchronization_task_tags) for details about the synchronization task status.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If the synchronization task is a bidirectional synchronization task, the reverse task is also terminated when the forward synchronization task is terminated. Terminating reverse tasks in bidirectional synchronization tasks separately is not supported.

* After the task is terminated, the task status becomes synchronization complete.

* Restart is not supported after task termination, and executed operations will not rollback. Proceed with caution.


<span id=".6LS555So"></span>
## Description


* When terminating a synchronization task, you can also terminate the data verification task associated with this task at the same time.

* If only the synchronization task is terminated, terminating the task will not affect the execution of the data verification task.


<span id=".6LS555So"></span>
## Billing

Terminating a task is the same as unsubscribing from the task. Once terminated, here's how you'll be billed based on your chosen billing method:


* Pay\-as\-you\-go: Terminating a task does not involve Unsubscribe amount, and will be charged according to the actual amount of resources used.

* Subscription: Terminating a task is equivalent to unsubscribing. After unsubscribing from a subscription DTS task, the refund will be credited to the account balance. For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).


<span id=".57uI5q2i5oyH5a6a5Lu75Yqh"></span>
## Terminate a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, click **Terminate** in the upper right corner of the target synchronization task.

5. In the **Terminate selected synchronization task?**  pop\-up, choose whether to terminate the data verification tasks associated with this task as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, <strong>Terminate the selected task and simultaneously terminate the associated data verification tasks.</strong> is checked, meaning that terminating the synchronization task also terminates all its associated data verification tasks.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Uncheck <strong>Terminate the selected task and simultaneously terminate the associated data verification tasks</strong> to terminate only the synchronization task without affecting the data verification tasks.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The pop\-up displays up to 5 associated verification tasks. Selecting this option will terminate all verification tasks linked to this task.   </div>
   

6. Click **Terminate**.


<span id=".5om56YeP57uI5q2i5Lu75Yqh"></span>
## Batch terminate tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, select the target tasks to terminate, and select **...**  in the bottom menu bar. \> **Batch terminate**.

5. In the **Terminate task** pop\-up, choose whether to terminate the related data verification tasks of the selected tasks as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, <strong>Terminate the selected task and simultaneously terminate the associated data verification tasks.</strong> is checked, meaning that terminating the synchronization task also terminates all its associated data verification tasks.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Uncheck <strong>Terminate the selected task and simultaneously terminate the associated data verification tasks</strong> to terminate only the selected synchronization tasks without affecting the execution of their related data verification tasks.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Confirm the tasks to terminate in the <strong>Terminate task</strong> pop\-up. To exclude tasks from termination, click <strong>Remove</strong> in the <strong>Actions</strong> column to delete them.   </div>
   

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[StopTransmissionTask](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTask) |Call the StopTransmissionTask API to terminate a transmission task. |
|[StopTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTasks) |Call the StopTransmissionTasks API to batch terminate transmission tasks. |
