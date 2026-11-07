---
title: "Clearing data"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/clear-data"
---

This topic describes how to clear data in Redis instance on the console.

## Precautions

Disabling the `flushall` command in **parameter** configuration (that is, adding the `flushall` command to the `disabled-commands` parameter) does not affect the normal execution of the data clearing function on the Redis console and the normal invocation of the [FlushDBInstance](https://docs.byteplus.com/en/docs/redis/flushdbinstance) API. For parameter settings, refer to [Setting instance parameters](https://docs.byteplus.com/en/docs/redis/set-parameter).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, in the upper\-right corner of the page, select ... **\> Clear data**.

   > **danger**

   * > After clearing data, existing business data in the instance will be erased and cannot be recovered. Proceed with caution.

   * > We recommend manually backing up Redis instance data before clearing it. For manual backup method, refer to [Manual backup](https://docs.byteplus.com/en/docs/redis/manual-backup).

   * > A single\-node instance does not support persistence and backup features, so data cannot be recovered after being cleared. Proceed with caution. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

5. In the pop\-up dialog box, click **Clear**.

   > **tip**

   * > After clicking **Clear**, Redis immediately starts executing the `flushall async` operation. The execution duration of this operation is affected by the amount of data to be cleared.

   * > You can initially determine if the data clearing is complete by checking the **Used memory** information in the **Configuration** area of the **Summary** page.

   * > The clear data operation does not affect newly written data, meaning data written after the clear operation is initiated will not be cleared.

## Relevant APIs

|API |Description |
|---|---|
|[FlushDBInstance](https://docs.byteplus.com/en/docs/redis/flushdbinstance) |Call the FlushDBInstance API to clear all business data in a specified instance. |
