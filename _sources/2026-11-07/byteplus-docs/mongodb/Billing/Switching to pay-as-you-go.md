---
title: "Switching to pay-as-you-go"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/switch-to-pay-as-you-go"
---

Document Database for MongoDB offers two billing methods: pay\-as\-you\-go and yearly or monthly subscription, and supports the conversion between the two billing methods. This topic introduces how to convert the billing method of a MongoDB instance from yearly or monthly subscription to pay\-as\-you\-go.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* The instance's billing method is **Subscription**, and it is not displayed as **Expired** under the billing method. For more details on instance billing methods and expiration, refer to [Billing method](https://docs.byteplus.com/en/docs/mongodb/billing-method) and [Expiration](https://docs.byteplus.com/en/docs/mongodb/arrears-and-expiration#.5Yiw5pyf6K-05piO).


<span id=".6LS555So6K-05piO"></span>
## Billing information

When switching to pay\-as\-you\-go for an instance, the system will first calculate the residual value of the instance according to the refund rules of non\-seven day unconditional unsubscription (the remaining amount will be refunded based on the payment method used). After switching, the instance will immediately be billed according to pay\-as\-you\-go. For more information on the refund rules of non\-seven day unconditional unsubscription, refer to [Non-seven-Day Refund Policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#non-seven-day-refund-rules).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After switching the billing method from subscription to pay\-as\-you\-go billing for an instance, you can restore to subscription. For specific procedures, refer to [Switching to subscription](https://docs.byteplus.com/en/docs/mongodb/switch-to-subscription). For instances in long\-term use, we recommend that you use subscription, which is more cost\-effective than pay\-as\-you\-go. Longer subscription duration enjoys more discount.

* Pay\-as\-you\-go instances incur fees by the second, with an hourly billing cycle. The system settles fees hourly (based on UTC+8 time). Ensure that you have an adequate account balance to avoid instance shutdown due to arrears.


<span id=".5Y2V5a6e5L6L6L2s5oyJ6YeP6K6h6LS5"></span>
## Switching to pay\-as\-you\-go for single instance


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, locate the target instance, then in the right\-side **Actions** column, select  **... \> Subscription to Pay\-as\-you\-go**.

5. On the **Switch to pay\-as\-you\-go** page, after confirming the information of selected instances (such as instance name, specifications, current billing method, and instance status), read and check the relevant agreements.

6. In the lower\-right corner of the page, click **Confirm order**.

7. On the **Confirm order information** page, confirm the order details, then click **Next step** to complete the payment.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the payment is completed, you can return to the instances page to view whether the target instance's <strong>Billing method</strong> has been successfully converted to <strong>Pay\-as\-you\-go</strong>.   </div>
   

<span id=".5om56YeP6L2s5oyJ6YeP6K6h6LS5"></span>
## Switching to pay\-as\-you\-go for multiple instances


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance list page, select the target instances to be switched in batch, then click **Switch to Pay\-as\-you\-go** in the lower\-left corner of the list.

5. On the **Switch to pay\-as\-you\-go** page, after confirming the information of selected instances (such as instance name, specifications, current billing method, and instance status), read and check the relevant agreements.

6. In the lower\-right corner of the page, click **Confirm order**.

7. On the **Confirm order information** page, confirm the order details, then click **Next step** to complete the payment.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the payment is completed, you can return to the instances page to view whether the target instance's <strong>Billing method</strong> has been successfully converted to <strong>Pay\-as\-you\-go</strong>.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType API to modify the billing method of the target instance. |


&nbsp;
