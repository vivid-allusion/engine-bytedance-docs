---
title: "Limiting output buffer size for publish-subscribe client"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-client-output-buffer-pubsub"
---

You can adjust the size of the buffer allocated by Redis for publish\-subscribe clients by customizing the value of the `client-output-buffer-pubsub` parameter. When the buffered data exceeds the limit, Redis will disconnect the publish\-subscribe client to prevent excessive memory usage and avoid impacting the performance of the Redis service.

## Output buffer limitation in Redis

Redis allocates an output buffer for each client. After processing a client's command, Redis temporarily stores the returned results in the output buffer and then sends this data to the client. If the output buffer size is not limited, the output buffer may accumulate a large amount of data, potentially reaching the maximum memory limit and causing service crashes. The following are two typical scenarios where this problem occurs:

* Exceptionally large return values generated in response to client commands.

* Publishers release messages faster than subscribers can consume them.

Properly setting the `client-output-buffer-pubsub` parameter can prevent excessive memory usage by publish\-subscribe client output buffers from negatively affecting the service.

## Parameter description and configuration suggestions

`client-output-buffer-pubsub` includes three options: `hard limit`, `soft limit`, and `soft seconds`:

* `hard limit`: It can be used to specify a hard limit, unit: MB. When a publish\-subscribe client's output buffer memory usage reaches or exceeds the `hard limit`, Redis disconnects the client.

* `soft limit`: It can be used to specify a soft limit, unit: MB. `soft seconds` specifies the duration in seconds for which the soft limit must be continuously triggered. When a publish\-subscribe client's output buffer memory usage reaches or exceeds the `soft limit` and this state persists for the number of seconds defined by `soft seconds`, Redis disconnects the client.

The default values for `hard limit`, `soft limit`, and `soft seconds` are 32 MB, 8 MB, and 60 seconds, respectively. You can customize the values for these options based on your actual business needs.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Batch modification of parameters**, find the `client-output-buffer-pubsub` parameter in the parameter list, and modify its value according to business requirements.

   You can enter the parameter name in the search bar on the right to filter.

6. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

7. In the popped\-up dialog box, confirm the modified parameters and parameter values, and click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the configuration parameters of a specified Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the configuration parameters of a specified Redis instance. |
