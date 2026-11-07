---
title: "Switching to yearly or monthly subscription"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Switching_to_yearly_or_monthly_subscription"
---

This topic describes how to change the billing method for an HBase instance from pay\-as\-you\-go to subscription.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance uses the pay\-as\-you\-go billing method.

* The instance has no unpaid orders for switching to a subscription plan.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If you upgrade an instance that has an unpaid order for switching to a subscription plan, that order will become invalid. You must first cancel the order on the orders page and then try switching to a subscription plan again.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select the target instance **Actions** column for  **...**   **\> Switch to subscription**.

4. On the **Switch to subscription** page, set the following configurations.

   
   |Parameter |Description |
   |---|---|
   |Purchase duration |Select the purchase duration for the subscription instance. |
   |Automatic renewal |Whether to enable the automatic renewal function. After checking the **Auto\-renewal on expiration** option, the system will automatically renew the instance before it expires. For more information about automatic renewal rules, see [Overview of renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules). |
   |Agreement |Read and check the terms of service. |
   

5. Click **Confirm order**.

6. On the **Confirm order** page, reconfirm the order information, and click **Next step**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the payment is complete, you can return to the <strong>Instances</strong> page to check if the <strong>Billing method</strong> for the target instance has successfully changed to <strong>Subscription</strong>. The billing method update may be delayed. We recommend waiting for a while before refreshing to confirm.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/HBase/ModifyInstanceChargeType) |Call the ModifyInstanceChargeType interface to convert the instance billing type from pay\-as\-you\-go to yearly or monthly subscription. |
