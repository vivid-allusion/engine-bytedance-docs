---
title: "Setting read/write splitting"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-read-write-splitting"
---

To save user costs and adapt to business scenarios with more reads than writes, Cache for Redis has launched a read/write splitting mode, offering highly available, high\-performance, and flexible read/write splitting services.

## Prerequisites

The instance type is the **Primary\-secondary** instance. Single\-node instances do not support read/write splitting. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Background information

Regardless of whether sharding cluster is enabled, by default, secondary nodes in Cache for Redis only serve as backups and do not provide external services. They only handle read/write traffic after being promoted to primary nodes when a failure occurs. In this scenario, instance performance is limited by the number and performance of primary nodes. For example, even with a small data volume, a higher\-specification instance is still required when traffic or concurrency is high.

The Cache for Redis supports a bandwidth throttling mechanism. When the business traffic exceeds the Default bandwidth of the instance, bandwidth throttling will be triggered. If bandwidth throttling occurs, you can resolve it by manually adjusting the bandwidth, optimizing big/hot keys, setting up read/write splitting, or scaling up instances. For more details, refer to [Suggestions for reasonable instance bandwidth](https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion).

## Description of read/write splitting strategy and setup suggestions

### Instance\-level read/write splitting strategy

Cache for Redis supports configuring the instance's sharded read/write splitting strategy through the `read_request_distribution_strategy` parameter. The valid values are as follows:

* `read_primary_node_only` (Default): Read requests are only sent to the primary node.

* `read_secondary_nodes_only`: Read requests are randomly distributed across all secondary nodes.

* `read_primary_node_and_secondary_nodes`: Read requests are randomly distributed across the primary node and all secondary nodes.

> **tip**

> For instance deployed in multiple availability zones, if local access is enabled (that is, when the `read_local_node_only` value is `yes`), the read request distribution strategy will be jointly determined by the read/write splitting parameter and the local access parameter. For more details, refer to [Setting read local node only](https://docs.byteplus.com/en/docs/redis/read-local-node-only).

### Connection\-level read/write splitting strategy

* **Strategy description**

   Cache for Redis supports setting the read/write splitting strategy for the current connection using the `clientsetopt read_priority` command. The value range is as follows:

   > **tip**

   * > The connection\-level read/write splitting strategy only takes effect when the instance has enabled the read/write splitting strategy (that is, when the `read_request_distribution_strategy` parameter is **not** `read_primary_node_only`).

   * > The connection\-level read/write splitting strategy is only effective for the current connection. After disconnecting or re\-establishing the connection, you must reset the connection\-level read/write splitting strategy. Otherwise, the read/write splitting strategy for the new connection will inherit the instance\-level read/write splitting strategy by default.

   * `default` (Default): If a new connection does not set a connection\-level read/write splitting strategy, it inherits the instance\-level read/write splitting strategy by default.

   * `primary_preferred`: Read requests are preferentially sent to the primary node.

   * `secondary_preferred`: Read requests are preferentially sent to the secondary node. Read requests are randomly sent among all secondary nodes and are evenly distributed.

* **Usage example**

   After connecting to Redis instance via redis\-cli or other client tools, you can use the above command to set the read/write splitting strategy for the current connection. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).

   After successfully connecting to a Redis instance, you can use the following command to set the read/write splitting strategy for the current connection to prioritize sending requests to secondary nodes.

   ```BASH
   clientsetopt read_priority secondary_preferred
   ```

   After the setting is complete, you can query the read/write splitting strategy of the current connection using the `CLIENT LIST` command (which is the `read-priority` information in the returned result).

   The query result example is as follows.

   ```BASH
   id=8598 addr=172.16.***.***:53206 fd=80 name= age=622 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 tot-mem=0 argv-mem=0 events=r cmd=client auth=1 lib-name= lib-ver= read-priority=secondary-preferred
   ```

## Precautions

* After modifying the `read_request_distribution_strategy` parameter, clients may briefly encounter request failure\-related error reports. It is recommended to perform parameter modification operations during off\-peak business hours and ensure that the client is configured with the correct retry mechanism.

* Cache for Redis supports enabling AOF persistence through the `appendonly-switch` parameter. However, there is a constraint relationship between the AOF persistence function and the read/write splitting function. Among them:

   * When parameter `read_request_distribution_strategy` is set to `read_secondary_nodes_only` or `read_primary_node_and_secondary_nodes`, parameter `appendonly-switch` cannot be set to `off`.

   * When parameter `appendonly-switch` is set to `off`, parameter `read_request_distribution_strategy` cannot be set to `read_secondary_nodes_only` or `read_primary_node_and_secondary_nodes`.

   For more details about the `appendonly-switch` parameter, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).

* After enabling read/write splitting for the instance, you can also use the event monitoring feature to check for read\-only node failure demotion (`ReadOnlyNodeDrop`) events. For more details, refer to [Event monitoring](https://docs.byteplus.com/en/docs/redis/event-monitoring).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Batch modification of parameters**, find `read_request_distribution_strategy` in the parameter list, and modify the parameter value as required by your business.

   You can enter the parameter name in the search bar on the right to filter.

6. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

7. In the popped\-up dialog box, confirm the modified parameters and parameter values, and click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the configuration parameters of a specified Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the configuration parameters of a specified Redis instance. |
