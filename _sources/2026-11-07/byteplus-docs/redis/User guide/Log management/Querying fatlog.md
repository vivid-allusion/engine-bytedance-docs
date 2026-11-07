---
title: "Querying fatlog"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/query-fat-log"
---

Cache for Redis supports logs management, allowing you to view or export fatlog details (such as query statements and statement length) within a specified time range on the console. This topic describes how to query fatlogs.

## Background information

Slow log is a commonly used tool in daily Redis operations and maintenance for troubleshooting performance issues. It records commands whose execution time exceeds a predefined threshold. However, slow log has certain limitations: some commands execute quickly and do not trigger slow log, but their response data size is enormous, consuming significant network bandwidth. For example, using the `GET` command to read a 10 MB large key, or executing commands like `KEYS *`, `ZRANGE`, or `HGETALL` that return massive amounts of data at once, can lead to an abnormal surge in network traffic despite low QPS. Such issues are difficult to pinpoint accurately using slow log alone.

To address this, Cache for Redis provides the fatlog feature, specifically designed to record commands whose response packet size exceeds a threshold. Fatlog and slow log monitor commands from different dimensions, complementing each other to help quickly identify large key access and anomalies such as network traffic surges.

## Precautions

* The fatlog threshold is fixed at 500 KB, meaning only query statements with returned result data exceeding 500 KB are recorded as fatlogs.

* You can view the details of fatlogs within the last 3 days.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, select the **Logs** tab.

5. On the **Fatlog logs** sub\-tab, you can view the details of fatlogs for the past 3 days by default, including **Node ID**, **Execution start time**, **Statement**, **Statement length (bytes)** , and **Client IP address**.

   > **tip**

   * > You can specify the query time range on the upper\-left corner of the list, or use node ID to filter out and view the relevant fatlog query results in the list.

   * > You can export fatlog query results that match the filter criteria to your local machine for management. For specific procedure, refer to [Exporting fatlog](https://docs.byteplus.com/en/docs/redis/export-fat-log).
