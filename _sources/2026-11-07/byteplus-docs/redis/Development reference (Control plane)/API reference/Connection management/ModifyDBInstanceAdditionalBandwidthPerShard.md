---
title: "ModifyDBInstanceAdditionalBandwidthPerShard"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstanceadditionalbandwidthpershard"
---

Call the ModifyDBInstanceAdditionalBandwidthPerShard API to modify the single shard bandwidth for target Redis instance.

## Request type

Synchronous request.

## Precautions

* Only instances created after May 25, 2023 support the bandwidth modification feature. For instances created before May 25, 2023 that need to modify shard bandwidth, you must first create a new instance and use this feature on the new instance. You can migrate data from the old instance to the new instance using tools like DTS. For specific procedures, refer to [Data migration](https://docs.byteplus.com/en/docs/redis/data-migration).

* Increasing bandwidth will not affect your business. Before reducing bandwidth, monitor the current bandwidth usage to avoid triggering bandwidth throttling.

* If you perform any of the following operations after modifying bandwidth, the instance bandwidth configuration will follow these rules:

   * [Modifying sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config)

      After changing from a non\-sharding cluster to a sharding cluster, the single shard bandwidth of the instance will equal the default bandwidth corresponding to the selected node specification when enabling the sharding cluster.

   * [Restoring to new instance by backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set) or [Restoring to new instance by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point)

      When restoring to a new instance by backup set or point in time, the bandwidth configuration of the original instance will not be applied to the new instance. The new instance will use the default bandwidth corresponding to the selected node specification.

   * [Restoring deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance)

      When restoring data from a deleted instance to a new instance via backup set, the bandwidth configuration of the deleted instance will not be applied to the new instance. The new instance will use the default bandwidth corresponding to the selected node specification.

   * [Purchasing instance with same configuration](https://docs.byteplus.com/en/docs/redis/purchase-same-config-instance)

      When creating a new instance based on an existing instance configuration, the bandwidth configuration of the original instance will not be applied to the new instance. The new instance will use the default bandwidth corresponding to the selected node specification.

* If you need to change the node specification after modifying the bandwidth, you can retain additional bandwidth by checking the **Additional bandwidth** when [Modifying node specification](https://docs.byteplus.com/en/docs/redis/modify-node-spec). When retaining the additional bandwidth, the following rules will be followed:

   * Total bandwidth per shard of the instance = Default bandwidth of the changed node specification + Additional bandwidth.

   * Additional bandwidth = min[ Current additional bandwidth per shard, Maximum additional bandwidth allowed by the changed node specification ].

* Bandwidth is limited by the CPU forwarding capacity. The maximum limit of bandwidth and the maximum limit of CPU are determined by whichever reaches the bottleneck first. Therefore, it is possible that CPU utilization reaches 100% while bandwidth utilization does not reach 100%. Please reasonably plan and use the bandwidth. For more details, refer to [Efficient bandwidth usage guide](https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion).

## Billing instructions

Additional bandwidth is billed on a gradient basis, meaning that the unit price of the bandwidth will increase as the amount of additional bandwidth increases. For more details on additional bandwidth pricing, refer to [Additional bandwidth billing rules](https://docs.byteplus.com/en/docs/redis/billing-item-price).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceAdditionalBandwidthPerShard&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|AdditionalBandwidth |Integer |No |2 |Set the additional read bandwidth and additional write bandwidth for a single shard. After configuration, the additional read and write bandwidth for a single shard will both be the set value. Unit: MB/s.<br><br>> **tip**<br><br><br><br>* > `AdditionalBandwidth` is used to set the default additional bandwidth for a single shard; `AdditionalWriteBandwidth` / `AdditionalReadBandwidth` have higher priority and specify additional write/read bandwidth separately. When both are set, the bandwidth for the corresponding direction will be based on the read/write parameters, while the unset direction will still use `AdditionalBandwidth` (e.g., if only `AdditionalWriteBandwidth` is set, the read bandwidth will still take the value of `AdditionalBandwidth`). It is recommended to prioritize using `AdditionalWriteBandwidth` and `AdditionalReadBandwidth`.<br><br><br>* > If `AdditionalBandwidth`, `AdditionalWriteBandwidth`, and `AdditionalReadBandwidth` are all not passed, the API will report an error.<br> |
|AdditionalWriteBandwidth |Integer |No |2 |Specify the additional write bandwidth for a single shard, which is the additional write bandwidth required beyond the default bandwidth. Unit: MB/s.<br><br>The extra write bandwidth value must meet the following conditions:<br><br><br>* Must be greater than or equal to 0. A value of 0 means no extra write bandwidth is added, and the single\-shard bandwidth is the default write bandwidth.<br><br>* The sum of the extra write bandwidth and default bandwidth must not exceed the current instance's modifiable bandwidth limit. For more details on bandwidth limits, see [Bandwidth modification range](https://docs.byteplus.com/en/docs/redis/modify-bandwidth#.5bim5a695L-u5pS56IyD5Zu0).<br><br>* **The overall bandwidth of a Redis instance cannot exceed 2.5 GB/s**. Therefore, the upper limit of the overall bandwidth of an instance = min[(number of shards x upper limit of bandwidth for a single shard), 2.5 GB/s]. For more details, refer to [Bandwidth description](https://docs.byteplus.com/en/docs/redis/product-specification#.5bim5a696K-05piO).<br><br><br>> Description<br><br><br><br>* > `AdditionalBandwidth` is used to set the default additional bandwidth for a single shard; `AdditionalWriteBandwidth` / `AdditionalReadBandwidth` have higher priority and specify additional write/read bandwidth separately. When both are set, the bandwidth for the corresponding direction will be based on the read/write parameters, while the unset direction will still use `AdditionalBandwidth` (e.g., if only `AdditionalWriteBandwidth` is set, the read bandwidth will still take the value of `AdditionalBandwidth`). It is recommended to prioritize using `AdditionalWriteBandwidth` and `AdditionalReadBandwidth`.<br><br><br>* > If `AdditionalBandwidth`, `AdditionalWriteBandwidth`, and `AdditionalReadBandwidth` are all not passed, the API will report an error.<br> |
|AdditionalReadBandwidth |Integer |No |2 |Specify the additional read bandwidth for a single shard, which is the additional read bandwidth beyond the default bandwidth. Unit: MB/s.<br><br>The value for additional read bandwidth must meet the following conditions:<br><br><br>* Must be greater than or equal to 0; a value of 0 means no additional read bandwidth is added, and the single\-shard bandwidth will be the default read bandwidth.<br><br>* The sum of the additional read bandwidth and the default bandwidth must not exceed the maximum modifiable bandwidth limit for the current instance. For more details on bandwidth limits, see [Bandwidth modification range](https://docs.byteplus.com/en/docs/redis/modify-bandwidth#.5bim5a695L-u5pS56IyD5Zu0).<br><br>* **The overall bandwidth of a Redis instance cannot exceed 2.5 GB/s**. Therefore, the upper limit of the overall bandwidth of an instance = min[(number of shards x upper limit of bandwidth for a single shard), 2.5 GB/s]. For more details, refer to [Bandwidth description](https://docs.byteplus.com/en/docs/redis/product-specification#.5bim5a696K-05piO).<br><br><br>> Description<br><br><br><br>* > `AdditionalBandwidth` is used to set the default additional bandwidth for a single shard; `AdditionalWriteBandwidth` / `AdditionalReadBandwidth` have higher priority and specify additional write/read bandwidth separately. When both are set, the bandwidth for the corresponding direction will be based on the read/write parameters, while the unset direction will still use `AdditionalBandwidth` (e.g., if only `AdditionalWriteBandwidth` is set, the read bandwidth will still take the value of `AdditionalBandwidth`). It is recommended to prioritize using `AdditionalWriteBandwidth` and `AdditionalReadBandwidth`.<br><br><br>* > If `AdditionalBandwidth`, `AdditionalWriteBandwidth`, and `AdditionalReadBandwidth` are all not passed, the API will report an error.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order217500000099909\*\*\*\* |Order ID. |

## Example

### Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceAdditionalBandwidthPerShard&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****",
    "AdditionalWriteBandwidth": 2,
    "AdditionalReadBandwidth": 2
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202407162055504B5C0337ED26FA2B05DD-ea4af2",
        "Action": "ModifyDBInstanceAdditionalBandwidthPerShard",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderNO": "Order217500000099909****"
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
