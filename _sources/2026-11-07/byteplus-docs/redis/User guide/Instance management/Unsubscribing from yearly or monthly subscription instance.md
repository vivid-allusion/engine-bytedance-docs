---
title: "Unsubscribing from yearly or monthly subscription instance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/unsubscribe-instance"
---

You can unsubscribe from yearly or monthly subscription Redis instances that are no longer in use on the Redis console at any time to save resources and costs. This topic describes how to unsubscribe yearly or monthly subscription Redis instances.

## Prerequisites

The instance billing method is yearly or monthly subscription.

## Billing instructions

After unsubscribing from yearly or monthly subscription Redis instances, the refund is returned to the account balance. For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#7d1daff3).

## Precautions

* Whether you use the Redis console or the Billing center to unsubscribe from yearly or monthly subscription Redis instance, you do not need to specify a backup policy when deleting the instance. The system automatically selects the corresponding default backup policy based on the instance type, where:

* Primary\-secondary instance: A final backup will be created by default before deleting the instance, and it will be retained for 7 days after successful creation. It is recommended to download and save it locally promptly. You can view or download backups of deleted instances on the **Backups** page and restore instances based on the backups. For more details, refer to [Restoring deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance).

* Single node instance: Single node instances do not support persistence and backup functions. No backup will be created by default when deleting, and instance data will be **completely cleared** after deletion. Please proceed with caution. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

* When managing subscription Redis instances with IAM user, the following points need to be noted:

   * If an IAM user needs to perform operations such as recharging, renewing, or unsubscribing for a Redis instance, it is necessary to add the `BillingCenterFullAccess` permission to the IAM user within the **global** scope. For specific procedure to add permissions for IAM users, refer to [Managing user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).

   * If you convert the billing method of a pay\-as\-you\-go Redis instance to monthly or yearly subscription, even if the IAM user has the `BillingCenterFullAccess` permission for the instance under the corresponding project, you still need to add the `BillingCenterFullAccess` permission for the IAM user at the **global** scope. Otherwise, the IAM user will receive a permission insufficiency error when recharging, renewing, or unsubscribing from the instance. For specific procedure to add permissions for IAM users, refer to [Managing user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).

   For more information, refer to [Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).

## Unsubscribe instance via Redis console

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, find the target instance, and in the **Actions** column on the right, select  **... \> Unsubscribe instance**.

   > **tip**

   > If your **Unsubscribe instance** button is grayed out and a prompt **Instance deletion protection is turned on and cannot be unsubscribed. Click to modify** pops up, it indicates that instance deletion protection is enabled for this instance. You need to disable the deletion protection function first according to the console prompt before you can unsubscribe the instance. For specific procedures, refer to [Disable deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection#.5YWz6Zet5a6e5L6L5Yig6Zmk5L-d5oqk).

4. Confirm the warning information in the popped\-up dialog box, and enter the name of the target instance in the **Unsubscription confirmation** text box for confirmation, and click **Unsubscribe** to go to the billing platform.

5. On the **Unsubscription** page, confirm information concerning the instance that you want to unsubscribe (such as product, configuration, instance ID/name and start and end time) and amount information (such as the amount actually paid, used amount and refundable amount), and click **Confirm unsubscription**.

   > **danger**

   * > Clicking **Confirm unsubscription** will immediately apply for unsubscription (the instance will enter the **Deleting** status), and there will be no secondary confirmation pop\-up. Please operate with caution.

   * > After clicking **Confirm unsubscription**, an **Unsubscription details** dialog will automatically pop up. You can view the relevant information of the unsubscribed instance (such as instance ID/name and refund amount) in the pop\-up window. You can also click the order number (starting with **Order**) to go to the order details page.

## Unsubscribing instance via Billing center

> **tip**

> For subscription instances, even if instance deletion protection is enabled, you can still unsubscribe through the billing platform. For more details, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection).

You can unsubscribe subscription Redis instances in bulk or individually through the billing center. For specific procedures, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#7d1daff3).

## Relevant APIs

|API |Description |
|---|---|
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/redis/deletedbinstance) |Call the DeleteDBInstance API to delete a specified Redis instance. |
