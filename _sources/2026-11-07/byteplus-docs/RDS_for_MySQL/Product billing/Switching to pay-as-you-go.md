---
title: "Switching to pay-as-you-go"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_to_pay-as-you-go"
---

You can convert the billing method from yearly/monthly subscription to post paid billing for MySQL instances at any time according to your business needs.

<span id="prerequisites"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The billing method of the instance is [Yearly or monthly subscription](https://docs.byteplus.com/en/docs/RDS_for_MySQL/subscription), and the instance has not expired.

* You have read and understood [Billing Rules for Resource Subscription Change](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change).

* Your account balance is greater than or equal to 100.


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no project is set, you should select the option <strong>All resources</strong> at this step.   </div>
   

3. Go to the **Instances** page, and choose  **... \> Switch from subscription to pay\-as\-you\-go** in the **Actions** column for the target instance or check multiple target instances and choose  **... \> Switch from subscription to pay\-as\-you\-go** in the lower\-left corner of the page to perform a batch operation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A maximum of 20 instances are supported in a single batch for conversion to a yearly or monthly subscription.   </div>
   

4. Complete the following settings and click **Confirm order** on the **Switch to Pay\-as\-you\-go** page.

   1. Confirm the selected instance(s).

   2. Read and check the agreements.

5. On the **Confirm order Information** page, confirm the order information and click **Next step**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the order is submitted, the instance status changes to <strong>Billing method changing</strong> in progress. When the billing type change is complete, the instance status changes to <strong>Running</strong>.   </div>
   

<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType interface to modify the billing method of an instance. |


&nbsp;
