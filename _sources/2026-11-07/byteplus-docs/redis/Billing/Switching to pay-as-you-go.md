---
title: "Switching to pay-as-you-go"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/switch-to-pay-as-you-go"
---

Cache for Redis offers two billing methods: pay\-as\-you\-go and yearly or monthly subscription, and supports the conversion between the two billing methods. This topic introduces how to convert the billing method of a Redis instance from yearly or monthly subscription to pay\-as\-you\-go.

## Prerequisites

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* Instance billing method is **Subscription**. For more information about instance billing methods, refer to [Billing method](https://docs.byteplus.com/en/docs/redis/billing-method).

## Billing information

When switching to pay\-as\-you\-go for an instance, the system will first calculate the residual value of the instance according to the refund rules of non\-seven day unconditional unsubscription (the remaining amount will be refunded based on the payment method used). After switching, the instance will immediately be billed according to pay\-as\-you\-go. For more information on the refund rules of non\-seven day unconditional unsubscription, refer to [Non-seven-Day Refund Policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#non-seven-day-refund-rules).

## Precautions

* After switching the billing method from subscription to pay\-as\-you\-go billing for an instance, you can restore to subscription. For specific procedures, refer to [Switching to subscription](https://docs.byteplus.com/en/docs/redis/switch-to-subscription). For instances in long\-term use, we recommend that you use subscription, which is more cost\-effective than pay\-as\-you\-go. Longer subscription duration enjoys more discount.

* Pay\-as\-you\-go instances incur fees by the second, with an hourly billing cycle. The system settles fees hourly (based on UTC+8 time). Ensure that you have an adequate account balance to avoid instance shutdown due to arrears.

## Switching to pay\-as\-you\-go for single instance

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. Find the target instance on **Instances** page, and in the **Actions** column on the right, select  **... \> Switch to pay\-as\-you\-go**.

4. On the **Switch to pay\-as\-you\-go** page, after confirming the information of selected instance (such as instance name, specification, current billing method, instance status), then read and check the relevant agreements.

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order information** page, confirm the order details, then click **Next step** to complete the payment.

   > **tip**

   > After the payment is completed, you can return to the **Instances** page to view whether the target instance's **Billing method** has been successfully converted to **Pay\-as\-you\-go**.

## Switching to pay\-as\-you\-go for multiple instances

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, select the target instances to be switched in batch, then click **Switch to Pay\-as\-you\-go** in the lower\-left corner of the list.

4. On the **Switch to pay\-as\-you\-go** page, after confirming the information of selected instance (such as instance name, specification, current billing method, instance status), then read and check the relevant agreements.

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order information** page, confirm the order details, then click **Next step** to complete the payment.

   > **tip**

   > After the payment is completed, you can return to the **Instances** page to view whether the target instance's **Billing method** has been successfully converted to **Pay\-as\-you\-go**.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/redis/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType API to modify the billing method of the target instance. |
