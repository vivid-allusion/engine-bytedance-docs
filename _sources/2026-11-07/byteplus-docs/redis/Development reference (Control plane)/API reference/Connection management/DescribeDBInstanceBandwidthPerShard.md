---
title: "DescribeDBInstanceBandwidthPerShard"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbinstancebandwidthpershard"
---

Call the DescribeDBInstanceBandwidthPerShard API to query the single\-shard bandwidth details of the target Redis, including default bandwidth and additional bandwidth.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceBandwidthPerShard&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xsh2xs |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DefaultBandwidthPerShard |Integer |48 |Default bandwidth for a single shard in an instance. Both read bandwidth (i.e., downstream bandwidth) and write bandwidth (i.e., upstream bandwidth) are this value. Unit: MB/s. <br><br>The default bandwidth varies depending on the instance's node specifications. For more information, refer to [Instance Specifications](https://docs.byteplus.com/en/docs/redis/product-specification). |
|AdditionalBandwidthPerShard |Integer |20 |This field is deprecated and no longer used. Disregard it. |
|AdditionalWriteBandwidthPerShard |Integer |20 |Extra write bandwidth for a single shard, which is the additional write bandwidth required beyond the default bandwidth. Unit: MB/s.<br><br>> **tip**<br><br><br>> If the value is `0`, no additional write bandwidth is configured for the current instance.<br> |
|AdditionalReadBandwidthPerShard |Integer |20 |Additional read bandwidth per shard, which is added on top of the default bandwidth. Unit: MB/s.<br><br>> **tip**<br><br><br>> When this value is `0`, it indicates that no additional read bandwidth is set for the current instance.<br> |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceBandwidthPerShard&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xsh2xs"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "DescribeDBInstanceBandwidthPerShard",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "DefaultBandwidthPerShard": 48,
        "AdditionalBandwidthPerShard": 20,
        "AdditionalWriteBandwidthPerShard": 20,
        "AdditionalReadBandwidthPerShard": 20
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
