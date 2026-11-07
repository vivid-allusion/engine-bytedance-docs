---
title: "Switching to subscription"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/switch-to-subscription"
---

Cache for Redis offers two billing methods: pay\-as\-you\-go and yearly or monthly subscription, and supports the conversion between the two billing methods. This topic introduces how to convert the billing method of a Redis instance from pay\-as\-you\-go to yearly or monthly subscription.

## Prerequisites

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* The instance billing method is **Pay\-as\-you\-go**. For more information about instance billing methods, refer to [Billing method](https://docs.byteplus.com/en/docs/redis/billing-method).

## Precautions

* After successfully changing the billing method for an instance, the instance is immediately billed by subscription.

* After changing the billing method from pay\-as\-you\-go to subscription for an instance, you can restore it to pay\-as\-you\-go. For specific procedures, refer to [Switching to pay-as-you-go](https://docs.byteplus.com/en/docs/redis/switch-to-pay-as-you-go).

## Switching to subscription for single instance

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. Find the target instance on the **Instances** page, and in the **Actions** column on the right, select  **... \> Switch to subscription**.

4. On the **Switch to subscription** page, set the following configurations.

   |Parameters |Description |
   |---|---|
   |Subscription duration |Select the subscription duration for the instances. |
   |Automatic renewal |Whether to enable the automatic renewal function. If you check **Automatic renewal**, the system will automatically renew the instance before it expires.<br><br>For more details on automatic renewal rules, refer to [Auto-renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). |
   |Agreements |Read and check the relevant agreements. |

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order information** page, confirm the order details, then click **Next step** to complete the payment.

   > **tip**

   > After the payment is completed, you can return to the **Instances** page to view whether the target instance's **Billing method** has been successfully converted to **Subscription**.

## Switching to Subscription for multiple instances

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, select the target instances to be switched in batch, then click **Switch to Subscription** in the lower\-left corner of the list.

4. On the **Switch to subscription** page, reconfirm the selected instance information and configure the following settings.

   |Parameters |Description |
   |---|---|
   |Subscription duration |Select the subscription duration for the instances. |
   |Automatic renewal |Whether to enable the automatic renewal function. If you check **Automatic renewal**, the system will automatically renew the instance before it expires.<br><br>For more details on automatic renewal rules, refer to [Auto-renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). |
   |Agreements |Read and check the relevant agreements. |

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order information** page, confirm the order details, then click **Next step** to complete the payment.

   > **tip**

   > After the payment is completed, you can return to the **Instances** page to view whether the target instance's **Billing method** has been successfully converted to **Subscription**.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/redis/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType API to modify the billing method of the target instance. |
