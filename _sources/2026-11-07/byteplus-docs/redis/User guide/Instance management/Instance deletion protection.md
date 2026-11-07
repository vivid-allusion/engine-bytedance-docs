---
title: "Instance deletion protection"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deletion-protection"
---

To prevent accidental instance deletion, Redis now supports an instance deletion protection feature. When the feature is enabled, the instance cannot be deleted. This topic describes how to enable and disable the instance deletion protection.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* For instances with yarly or monthly subscription:

   * Even after enabling instance deletion protection, you can still unsubscribe through the billing platform. For how to unsubscribe subscription instance, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#iv-unsubscription-procedure).

   * When an instance is out of service due to its expiration, the instance is deleted even if deletion protection is enabled. For more information about instance expiration, refer to [Expiration](https://docs.byteplus.com/en/docs/redis/arrear-and-expiration#bhAMBfdp).

* For pay\-as\-you\-go instances, if an instance is shut down due to account arrears, even if deletion protection is enabled, the instance will be forcibly deleted. For more information on account arrears, refer to [Arrears](https://docs.byteplus.com/en/docs/redis/arrear-and-expiration#.5qyg6LS56K-05piO).

## Enable instance deletion protection

You can enable instance deletion protection using any of the following methods:

* **Method 1**

   When creating instance, directly enable deletion protection. For specific procedure, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* **Method 2**

   1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

   2. In the top menu bar, select the project and region to which the instance belongs.

   3. On the **Instances** page, click the target instance.

   4. In the **Basic information** section under the **Summary** tab, click **Enable deletion protection** after the **Deletion protection**.

   5. In the pop\-up dialog box, click **OK**.

## Disable instance deletion protection

You can disable instance deletion protection using any of the following methods:

* **Method 1**

   1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

   2. In the top menu bar, select the project and region to which the instance belongs.

   3. On the **Instances** page, find the target instance, and in the **Actions** column on the right, select  **...**  \> **Delete instance**, and in the pop\-up prompt box where instance deletion protection is enabled, click **Click to modify**.

   4. In the pop\-up dialog box, click **OK**.

* **Method 2**

   1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

   2. In the top menu bar, select the project and region to which the instance belongs.

   3. On the **Instances** page, click the target instance.

   4. In the **Basic information** section under the **Summary** tab, click **Disable deletion protection** after the **Deletion protection**.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/redis/modifydbinstancedeletionprotectionpolicy) |Call the ModifyDBInstanceDeletionProtectionPolicy API to enable or disable the instance deletion protection. |
