---
title: "Configuring forward synchronization"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/configuring_forward_synchronization"
---

Database Transmission Service (DTS) provides various types of database synchronization services. This topic describes how to configure data forward synchronization tasks through Database Transmission Service (DTS).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The task has been created, and the forward synchronization task status is **To be started**. For the method to create a synchronization task, refer to [Creating a synchronization task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task).

<span id="6zfKHoHY"></span>
## Precautions

If a data verification task is enabled in the synchronization task, the data verification task can be disabled by configuring the synchronization task before it starts. Once the built\-in data verification task is disabled, it will be removed from the data verification task list. After the synchronization task is started, the built\-in data verification task can not be disabled.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. In the left navigation bar, click **Data synchronization**.


4. Find the target task on the synchronization task list page and click **Configuration** in the upper\-right corner.

5. On the **Configuring source and target database** page, configure the task name, link specifications, and the configuration of source and destination instances.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the current task is a copy task, configuring link specifications is supported.   </div>
   

5. Configure the billing information for the task, you can select **Pay\-as\-you\-go** and **Subscription**.

7. In the lower\-right corner of the page, click **Next: configure synchronization object**.

8. On the **Synchronization objects** page, refer to [Overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions) for parameter configuration of different database types.

9. Click **Pre\-check**. You can perform the following operations based on the pre\-check result:

   * Click ** Details** in the **Actions ** column of the pre\-check results to view a detailed alarm or failure message. After modifying the databases and tables according to the alarm or failure message, click ** Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the synchronization task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you choose to <strong>Ignore</strong> the alert and start the synchronization Task, it may cause data inconsistencies and business risks.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql">Pre\-check items</a>.   </div>
   

10. In the lower\-right corner of the page, click **Purchase and start**.

11. Select the configuration method according to the billing method of task creation:

   * Pay\-as\-you\-go

      On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   * Subscription

      1. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

      2. On the **Confirm order information** configuration wizard page, confirm the billing information of the task.

      3. Optional. Click **Voucher redemption**. In the **Voucher redemption** dialog box, enter the voucher code and click **Redeem**.

      4. Optional. In the voucher area, select an available voucher as needed. Only one voucher can be selected at a time to offset part of the cost. You can also choose not to use a voucher.

      5. Click **Next step**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Once the <strong>Payment is completed</strong> on the configuration wizard page, a <strong>Successful payment</strong> message means your task has been created.      </div>
      

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

If you select bidirectional synchronization for the synchronous topology when creating a synchronization task, you can configure the reverse synchronization task after the forward synchronization task enters the incremental synchronization stage. Refer to [Configuring reverse synchronization](https://docs.byteplus.com/en/docs/DTS/configuring_reverse_synchronization) for the configuration method.
