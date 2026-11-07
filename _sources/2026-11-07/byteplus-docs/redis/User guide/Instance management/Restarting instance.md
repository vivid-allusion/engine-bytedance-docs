---
title: "Restarting instance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/restart-instance"
---

You can restart the Redis instance to release all connections to solve database connection or performance issues. This topic describes how to manually restart Redis instance on console.

## Precautions

* Only instance whose status is **Running** supports restart operations. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* During an instance restart, access to some services may be affected for a short period. Proceed with caution.

* Restart instances during off\-peak hours and ensure your application has an automatic reconnection mechanism.

* Single\-node instances do not support persistence or backup, and cannot guarantee data availability or service continuity. We recommend that you use them only in testing, learning, and other scenarios, and not in production environments. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

## Restart specified instance

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, find the target instance, and in the **Actions** column on the right, select  **... \> Restart instance**.

4. Select the execution time in the pop\-up dialog box, and click **OK**.

   > **tip**

   * > You can choose to either **Execute now** or **Execution during maintenance period**. For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).

   * > If the instance is a single\-node instance, you also need to read and check **Risk recognition**. Single\-node instances are not guaranteed SLAs, and this change will result in the loss of all data. Proceed with caution.

   * > When the instance status changes from **Restarting** to **Running**, it indicates that the instance is successfully restarted and the database can now provide services to external users. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Restart instances in batches

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, select the target instances to restart in batches, then click **Restart instance** in the lower left corner of the instance list.

4. Confirm the information of the instances to be restarted in the pop\-up dialog box, and click **OK**.

   > **tip**

   * > When restarting instances in batches, specifying an execution time is not supported. After clicking **OK**, the target instances restart immediately.

   * > If the selected instances include single node instance, you also need to read and check **Risk recognition**. Single\-node instances are not guaranteed SLAs, and this change will result in the loss of all data. Proceed with caution.

   * > Bulk instance restart will fail if any instances are not in the **Running** status.

## Relevant APIs

|API |Description |
|---|---|
|[RestartDBInstance](https://docs.byteplus.com/en/docs/redis/restartdbinstance) |Call the RestartDBInstance API to restart a specified Redis instance. |
