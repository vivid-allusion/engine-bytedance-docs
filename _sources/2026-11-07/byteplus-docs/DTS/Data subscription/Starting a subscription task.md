---
title: "Starting a subscription task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/initiating_a_subscription_task"
---

You can start an unpaid subscription task to resume the data subscription. This topic describes how to start a subscription task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A task has been created but remains unstarted in the **Confirm order** configuration wizard. For more information, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id=".5ZCv5Yqo5oyH5a6a5Lu75Yqh"></span>
## Start a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, click **Start** in the upper\-right corner of the target task.

5. In the **Start selected subscription task?**  dialog box, click **Start**.


<span id=".5om56YeP5ZCv5Yqo5Lu75Yqh"></span>
## Batch start tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, select the tasks to be started. in the bottom menu bar, click **Batch start**.

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
