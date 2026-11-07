---
title: "Clearing expired key"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/clear_expired_key"
---

Cache for Redis provides an expired key management feature, supporting one\-click scanning (SCAN) of all keys and immediate deletion of expired ones to free up memory. This topic describes how to immediately clear expired keys on the console.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

After initiating an expired key scanning task, the system will automatically execute a SCAN ** ** command to scan all data. At this time, the CPU load of the instance will increase, which may affect the performance of the instance. It is recommended that you execute this task during the off\-peak period of your business.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **Expired key management** sub\-tab.

6. Under the **Expired key management** sub\-tab, click **Clear now**.

7. In the dialog box that appears, configure the following parameters, then click **OK**.

   |Parameters |Description |
   |---|---|
   |Keys scanned per second |Set the number of expired keys to scan per second. Value range: An integer between 2000 and 100000.<br><br>> **warning**<br><br><br>> The larger the parameter value, the faster the scan speed, but the higher the CPU load of the instance. Set reasonably based on the acceptable performance impact level for your business.<br> |
   |Scan timeout |Set the scan timeout duration. Value range: An integer between 30 and 1440. Unit: minute. |

## Subsequent operations

* After the expired key clear task is completed, you can view the task details in the task list under the **Expired key management** tab, including task ID, status, total shards analyzed, completed shards, task creation time, task start time, and task end time.

* After the expired key clear task is completed, the expired keys will be deleted, and the corresponding memory space will be released. You can go to the **Monitoring** page of the instance and check the **Memory usage** metric under the **Aggregated server** or **Server** node tab. Compared to before the scan task was completed, this monitoring metric will show a decrease. For the specific method to view monitoring data, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data).

* You can manually cancel expired key cleanup task at any time during its execution to avoid impacting the performance and stability of the Redis service during business peak hours or periods of resource strain. For specific procedures, refer to [Canceling expired key clear task](https://docs.byteplus.com/en/docs/redis/cancel_expired_key_cleanup_task).

## Relevant APIs

|API |Description |
|---|---|
|[CreateKeyScanJob](https://docs.byteplus.com/en/docs/redis/createkeyscanjob) |Call the CreateKeyScanJob API to create an expired key scanning task for the target Redis Instance. |
|[DescribeKeyScanJobs](https://docs.byteplus.com/en/docs/redis/describekeyscanjobs) |Call the DescribeKeyScanJobs API to query the list of key scanning tasks for the target Redis instance within the specified time period. |
