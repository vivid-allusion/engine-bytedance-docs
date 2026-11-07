---
title: "TestShutDownDBInstanceNodes"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/testshutdowndbinstancenodes"
---

Call the TestShutDownDBInstanceNodes API to simulate a specified Server or Proxy node failover for the target Redis instance.

## Request type

Asynchronous request.

## Limits Only Redis instances of the primary\-secondary type (that is, (that is, in the response of the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API, the `InstanceClass` returns `PrimarySecondary` ) support calling this API. For more details about the instance type, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

## Precautions

* The node being switched has a temporary disconnection of a few seconds.

* The node being switched may be not writable briefly (less than 30 seconds), which aims to avoid potential data loss risks caused by failover and data double\-write caused by the DNS cache.

* Pub/Sub does not support data persistence, and there may be a risk of data loss for data in the subscription buffer during failover.

* The application needs to have an automatic reconnection mechanism and the ability to handle exceptions, otherwise the application will prompt an exception message during the instance's leader/follower switch, such as `READONLY You can't write against a read only replica`.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=TestShutDownDBInstanceNodes&serviceCode=Redis&version=2020-12-07&groupName=故障演练)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfkmh6uiii87hla |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ServerShardIds |Array of String |No |["server\-redis\-cnlfkmh6uiii8\*\*\*\*\-0"] |The shard ID of the server primary node where the simulated fault occurs.<br><br>> **tip**<br><br><br><br>* > Call the [DescribeDBInstanceShards](https://docs.byteplus.com/en/docs/redis/describedbinstanceshards) API to query the details of each shard, including the Shard ID, for the target Redis instance.<br><br><br>* > If this parameter is left blank, it means no failover will be simulated for any server primary node in the instance.<br> |
|ProxyNodeIds |Array of String |No |["proxy\-redis\-cnlfkmh6uiii8\*\*\*\*\-0"] |The proxy node ID where a fault is simulated. Supports passing in multiple nodes simultaneously, separated by English commas (,).<br><br>> **tip**<br><br><br><br>* > Call the [DescribeNodeIds](https://docs.byteplus.com/en/docs/redis/describenodeids) API to query information of all nodes in the target instance, including Proxy node IDs.<br><br><br>* > If this parameter is left blank, it indicates that no failover is simulated for any proxy nodes in the Instance.<br> |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=TestShutDownDBInstanceNodes&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cnlfkmh6uiii87hla",
    "ServerShardIds": [
        "server-redis-cnlfkmh6uiii8****-0"
    ],
    "ProxyNodeIds": [
        "proxy-redis-cnlfkmh6uiii8****-0"
    ]
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TestShutDownDBInstanceNodes",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
