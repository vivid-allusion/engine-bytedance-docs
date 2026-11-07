---
title: "Deleting data subscription task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/deleting_a_subscription_task"
---

This topic describes how to delete unnecessary subscription tasks on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A subscription task has been created. For more information, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Deleting tasks in progress is not supported.

* Deleted tasks can not be recovered, and executed operations will not be rolled back. Proceed with caution.


<span id=".6LS555So"></span>
## Billing

Deleting a task is the same as unsubscribing from the task. Once deleted, here's how you'll be billed based on your chosen billing method:


* Pay\-as\-you\-go: No refunds are involved when a task is deleted. You will only be charged for the resources that were actually consumed.

* Subscription: Deleting a task is equivalent to unsubscribing. After unsubscribing from a subscription DTS task, the refund will be credited to the account balance. For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/6269/81013#.5LqM44CB6Z2e5LiD5aSp5peg55CG55Sx6YCA6K6i6K-05piO).


<span id=".5Yig6Zmk5oyH5a6a5Lu75Yqh"></span>
## Delete a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, in the upper\-right corner of the target subscription task, select **More operations** \> **Delete**.

5. In the **Whether to delete the selected task** dialog box, click **Delete**.


<span id=".5om56YeP5Yig6Zmk5Lu75Yqh"></span>
## Batch delete tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, select the tasks to delete, then in the bottom menu bar, choose **More operations** \> **Batch delete**.

5. In the **Delete task** dialog box, click **OK**.


Confirm the tasks to be deleted in the **Delete task** dialog box. To exclude any tasks, click **Remove** in the **Actions** column to delete them.

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DeleteTransmissionTask](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTask) |Call the DeleteTransmissionTask API to delete a transmission task |
|[DeleteTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTasks) |Call the DeleteTransmissionTasks API to batch delete transmission tasks |
