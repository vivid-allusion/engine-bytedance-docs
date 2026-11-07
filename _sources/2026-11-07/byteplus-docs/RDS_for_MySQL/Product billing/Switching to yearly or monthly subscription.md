---
title: "Switching to yearly or monthly subscription"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_to_yearly_or_monthly_subscription"
---

You can convert the billing method from post paid billing to yearly/monthly subscription for MySQL instances at any time according to your business needs.

<span id="prerequisites"></span>
## Prerequisites


* The instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The billing method of the instance is [Pay-as-you-go](https://docs.byteplus.com/en/docs/RDS_for_MySQL/pay-as-you-go).

   The instance cannot have unpaid orders for conversion to yearly/monthly subscription.

* Your account balance is sufficient to cover the order amount for the current instance specification at the target purchase duration.


<span id="precautions"></span>
## Precautions

If there is an unpaid order for conversion to yearly/monthly subscription for an instance, this order becomes invalid when you upgrade the instance specification. You must invalidate it on the order page, and then perform the conversion to the yearly/monthly subscription mode again.

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no project is set, you should select the option <strong>All resources</strong> at this step.   </div>
   

3. Go to the **Instances** page, and choose  **... \> Switch to Subscription** in the **Actiosn** column for the target instance or check multiple target instances and choose  **… \> Switch to Subscription** in the lower\-left corner of the page to perform a batch operation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A maximum of 20 instances are supported in a single batch for conversion to a yearly or monthly subscription.   </div>
   

4. Complete the following settings and click **Confirm order** on the **Switch to subscription** page.

   * Select the **Subscription duration**.

   * Decide whether you need **Automatic renewal**.

   * Read and check the agreements.

5. On the **Confirm order information** page, confirm the order information and click **Next step**.

6. On the **Submit payment information** page, confirm the payment details and select the payment method, click **Pay**, and complete payment according to the prompts to complete instance creation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the order is submitted, the instance status changes to <strong>Billing method changing</strong> in progress. When the billing type change is complete, the instance status changes to <strong>Running</strong>.   </div>
   

<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType interface to modify the billing method of an instance. |


&nbsp;
