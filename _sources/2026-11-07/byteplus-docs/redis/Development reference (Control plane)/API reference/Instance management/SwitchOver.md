---
title: "SwitchOver"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/switchover"
---

Call the SwitchOver API to perform primary\-secondary node switchover for a specified instance.

## Request type

Asynchronous request.

## Limits Only primary\-secondary instances (that is, where `InstanceClass` is set to `PrimarySecondary`) support calling this API; single node instances (that is, where `InstanceClass` is set to `Standalone`) do not. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Precautions

* The node being switched may experience a temporary disconnection lasting several seconds. We recommend that you switch it during off\-peak hours and ensure that there is an automatic reconnection mechanism.

* The node being switched becomes temporarily read\-only for a short period of time (within 30 seconds) to avoid potential data loss caused by primary\-secondary switchover and dual writes caused by DNS cache.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=SwitchOver&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br><br>* > Only primary\-secondary instance (i.e., where `InstanceClass` is `PrimarySecondary`) supports calling this API. Single node instance (i.e., where `InstanceClass` is `Standalone`) always contains one node and does not support primary\-secondary node switchover.<br><br><br>* > Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query basic information about all Redis instances in the target region, including their instance IDs.<br> |
|TargetPrimaryNodeIds |Array of String |No |["server\-redis\-redis\-cn0212gzmh2xs\*\*\*\*\-0\-1"] |List of secondary node IDs for batch primary\-secondary switchover.<br><br>> **tip**<br><br><br><br>* > A batch primary switchover supports up to 50 shards simultaneously.<br><br><br>* > During a batch primary switchover, only one secondary node can be selected from per shard.<br><br><br>* > `TargetPrimaryNodeIds` and `TargetPrimaryNodeId` cannot both be empty; if both parameters are set, priority will be given to the parameter value set by `TargetPrimaryNodeIds`.<br><br><br>* > The current role of the input node must be a secondary node (i.e., `CurrentRole` is `SecondaryNode`).<br><br><br>* > You can call the [DescribeDBInstanceShards](https://docs.byteplus.com/en/docs/redis/describedbinstanceshards) API to query the details of server nodes for each shard in the target Redis instance, including node ID and node role.<br> |
|TargetPrimaryNodeId |String |No |server\-redis\-cn0212gzmh2xs\*\*\*\*\-0\-1 |The ID of the Secondary node for which a primary\-secondary switchover is required.<br><br>> **tip**<br><br><br><br>* > `TargetPrimaryNodeIds` and `TargetPrimaryNodeId` cannot both be empty; if both parameters are set, priority will be given to the parameter value set by `TargetPrimaryNodeIds`.<br><br><br>* > The current role of the input node must be a secondary node (i.e., `CurrentRole` is `SecondaryNode`).<br><br><br>* > You can call the [DescribeDBInstanceShards](https://docs.byteplus.com/en/docs/redis/describedbinstanceshards) API to query the details of server nodes for each shard in the target Redis instance, including node ID and node role.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=SwitchOver&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****",
    "TargetPrimaryNodeIds": [
        "server-redis-cn0212gzmh2xs****-0-1"
    ]
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230915202143DA8DBA604CA9E91C****",
        "Action": "SwitchOver",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
