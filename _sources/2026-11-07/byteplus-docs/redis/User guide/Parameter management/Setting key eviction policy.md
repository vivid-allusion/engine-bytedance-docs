---
title: "Setting key eviction policy"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-maxmemory-policy"
---

You can configure key eviction policies on the console by setting the `maxmemory-policy` parameter.

## Eviction policy

As an in\-memory database, when Redis runs out of memory, to ensure the hit rate, it evicts certain data. The available eviction policies are described as follows:

* `volatile-lru` (Default): Select the least recently used keys from the keys that have been set to expire for eviction.

* `volatile-lfu`: Select the least frequently used keys from the keys that have been set to expire for eviction.

* `volatile-random`: Select some keys randomly from the keys that have been set to expire for eviction.

* `volatile-ttl`: Select the key with the shortest Time To Live (TTL) from the keys that have been set to expire for eviction.

* `allkeys-lru`: Preferentially evict the least recently used keys.

* `allkeys-lfu`: Preferentially evict the least recently used keys.

* `allkeys-random`: Select some keys randomly to evict.

* `noeviction`: Do not evict any keys. When memory is insufficient to accommodate new data, new write operations will result in errors, and requests cannot be processed. Selecting the `noenviction` policy prevents data from being discarded.

You can select an appropriate eviction policy based on your business needs.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Batch modification of parameters**, find the `maxmemory-policy` parameter in the parameter list, and modify its value according to business requirements.

   You can enter the parameter name in the search bar on the right to filter.

6. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

7. In the popped\-up dialog box, confirm the modified parameters and parameter values, and click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the configuration parameters of a specified Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the configuration parameters of a specified Redis instance. |
