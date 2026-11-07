---
title: "Canceling expired key clear task"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/cancel_expired_key_cleanup_task"
---

Cache for Redis provides an expired key management feature, supporting one\-click scanning (SCAN) of all keys and immediate deletion of expired ones. You can manually cancel expired key cleanup task at any time during its execution to avoid impacting the performance and stability of the Redis service during business peak hours or periods of resource strain.

## **Prerequisites**

The status of the task to be canceled must be **Created** or **Running**. For more details on task statuses, refer to [Expired key cleanup task status](https://docs.byteplus.com/en/docs/redis/Expired_key_management#2GwsNtg2).

## **Precautions**

After canceling expired key cleanup task, the task will be terminated immediately, and deleted expired keys cannot be recovered.

## **Procedure**

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **Expired key management** sub\-tab.

6. Under the **Expired key management** sub\-tab, find the target task, and in the **Actions** column on the right, click **Cancel**.

7. In the pop\-up dialog box, click **OK**.

## **Relevant APIs**

|API |Description |
|---|---|
|[InterruptKeyScanJob](https://docs.byteplus.com/en/docs/redis/interruptkeyscanjob) |Call the InterruptKeyScanJob API to cancel specified expired key clearup task. |
|[DescribeKeyScanJobs](https://docs.byteplus.com/en/docs/redis/describekeyscanjobs) |Call the DescribeKeyScanJobs API to query the list of key scanning tasks for the target Redis instance within the specified time period. |
