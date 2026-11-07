---
title: "Adjusting frequency of Redis scheduled tasks"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-hz"
---

By modifying the value of the `hz` parameter, you can adjust the frequency at which Redis executes periodic tasks, thereby changing Redis's efficiency in clearing expired keys, cleaning up timed\-out connections, and reclaiming memory fragmentation.

## Redis periodic tasks and the hz parameter

To regularly check resource and service status and perform corresponding operations according to a predetermined strategy, Redis calls an internal function to execute various background tasks, for example:

* Calculating LRU information and clearing expired keys.

* Closing timed\-out client connections.

* Optimizing hash type data.

* Executing RDB or AOF persistence\-related operations.

* Updating statistics.

* Reclaiming memory fragments.

These regular tasks are essential for the normal operation of the Redis service. Their execution frequency is determined by the `hz` parameter, with a default value of 10, meaning 10 executions per second.

## Typical application scenarios

Redis actively clears expired keys by executing regular tasks. The process is as follows:

1. Randomly check 20 keys from the set of keys with expiration times.

2. Delete all expired keys detected during the check.

3. If more than 25% of the checked keys have expired, start a new round of tasks.

If there is a large number of expired keys or they increase rapidly, and Redis's active clearing frequency is low, these expired keys will consume significant memory and potentially impact Redis service performance. Adjusting the `hz` parameter to increase the clearing frequency can effectively resolve this issue.

## Parameter description and configuration suggestions

The value range for the `hz` parameter is 1 to 500. Increasing the value of the `hz` parameter increases the execution frequency of periodic tasks but also increases the CPU usage of the Redis service. The default value of 10 is generally sufficient. If your business scenario requires a very high execution frequency for certain periodic tasks, you can try adjusting the parameter value within 100. Increasing the value of `hz` to more than 100 will cause Redis to handle scheduled tasks more frequently, increasing the main thread's latency. Proceed with caution.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Batch modification of parameters**, find the `hz` parameter in the parameter list, and modify its value according to business requirements.

   You can enter the parameter name in the search bar on the right to filter.

6. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

7. In the popped\-up dialog box, confirm the modified parameters and parameter values, and click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the configuration parameters of a specified Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the configuration parameters of a specified Redis instance. |
