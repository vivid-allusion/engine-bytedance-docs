---
title: "Setting instance parameters"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-parameter"
---

Some Redis parameter values can be customized. The customizable parameters vary depending on the Redis engine version and architecture. This topic describes how to configure each parameter.

## Background information

For more details on parameters supported by Redis, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Batch modification of parameters**, find the parameter(s) that need to be modified in the parameter list, and set the new parameter value(s) according to your service needs.

   > **tip**

   * > You can choose to modify one parameter or multiple parameters simultaneously based on your business needs.

   * > To undo the last modification, click **Undo previous step** in the upper\-left corner of the parameter list. To cancel all parameter modifications for this session, click **Cancel**.

6. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

7. In the popped\-up dialog box, confirm the modified parameters and parameter values, and click **OK**.

## Subsequent operations

After successfully modifying the parameters, you can view the details of parameter modifications made under the **Parameter modification history** tab, including the name of the modified parameters, the values before and after modification, the parameter modification status, and the modification time. For specific procedures, refer to [Viewing parameter modification history](https://docs.byteplus.com/en/docs/redis/view-parameter-modification-history).

## Relevant documents

* [Adjusting frequency of Redis scheduled tasks](https://docs.byteplus.com/en/docs/redis/set-hz)

* [Limiting output buffer size for publish-subscribe client](https://docs.byteplus.com/en/docs/redis/set-client-output-buffer-pubsub)

* [Adjusting slow log parameters](https://docs.byteplus.com/en/docs/redis/adjust-slow-log-parameters)

* [Setting key eviction policy](https://docs.byteplus.com/en/docs/redis/set-maxmemory-policy)

* [Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting)

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the configuration parameters of a specified Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the configuration parameters of a specified Redis instance. |
