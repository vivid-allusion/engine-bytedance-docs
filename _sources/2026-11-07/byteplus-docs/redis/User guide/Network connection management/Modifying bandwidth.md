---
title: "Modifying bandwidth"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-bandwidth"
---

Cache for Redis instances of different specifications have varying bandwidths. When the instance default bandwidth cannot meet the peak service traffic requirements (such as time\-limited flash sales), you can easily cope with traffic peaks by increasing the read and write bandwidth of the instance separately without changing the instance specifications.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Bandwidth modification range

Cache for Redis supports different node specifications. The default bandwidths of nodes with different specifications vary, but the ranges of read and write bandwidths that can be modified are the same. Specifically:

* Maximum modifiable **write** bandwidth for Redis instances across all node specifications: 288 MB/s.

* Maximum modifiable **read** bandwidth for Redis instances across all node specifications: 512 MB/s.

> **tip**

* > The above bandwidth limits are the default limits displayed on the Redis console. If you need to increase the additional read/write bandwidth limits that can be modified, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for an application.

* > For Redis instances with sharded clusters enabled, the above bandwidth limits are the read/write bandwidth limits that can be modified for **each single shard**.

* > **The overall bandwidth of a Redis instance cannot exceed a maximum of 2.5 GB/s**. Therefore, the upper limit of the overall bandwidth of an instance = min[(number of shards x upper limit of bandwidth for a single shard), 2.5 GB/s]. For more details, refer to [Bandwidth description](https://docs.byteplus.com/en/docs/6293/72111#%25%E5%B8%A6%E5%AE%BD%E8%AF%B4%E6%98%8E).

* > The Cache for Redis supports a bandwidth throttling mechanism. When the business traffic exceeds the **Default bandwidth** of the instance, bandwidth throttling will be triggered. If bandwidth throttling occurs, you can resolve it by manually adjusting the bandwidth, optimizing big keys or hot keys, setting up read/write splitting, or scaling up instances. For more details, refer to [Suggestions for reasonable instance bandwidth](https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion).

## Precautions

* Only instances created after May 25, 2023 support the bandwidth modification feature. For instances created before May 25, 2023 that need to modify shard bandwidth, you must first create a new instance and use this feature on the new instance. You can migrate data from the old instance to the new instance using tools like DTS. For specific procedures, refer to [Data migration](https://docs.byteplus.com/en/docs/redis/data-migration).

* Increasing bandwidth will not affect your business. Before reducing bandwidth, monitor the current bandwidth usage to avoid triggering bandwidth throttling.

* If you perform any of the following operations after modifying bandwidth, the instance bandwidth configuration will follow these rules:

   * [Modifying sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config)

      After changing from a non\-sharding cluster to a sharding cluster, the single shard bandwidth of the instance will equal the default bandwidth corresponding to the selected node specification when enabling the sharding cluster.

   * [Restoring to new instance by backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set#.5oGi5aSN5Yiw5paw5a6e5L6L77yI5o6o6I2Q77yJ) or [Restoring to new instance by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point#.5oGi5aSN5Yiw5paw5a6e5L6L77yI5o6o6I2Q77yJ)

      When restoring to a new instance by backup set or point in time, the bandwidth configuration of the original instance will not be applied to the new instance. The new instance will use the default bandwidth corresponding to the selected node specification.

   * [Restoring deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance)

      When restoring data from a deleted instance to a new instance via backup set, the bandwidth configuration of the deleted instance will not be applied to the new instance. The new instance will use the default bandwidth corresponding to the selected node specification.

   * [Purchasing instance with the same configuration](https://docs.byteplus.com/en/docs/redis/purchase-same-config-instance)

      When creating a new instance based on an existing instance configuration, the bandwidth configuration of the original instance will not be applied to the new instance. The new instance will use the default bandwidth corresponding to the selected node specification.

* If you need to change the node specification after modifying the bandwidth, you can retain additional bandwidth by checking the **Additional bandwidth** when [Modifying node specification](https://docs.byteplus.com/en/docs/redis/modify-node-spec). When retaining the additional bandwidth, the following rules will be followed:

   * Total bandwidth per shard of the instance = Default bandwidth of the changed node specification + Additional bandwidth.

   * Additional bandwidth = min[ Current additional bandwidth per shard, Maximum additional bandwidth allowed by the changed node specification ].

* Bandwidth is limited by the CPU forwarding capacity. The maximum limit of bandwidth and the maximum limit of CPU are determined by whichever reaches the bottleneck first. Therefore, it is possible that CPU utilization reaches 100% while bandwidth utilization does not reach 100%. Please reasonably plan and use the bandwidth. For more details, refer to [Efficient bandwidth usage guide](https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion).

## Billing information

- [ ] Additional bandwidth is billed on a gradient basis, meaning that the unit price of the bandwidth will increase as the amount of additional bandwidth increases. For more details on additional bandwidth pricing, refer to [Additional bandwidth billing rules](https://docs.byteplus.com/en/docs/redis/billing-item-price#.6aKd5aSW5bim5a696K6h6LS56KeE5YiZ).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. On the **Summary** tab, in the **Configuration** section, click the edit icon next to **Bandwidth** to navigate to the **Modify bandwidth** page. Configure the following parameters as required.

   > **tip**

   > Hover your mouse over the value after **Bandwidth** to view the instance's current **Default bandwidth** and **Additional bandwidth** information in the pop\-up window.

   |Parameters |Required to config |Description |
   |---|---|---|
   |Instance ID/Name |No |Instance ID and name. |
   |Instance specification |No |The current specifications of the instance, including node specifications and node and shard counts. |
   |Default read bandwidth per shard |No |The default read bandwidth for each data node. Different node specifications have different default bandwidths. For more information, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification). |
   |Target read bandwidth |Yes<br><br> |Target read bandwidth: Supports direct input or step adjustment of additional bandwidth **per single shard**. The right side simultaneously displays the current instance's **default bandwidth** (not modifiable) and **additional bandwidth**. The console automatically calculates and previews the total instance bandwidth based on the number of shards. During step adjustment, the single\-shard total, total instance bandwidth, and cost are updated in real time, eliminating the need for manual conversion by shard count. |
   |Read bandwidth estimation |No<br><br> |Simultaneously display post\-expansion bandwidth from two dimensions: single\-shard read bandwidth (default + additional + total) and total instance read bandwidth. The console automatically calculates the total instance bandwidth based on the number of shards (and multiplies it by the number of readable nodes when read/write splitting is enabled), eliminating the need for manual conversion.<br><br>> **tip**<br><br><br><br>* > The estimated read bandwidth displayed here refers to the estimated total read bandwidth of the instance in non\-read/write splitting scenarios.<br><br><br>* > The instance's [read/write splitting policy](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting) and [read local node only settings](https://docs.byteplus.com/en/docs/redis/read-local-node-only) affect the number of readable nodes. Therefore if the instance is configured with read/write splitting policy or read local node only, the total write bandwidth of the instance remains unchanged, and the total read bandwidth is increased by a multiple of the number of readable nodes, so the actual total read bandwidth may be larger than the estimated bandwidth.<br><br><br>* > Different read/write splitting policies result in different calculation methods for instance's total read bandwidth, specifically:<br><br><br>   * > Disable read/write splitting: Instance total read bandwidth = Target bandwidth x Number of shards.<br><br><br>   * > Enable read/write splitting: Instance total read bandwidth = Target bandwidth x Number of shards x Number of readable nodes.<br> |
   |Default write bandwidth per shard |No |The default write bandwidth for each data node. Different node specifications have different default bandwidths. For more information, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification). |
   |Target write bandwidth<br><br> |Yes<br><br> |Target write bandwidth: supports direct input per **shard** or incremental adjustment of additional bandwidth. The right panel displays the current instance's **default bandwidth** (non\-editable) and **additional bandwidth**. The console automatically calculates and previews the total instance bandwidth based on the number of shards. When incrementally adjusting, the total per\-shard, total instance bandwidth, and costs update in real\-time, eliminating the need for manual conversion based on the number of shards. |
   |Write bandwidth estimation |No<br><br> |Simultaneously display post\-expansion bandwidth from two dimensions: single\-shard write bandwidth (default + additional + total) and total instance write bandwidth. The console automatically calculates the total instance bandwidth based on the number of shards, eliminating the need for manual conversion.<br><br>> **tip**<br><br><br><br>* > The estimated write bandwidth displayed here refers to the estimated total write bandwidth of the instance in non\-read/write splitting scenarios.<br><br><br>* > Enabling or disabling the read/write splitting strategy does not affect how the instance's total write bandwidth is calculated, that is, total write bandwidth = target bandwidth \* shard number<br> |

5. The page content is fully displayed on a single screen. Cost information is updated in real time with the configuration in a sticky footer. After confirming the configuration and costs in the sticky cost bar at the bottom, click **OK** to submit.

## Subsequent operations

* To reduce costs and save resources, you can decrease additional bandwidth after the peak in service traffic. You can monitor instance traffic usage using metrics such as **Outbound bandwidth utilization**, **Inbound bandwidth utilization**, **Network peak input rate** and **Network peak output rate**. For specific procedures, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-monitoring-data).

* If business traffic exceeds the instance's default bandwidth, leading to issues like bandwidth throttling, refer to [Suggestions for reasonable instance bandwidth](https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion) for optimization.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceAdditionalBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/modifydbinstanceadditionalbandwidthpershard) |Call the ModifyDBInstanceAdditionalBandwidthPerShard API to modify the single shard bandwidth for target Redis instance. |
|[DescribeDBInstanceBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/describedbinstancebandwidthpershard) |Call the DescribeDBInstanceBandwidthPerShard API to query the details of the bandwidth per shard of target Redis, including the default bandwidth and the additional bandwidth. |
