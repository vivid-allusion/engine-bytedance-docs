---
title: "Deleting a synchronization task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/deleting_a_synchronization_task"
---

This topic describes how to delete unnecessary synchronization tasks on the Database Transmission Service (DTS) Console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If the **synchronization** task is a bidirectional synchronization task, the forward or reverse synchronization task cannot be deleted separately. If you need to batch delete tasks, select the forward synchronization task.

* When deleting a migration task, you can also delete the data verification task associated with this task at the same time. Task delete is not supported for recovery, and the actions that have been executed will not be rolled back. Execute with caution.


<span id=".6LS555So"></span>
## Billing

Deleting a task is the same as unsubscribing from the task. Once deleted, here's how you'll be billed based on your chosen billing method:


* Pay\-as\-you\-go: No refunds are involved when a task is deleted. You will only be charged for the resources that were actually consumed.

* Subscription: Deleting a task is equivalent to unsubscribing. After unsubscribing from a subscription DTS task, the refund will be credited to the account balance. For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).


<span id=".5Yig6Zmk5oyH5a6a5Lu75Yqh"></span>
## Delete a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list ** page, click **Delete** in the upper\-right corner of the target task.

5. In the **Delete selected synchronization task?**  dialog box, click **Delete**.

   When deleting a migration task, you can also delete the data verification task associated with this task at the same time.


<span id=".5om56YeP5Yig6Zmk5Lu75Yqh"></span>
## Batch delete tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list ** page, select the tasks to delete, then select  **...**  \> **Batch delete** in the bottom menu bar.

5. In the **Delete task** dialog box, click **OK**.

   Confirm the tasks to be deleted in the **Delete task** dialog box. To exclude any tasks, click **Remove** in the **Actions** column to delete them. When deleting a migration task, you can also delete the data verification task associated with this task at the same time.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DeleteTransmissionTask](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTask) |Call the DeleteTransmissionTask API to delete a transmission task |
|[DeleteTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTasks) |Call the DeleteTransmissionTasks API to batch delete transmission tasks |
