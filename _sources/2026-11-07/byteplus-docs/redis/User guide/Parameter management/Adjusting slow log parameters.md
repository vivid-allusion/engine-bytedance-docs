---
title: "Adjusting slow log parameters"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/adjust-slow-log-parameters"
---

The slow query log feature of Redis is used to record commands whose execution time exceeds a certain length. You can customize the values of the `slowlog-log-slower-than`, `slowlog-max-len` or `proxy-slowlog-slower-than` parameters to adjust the threshold for logging slow operations and the length of the queue to monitor and optimize query speed.

## Parameter description and configuration suggestions

Redis supports the following three slow log parameters:

* `slowlog-log-slower-than`

   Specifies the execution time threshold for requests to be recorded as slow logs on server nodes. Requests exceeding this threshold will be logged as slow queries.

   Unit: microseconds. Value range: 10000~10000000. Default value: 20000.

* `slowlog-max-len`

   Specifies the maximum number of slow query logs that the server retains. The slow log is a FIFO queue; when its length exceeds `slowlog-max-len`, the oldest slow log is deleted before new logs are added to the Server node's slow logs.

   Value range: 1~1000. Default value: 128.

* `proxy-slowlog-slower-than`

   Specifies the execution time threshold for requests to be recorded as slow logs on proxy nodes. Requests exceeding this threshold will be logged as slow queries.

   Unit: microseconds. Value range: 50000~2000000. Default value: 500000.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Batch modification of parameters**, find the slow log related parameter in the parameter list, and modify its value according to business requirements.

   You can enter the parameter name in the search bar on the right to filter.

6. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

7. In the popped\-up dialog box, confirm the modified parameters and parameter values, and click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the configuration parameters of a specified Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the configuration parameters of a specified Redis instance. |
