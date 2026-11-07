---
title: "DescribeDBInstanceSlots"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/DescribeDBInstanceSlots"
---

Call the DescribeDBInstanceSlots API to query the slot allocation of each shard under the target Redis instance.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceSlots&serviceCode=Redis&version=2020-12-07&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Slots |Array of [ShardSlots](https://docs.byteplus.com/en/docs/55/105059#shardslots) |Refer to the Sample response. |Slot allocation information for each shard. |

### ShardSlots

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ShardId |Integer |0 |Shard ID. |
|Slots |Array of String |[ "0\-16383" ] |Slot distribution for this shard. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceSlots&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDBInstanceSlots",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-north-1"
    },
    "Result": {
        "Slots": [
            {
                "Slots": [
                    "0-16383"
                ],
                "ShardId": 0
            }
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
