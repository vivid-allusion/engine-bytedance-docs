---
title: "DescribeDBInstanceShards"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbinstanceshards"
---

Call the DescribeDBInstanceShards API to query details about Server nodes in each shard of the target Redis instance.

## Request type

Synchronous request.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceShards&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|PageNumber |Integer |Yes |1 |The page number of the instance list. The value cannot exceed the maximum value of the Integer data type. The starting value is 1. |
|PageSize |Integer |Yes |10 |Number of records per page. An integer from 1 to 100. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |2 |Total number of shards in the current instance. |
|InstanceShards |Array of [InstanceShardInfo](https://docs.byteplus.com/en/docs/55/12510#instanceshardinfo) |Refer to the Sample response. |List of details for all Shard shards in the instance. |

### InstanceShardInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ShardId |String |server\-redis\-cnlf55bkfgx2s\*\*\*\*\-0 |Shard ID. |
|NodeNumber |Integer |2 |Number of nodes in the shard. |
|ServerNodes |Array of [ServerNodeInfo](https://docs.byteplus.com/en/docs/55/12510#servernodeinfo) |Refer to the Sample response. |Details list of all Server nodes in the shard. |

### ServerNodeInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|NodeId |String |server\-redis\-cnlf55bkfgx2s\*\*\*\*\-0\-0 |Node ID. |
|Status |String |running |Node status. Valid values:<br><br><br>* `deploy`: Starting.<br><br>* `running`: Running.<br><br>* `loading`: Loading data.<br><br>* `error`: error. |
|ZoneId |String |cn\-beijing\-a |The node's Availability Zone. |
|CurrentRole |String |PrimaryNode |The node's current role. Valid values:<br><br><br>* `PrimaryNode`: Primary node<br><br>* `SecondaryNode`: Secondary node |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceShards&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****",
    "PageNumber": 1,
    "PageSize": 10
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202309211602263758842C63CA00Exxxx",
        "Action": "DescribeDBInstanceShards",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceShards": [
            {
                "NodeNumber": 2,
                "ServerNodes": [
                    {
                        "CurrentRole": "PrimaryNode",
                        "NodeId": "server-redis-cn0212gzmh2xs****-0-0",
                        "Status": "running",
                        "ZoneId": "cn-beijing-a"
                    },
                    {
                        "CurrentRole": "SecondaryNode",
                        "NodeId": "server-redis-cn0212gzmh2xs****-0-1",
                        "Status": "running",
                        "ZoneId": "cn-beijing-a"
                    }
                ],
                "ShardId": "server-redis-cn0212gzmh2xs****-0"
            },
            {
                "NodeNumber": 2,
                "ServerNodes": [
                    {
                        "CurrentRole": "PrimaryNode",
                        "NodeId": "server-redis-cn0212gzmh2xs****-1-0",
                        "Status": "running",
                        "ZoneId": "cn-beijing-a"
                    },
                    {
                        "CurrentRole": "SecondaryNode",
                        "NodeId": "server-redis-cn0212gzmh2xs****-1-1",
                        "Status": "running",
                        "ZoneId": "cn-beijing-a"
                    }
                ],
                "ShardId": "server-redis-cn0212gzmh2xs****-1"
            }
        ],
        "Total": 2
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
