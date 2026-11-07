---
title: "ModifyDBInstanceMaxConn"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstancemaxconn"
---

Call the ModifyDBInstanceMaxConn API to modify the maximum number of connections per shard of the specified Redis instance.

## Request type

Asynchronous request.

## Precautions

* Increasing the maximum number of connections has no impact on your business.

* The default number of connections for each Redis single shard in all specifications is 10,000, and **the maximum number of connections for the entire instance cannot exceed 1,000,000**. Therefore, if you need to increase the number of connections, ensure that the upper limit of the overall number of connections of an instance = min[(number of shards × maximum number of connections of a single shard), 1,000,000]. For more details, refer to [Connection number description](https://docs.byteplus.com/en/docs/redis/product-specification).

* If you need to reduce the maximum number of connections, you must ensure that the number of existing connections does not exceed the modified maximum number of connections. Otherwise, it will cause the existing connections to be disconnected and also prevent new connections from being established. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-max-conn-number).

* After the maximum number of connections is reached, the system will refuse to create new connections.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceMaxConn&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|MaxConnections |Integer |Yes |20000 |The maximum number of connections per shard after modifying. Value range: 10,000\-50,000 with a step size of 1,000. <br><br>> **tip**<br><br><br>> If you need to reduce the maximum number of connections, you must ensure that the number of existing connections does not exceed the modified maximum number of connections. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-max-conn-number).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceMaxConn&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs1111",
    "MaxConnections": 20000
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240722143347B9E4EDCEF3EEE88A****",
        "Action": "ModifyDBInstanceMaxConn",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
