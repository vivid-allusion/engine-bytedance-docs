---
title: "Deleting a migration task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/deleting_a_migration_task"
---

This topic describes how to delete unnecessary migration tasks on the Database Transmission Service (DTS) console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If source and target instances are in different regions, you need to delete the task at the destination.

* When deleting a migration task, you can also delete the data verification task associated with this task at the same time. Tasks cannot be recovered or rolled back after deletion. Proceed with caution.


<span id=".6LS555So"></span>
## Billing

Data migration tasks currently only support pay\-as\-you\-go billing. Deleting the task does not involve unsubscribing fees and will be billed based on the actual resource usage.

<span id=".5Yig6Zmk5oyH5a6a5Lu75Yqh"></span>
## Delete a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, select **More operations** \> **Delete** at the upper right of the target task.

5. In the **Delete selected migration task?**  dialog, click **Delete**.

   When deleting a migration task, you can also delete the data verification task associated with this task at the same time.


<span id=".5om56YeP5Yig6Zmk5Lu75Yqh"></span>
## Batch delete tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, select the migration tasks to delete, then at the bottom menu bar, choose **More operations** \> **Batch delete**.

5. In the **Delete task** dialog box, click **OK**.

   Confirm the tasks to be deleted in the **Delete task** dialog box. To exclude any tasks, click **Remove** in the **Actions** column to delete them. When deleting a migration task, you can also delete the data verification task associated with this task at the same time.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DeleteTransmissionTask](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTask) |Call the DeleteTransmissionTask API to delete a transmission task |
|[DeleteTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTasks) |Call the DeleteTransmissionTasks API to batch delete transmission tasks |
