---
title: "Terminating a subscription task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/terminating_a_subscription_task"
---

You can terminate tasks that must be stopped or have been paused. This topic describes how to terminate a subscription task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A subscription task has been created, and the task status is **Paused** or **In progress**. For more information, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After termination, the task status will change to completed.

* Restart is not supported after task termination, and executed operations will not rollback. Proceed with caution.


<span id=".6LS555So"></span>
## Billing

Terminating a task is the same as unsubscribing from the task. Once terminated, here's how you'll be billed based on your chosen billing method:


* Pay\-as\-you\-go: No refunds are involved when a task is terminated. You will only be charged for the resources that were actually consumed.

* Subscription: Terminating a task is equivalent to unsubscribing. After unsubscribing from a subscription DTS task, the refund will be credited to the account balance. For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/6269/81013#.5LqM44CB6Z2e5LiD5aSp5peg55CG55Sx6YCA6K6i6K-05piO).


<span id=".57uI5q2i5oyH5a6a5Lu75Yqh"></span>
## Terminate a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, select **More operations** \> **Terminate** in the upper\-right corner of the target subscription task.

5. In the **Terminate selected task?**  dialog box, click **Terminate**.


<span id=".5om56YeP57uI5q2i5Lu75Yqh"></span>
## Batch terminate tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, select the tasks to terminate, then in the bottom menu bar, choose **More operations** \> **Batch terminate**.

5. In the **Terminate task** dialog box, click **OK**.

   Confirm the tasks to terminate in the **Terminate task** dialog box. To exclude tasks from termination, click **Remove** in the **Actions** column to delete them.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[StopTransmissionTask](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTask) |Call the StopTransmissionTask API to terminate a transmission task. |
|[StopTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTasks) |Call the StopTransmissionTasks API to batch terminate transmission tasks. |
