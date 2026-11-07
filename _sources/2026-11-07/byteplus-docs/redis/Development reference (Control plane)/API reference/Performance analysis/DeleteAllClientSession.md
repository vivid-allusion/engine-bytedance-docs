---
title: "DeleteAllClientSession"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deleteallclientsession"
---

Call the DeleteAllClientSession API to terminate all sessions in the target Redis instance.

## Request type

Synchronous request.

## Precautions

Terminating the sessions will cause the connections involved to be automatically disconnected. Please proceed with caution. For more details, please refer to [Instance sessions](https://docs.byteplus.com/en/docs/redis/instance-session).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteAllClientSession&serviceCode=Redis&version=2020-12-07&groupName=性能分析)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|IsSuccess |Boolean |true |Whether all sessions are successfully terminated. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DeleteAllClientSession&Version=2020-12-07 HTTP/1.1
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
        "RequestId": "20230604110420****10023228002****",
        "Action": "DeleteAllClientSession",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "IsSuccess": true
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
