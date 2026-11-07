---
title: "Executing failover manually"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/switch-primary-node-manually"
---

Cache for Redis supports manual failover. You can switch a specified secondary node to a primary node, or batch switch primary nodes for multiple shards in an instance. This meets the requirements for disaster recovery drills or proximate connections in multi\-zone scenarios. This topic contains instructions on how to manually execute failovers.

## Prerequisites

The instance type is the **Primary\-secondary** instance. Failover is not available in single\-node instances. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Precautions

* The node being switched may experience a temporary disconnection lasting several seconds. We recommend that you switch it during off\-peak hours and ensure that there is an automatic reconnection mechanism.

* The node being switched may have a brief (less than 30 seconds) read\-only state, which aims to avoid potential data loss risks caused by primary and secondary switchover and data double\-write due to the DNS cache.

* After manually switching the primary node, if the instance fails, the system will immediately trigger a failover to ensure the high availability of the instance. At this time, the primary node of the instance may be inconsistent with the primary node you selected during the manual switch.

## Limits

* A batch primary switchover supports up to 50 shards simultaneously.

* During a batch primary switchover, only one secondary node can be selected from per shard.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. In the **Topology** pane under the **Summary** tab, click the Server node icon ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b5723640d79ba0e002362bd6e00bf01.png) on the right of the topology chart.

5. In the Shard list below, based on your business scenario, select the nodes to switch and perform the corresponding operation.

   * **Switch for single node**

      Locate the target secondary node for the switch, then click **Switch to primary node ** in the **Actions** column on the right.

   * **Switch for multiple nodes**

      Select the target secondary nodes for the switch, then click **Batch switch to primary node** above the node list.

6. In the pop\-up dialog box, confirm the outcome of the failover and the information of the node to be switched, and click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[SwitchOver](https://docs.byteplus.com/en/docs/redis/switchover) |Call the SwitchOver API to switch roles of primary and secondary nodes of target Redis instance. |
|[DescribeDBInstanceShards](https://docs.byteplus.com/en/docs/redis/describedbinstanceshards) |Call the DescribeDBInstanceShards API to query the details of server nodes for each shard in target Redis instance. |
