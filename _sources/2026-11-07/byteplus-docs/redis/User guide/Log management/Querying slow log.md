---
title: "Querying slow log"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/query-slow-log"
---

Cache for Redis supports log management, allowing you to view or export details of slow logs (such as slow query statements and execution time) within a specified time period. This topic contains instructions on how to check slow logs. This topic describes how to query slow log.

## Feature introduction

Cache for Redis records requests with the execution time exceeding the specified threshold in the slow log. You can view details of the slow logs for server nodes and proxy nodes in the Redis console. Among them:

* **Server node slow logs**

   * The **Execution time** displayed in a server node slow log only indicates the length of time that command execution lasts on the server node. The time required for communication between the server node and the proxy or client and the command queuing delay on the single\-threaded queue are not included in the execution time.

   * Cache for Redis supports customizing the slow log\-related parameters of server nodes:

      * `slowlog-log-slower-than`: Configure the execution duration threshold for slow logs. Unit: microseconds. Value range: 10000~1000000. Default value: 20000 microseconds (that is, 20 milliseconds).

      * `slowlog-max-len`: Configure the maximum number of slow log entries. Default value: 128.

* **Proxy node slow logs**

   * The **Execution time** displayed in the proxy node slow log includes not only the length of time taken by command execution on the server node, but also the communication time between the server node and the proxy or client, as well as the command queuing delay on the single\-threaded queue.

   * Blocking commands will not be recorded in slow logs, even if their execution, communication, and waiting durations exceed the threshold. Block commands include all the commands in the table below.

      |Command group |Commands |
      |---|---|
      |List |BLPOP, BRPOP, BRPOPLPUSH |
      |Sorted Set |BZPOPMIN, BZPOPMAX |
      |Stream |XREAD, XREADGROUP |

   * Cache for Redis supports customizing the slow log execution duration threshold on proxy nodes via the `proxy-slowlog-slower-than` parameter. Unit: microseconds. Value range: 50000~2000000. Default value: 500000 microseconds (that is, 500 milliseconds).

   * Cache for Redis does not limit the number of entries retained in proxy node slow logs. You can view the details of slow logs within the last 3 days.

For more information about how to set slow log parameters, refer to [Adjusting slow log parameters](https://docs.byteplus.com/en/docs/redis/adjust-slow-log-parameters).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, select the **Logs** tab.

5. On the **Slow log** sub\-tab, you can first specify the node type and query time range in the upper\-left corner of the list. Alternatively, filter the list by node ID to view the desired slow log query results.

   > **tip**

   * > By default, slow logs for all server nodes are displayed. The execution duration thresholds for requests to be recorded as slow logs vary across different nodes:

      * > Server node: Requests with an execution duration exceeding the `slowlog-log-slower-than` parameter value (default: 20 milliseconds) are recorded in the server node's slow logs.

      * > Proxy node: Requests with an execution duration exceeding the `proxy-slowlog-slower-than` parameter value (default: 500 milliseconds) are recorded in the proxy node's slow logs.

   * > You can view the details of slow logs within the last 3 days.

   * > The query results display the slow request's **Node ID**, **Execution start time**, **Execution time (μs)**, and **Statement**. The slow log list for the proxy node also displays the **Database name**, **Client IP address**, and **Accounts** details involved in the request.

   * > You can export the slow log query results that meet the filtering criteria to a local device for management. For specific procedures, refer to [Exporting slow logs](https://docs.byteplus.com/en/docs/redis/export-slow-log).

## Relevant APIs

|API |Description |
|---|---|
|[DescribeSlowLogs](https://docs.byteplus.com/en/docs/redis/describeslowlogs) |Call the DescribeSlowLogs API to view the details of slow logs of target Redis instance within specified time. |
