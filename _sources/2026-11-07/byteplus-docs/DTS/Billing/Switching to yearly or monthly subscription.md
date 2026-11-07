---
title: "Switching to yearly or monthly subscription"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/switching_to_yearly_or_monthly_subscription"
---

This document describes how to convert a task billed by a Pay\-As\-You\-Go billing method to yearly/monthly subscription.

<span id="prerequisites"></span>
## Prerequisites


* You have created a subscription or synchronization task. The task status is "running" and subject to Pay\-As\-You\-Go billing.For more information on operations, refer to [Overview of subscription scheme](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions) and [Overview of synchronization scheme](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).

* The task should not have any uncompleted orders for converting to a yearly/monthly subscription.


<span id="precautions"></span>
## Precautions

Only data synchronization and data subscription tasks are eligible for converting from Pay\-As\-You\-Go billing to yearly/monthly subscription.

<span id="the-procedure-is-as-follows"></span>
## **The procedure is as follows:** 


1. Log in to the [DTS console](https://console.volcengine.com/dts).

2. Select the project and region in the top menu bar.

3. Select the option to convert the billing method for the task as needed.

   * To convert the billing type of a subscription task:

      1. In the navigation pane on the left, click **Data subscription**.

      2. On the **Data subscription list** page, select  **... \> Switching to yearly or monthly subscription** on the right of the target task.

   * To convert the billing type of a synchronization task:

      1. In the navigation pane on the left, click **Data synchronization**.

      2. On the **Data synchronization list** page, select  **... \> Switching to yearly or monthly subscription** on the right of the target task.

4. On the **Switching to yearly or monthly subscription** page, select **Purchase time**, read the Database Product and Service Terms, check the box **I have read and agree《Service\-Specific Terms for BytePlus Database Products and Services》** , and click **Next step：**  **Confirm the order**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can optionally select whether to enable <strong>Automatic renewal due</strong>. It is not selected by default.   </div>
   

5. On the **Confirm order configuration** wizard page, confirm the instance billing information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there are available cash coupons, click <strong>Voucher redemption</strong>. In the <strong>Voucher redemption</strong> dialog box, enter the cash coupon redemption code and click <strong>Redemption</strong> to reduce the fee to be paid.   </div>
   

6. Click **Next step**.


<span id="execution-result"></span>
### Execution result

After the conversion is complete, click **Go console**, and you can see the **Billing type** of the target task as **Yearly or monthly subscription** in the task list page.
