---
title: "Modifying data synchronization task specifications"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/modifying_synchronization_task_specifications"
---

You can adjust the task link specification during the data synchronization task execution process based on business data pressure. This topic explains how to change the link specifications of a synchronization task on the Database Transmission Service (DTS) Console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A synchronization task has been created. Refer to [Overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions) for detailed operations.

<span id=".6LS555So6K-05piO"></span>
## Billing

After changing the link specification of a synchronization task, BytePlus will recalculate billing based on the changes to the task, as follows:


* Pay\-as\-you\-go: The modified task will be re\-billed at the next full hour after the modification.

* Subscription: The task takes effect immediately after payment.


For more information, refer to Configuration change and unsubscription.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The link specification can only be changed when the synchronization process enters the incremental synchronization stage. Refer to [Viewing the synchronization progress](https://docs.byteplus.com/en/docs/DTS/viewing_synchronization_progress) for how to view the synchronization progress.

* For a Pay\-as\-you\-go task, you cannot modify the task configuration again before the modification officially takes effect.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, click **More operations** \> **Modify configuration** in the upper\-right corner of the target task.

5. In the **Modify configuration** dialog box, set the **Link specifications**.

6. Select the configuration method according to the billing method of the task:

   * Pay\-as\-you\-go

      Click **OK**.

   * Subscription

      1. Click OK.

      2. In the **Confirm order** configuration wizard, confirm the order information, and then click **Next**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about each link specification, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specifications</a>.</div>
