---
title: "Hot key analysis"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/hot-key-analysis"
---

Cache for Redis supports performance analysis, allowing you to view the details of big keys and hot keys in the database in real time while using Redis. It also supports viewing historical details of big keys and hot keys. This topic describes how to use the hot key analysis feature.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **Hot key analysis** sub\-tab.

6. On the **Hot key analysis** sub\-tab, you can view real\-time or historical hot key details in the current Redis instance, including the specific key name, data type, access count, request type (read or write), the key's shard ID, node ID, collection time, and database name.

   > **tip**

   * > By default, it shows the details of the top 50 keys with the most accesses among all data types of keys in all shards under the current Redis instance within the last 1 hour.

   * > You can select the required data types from the **Data type** drop\-down box to filter the results displayed. The supported data types are: String, List, Set, Zset and Hash.

   * > You can click  icon in the **Shard ID** column and then select to view the details of hot keys of a specified shard. A maximum of 40 shard IDs can be selected at a time.![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64d3d8547df5760a41a50d1a2f6b6f49.png)

   * > If you choose to view the details of hot keys in **Real time**, the system will refresh the real\-time hot key query results every 5 seconds by default. You can modify the automatic refresh time in the upper\-right corner of the list. Time range: 5 seconds to 1 minute. You may also directly disable **Auto refresh**.

   * > You can view the most recent historical hot key details for up to last 15 days.

   * > You can set the query result cache feature under the **Hot****key****Analysis** tab. For specific procedures, refer to [Setting query result cache](https://docs.byteplus.com/en/docs/redis/set_query_result_cache).

## Relevant APIs

|API |Description |
|---|---|
|[DescribeHotKeys](https://docs.byteplus.com/en/docs/redis/describehotkeys) |Call the DescribeHotKeys interface to query the details of hot keys for the target Redis instance within the specified time period. |
