---
title: "RestartDBInstanceProxy"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/restartdbinstanceproxy"
---

Call the RestartDBInstanceProxy API to restart one or more proxy nodes in a specified Redis instance.

## Request type

Asynchronous request.

## Precautions

Restarting a proxy node affects existing connections. Perform this operation during off\-peak hours and make sure that your services have a reconnection mechanism. For more details, refer to [Restarting proxy node](https://docs.byteplus.com/en/docs/redis/restart-proxy-node).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=RestartDBInstanceProxy&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ProxyNodeIds |Array of String |Yes |["proxy\-redis\-cn0212gzmh2xs\*\*\*\*\-0"] |Proxy node ID. Supports passing multiple nodes simultaneously in an array.<br><br>> **tip**<br><br><br>> Call the [DescribeNodeIds](https://docs.byteplus.com/en/docs/redis/describenodeids) API to query information of all nodes in the target instance, including Proxy node IDs.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=RestartDBInstanceProxy&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs1111",
    "ProxyNodeIds": [
        "proxy-redis-cn0212gzmh2xs****-0",
        "proxy-redis-cn0212gzmh2xs****-1"
    ]
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231115180150C30D2256D19131EB1111",
        "Action": "RestartDBInstanceProxy",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
