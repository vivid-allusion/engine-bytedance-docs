---
title: "Purchasing instance with same configuration"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/purchase-same-config-instance"
---

You can purchase instances with the same configuration as the source instance on the Redis console, eliminating the need to manually select the same configuration when creating new instances, helping you create instances quickly. This topic describes the relevant procedures.

## Precautions

When creating a new instance based on the configurations of an existing instance, some configurations cannot be applied to the new instance. Among them:

* **Configurations that can be applied to new instances include**: Database version, instance type, number of shards, number of nodes per shard, node specifications, availability zone, billing type, port number, associated project, and allowlist groups.

* **Configurations that cannot be applied to new instances include**: instance name, account and password, delete protection configuration, tags, parameter configuration, and SSL configuration.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, find the target instance, and in the **Actions** column on the right, select  **... \> Buy same instance**.

4. On the **Create instance** page, you can directly use the source instance's configuration or modify it as needed. For more details on the instance configurations supported by Redis, refer to [Instance configuration parameter table](https://docs.byteplus.com/en/docs/redis/create-instance#.5pON5L2c5q2l6aqk).

5. After selecting the number of instances to purchase at the lower\-left corner of the page, click **Confirm order** at the lower\-right corner.

   > Description

   > Purchase at least 1 instance and up to 10 instances simultaneously.

6. Complete the subsequent steps according to the billing type you selected.

   |Billing method |Procedure |
   |---|---|
   |Pay\-as\-you\-go |On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Buy now**. |
   |Subscription |1. On the **Confirm order** page, confirm the order details, read and check the service terms, and then click **Submit order**.<br><br>2. On the **Confirm order information** page, confirm the order details again and then click **Next step**.<br><br>3. On the **Submit payment information** page, confirm the payment details and select the payment method, and then click **Go to pay**.<br><br>   > **tip**<br>   <br><br>   * > If you have submitted an order to create an instance but have not completed the payment or the payment has failed, the instance will enter the **Waiting for payment** status. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).<br>   <br><br>   * > The successfully created instance order waiting for payment will be retained for 24 hours. It is recommended to complete the payment in a timely manner, otherwise the order will be automatically cancelled and you will need to recreate the instance order.<br>   <br><br>   * > You can choose any of the following methods to complete the payment:<br>   <br><br>      * > On the instance list page of the [Redis console](https://console.byteplus.com/db/redis), find the target instance in the **Waiting for payment** status. In the **Actions** column on the right side of the instance, click **Go to pay** to jump to the **Submit payment information** page of the instance, and you need to complete the payment according to the prompts on the page.<br>   <br><br>      * > Go to [Billing center \> Order](https://console.byteplus.com/finance/order/) page, find the corresponding **Waiting for payment** order and complete the payment according to the prompts on the page.<br>    |

   > Description

   * > It takes about a few minutes to create an instance. You can view the newly created instance in the instance list.

   * > You can go to **Tasks** to view the corresponding task of the newly created instance (the **Task name/ID** is `CreateInstanceInner`), and check the stage and progress details of the current task. For specific procedures, refer to [Task management](https://docs.byteplus.com/en/docs/redis/task-management).

   * > Before the **Task status** of a newly created instance enters **Task success 100%**, do not perform any read or write operations on the new instance. Otherwise, it may lead to instance recovery failure or data not meeting expectations after recovery.
