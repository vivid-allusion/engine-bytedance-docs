---
title: "DescribeNodeIds"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describenodeids"
---

Call the DescribeNodeIds API to query the list of all Proxy and Server node IDs in the target Redis instance.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNodeIds&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|NodeIds |Array of String |[<br><br>"server\-redis\-cn02sg5o56sbs\*\*\*\*\-0\-0",<br><br>"server\-redis\-cn02sg5o56sbs\*\*\*\*\-0\-1",<br><br>"proxy\-redis\-cn02sg5o56sbs\*\*\*\*\-0",<br><br>"proxy\-redis\-cn02sg5o56sbs\*\*\*\*\-1"<br><br>] |Node ID list. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeNodeIds&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId":"redis-cn0212gzmh2xs****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022072614403501017424420200ABxxxx",
        "Action": "DescribeNodeIds",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "NodeIds": [
            "server-redis-cn02sg5o56sbs****-0-0",
            "server-redis-cn02sg5o56sbs****-0-1",
            "proxy-redis-cn02sg5o56sbs****-0",
            "proxy-redis-cn02sg5o56sbs****-1"
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
