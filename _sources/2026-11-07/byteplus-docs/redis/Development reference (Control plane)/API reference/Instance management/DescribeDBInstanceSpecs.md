---
title: "DescribeDBInstanceSpecs"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbinstancespecs"
---

Call the DescribeDBInstanceSpecs API to query the list of instance specifications supported by Redis.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceSpecs&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|ArchType |String |No |Standard |Architecture type of the Redis instance. Valid values:<br><br><br>* `Cluster`: Shard cluster is enabled (i.e., the number of shards is greater than 1).<br><br>* `Standard`: Shard cluster is not enabled (i.e., the number of shards is 1).<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the instance architecture type condition will not be used for filtering.<br><br><br>* > For more information about product architecture, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br> |
|InstanceClass |String |No |Standalone |Redis instance type. Valid values:<br><br><br>* `PrimarySecondary`: primary\-secondary instance.<br><br>* `Standalone`: single node instance.<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, no instance type condition is used for filtering.<br><br><br>* > For more details about instance types, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceSpecs |Array of [InstanceSpecInfo](https://docs.byteplus.com/en/docs/55/41939#instancespecinfo) |Refer to the Sample response. |Redis instance specification list.<br><br>> **tip**<br><br><br>> For more details about Redis instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br> |

### InstanceSpecInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ArchType |String |Standard |The architecture type of the instance. Valid values:<br><br><br>* `Cluster`: Shard cluster is enabled (i.e., the number of shards is greater than 1).<br><br>* `Standard`: Shard cluster is not enabled (i.e., the number of shards is 1). |
|InstanceClass |String |Standalone |Instance type. Valid values:<br><br><br>* `PrimarySecondary`: primary\-secondary instance.<br><br>* `Standalone`: single node instance. |
|NodeNumbers |Array of Integer |[1] |List of nodes allowed per shard. The number of nodes allowed varies for different instance types:<br><br><br>* Primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`): allow at least 2 nodes.<br><br>* Single node instances (i.e., where `InstanceClass` is `Standalone`): only allow 1 node. |
|ShardNumbers |Array of Integer |[1] |List of allowed shard numbers for the instance. The number of allowed shards varies by instance architecture type:<br><br><br>* Enable shard cluster (i.e., `ArchType` is `Cluster`): Allows at least 2 shards.<br><br>* Do not enable shard cluster (i.e., `ArchType` is `Standard`): Only allows 1 shard. |
|ShardCapacitySpecs |Array of [ShardCapacitySpecInfo](https://docs.byteplus.com/en/docs/55/41939#shardcapacityspecinfo) |Refer to the Sample response. |List of capacity specifications for a single shard. |
|MaxConnectionsPerShard |Integer |10000 |Maximum default connections per shard. |

### ShardCapacitySpecInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ShardCapacity |Integer |1024 |Memory capacity per shard. Unit: MiB. |
|DefaultBandwidthPerShard |Integer |48 |Default bandwidth of the instance at the current memory capacity Unit: MB/s. |
|MaxAdditionalBandwidthPerShard |Integer |144 |The maximum bandwidth allowed for instance modification under the current memory capacity.<br><br>> **tip**<br><br><br>> For more information on modifying bandwidth, see [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).<br> |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceSpecs&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "ArchType": "Standard",
    "InstanceClass": "Standalone"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31****",
        "Action": "DescribeDBInstanceSpecs",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceSpecs": [
            {
                "ArchType": "Cluster",
                "NodeNumbers": [
                    1
                ],
                "ShardNumbers": [
                    1
                ],
                "InstanceClass": "PrimarySecondary",
                "ShardCapacitySpecs": [
                    {
                        "ShardCapacity": 1024,
                        "DefaultBandwidthPerShard": 48,
                        "MaxAdditionalBandwidthPerShard": 144
                    }
                ],
                "MaxConnectionsPerShard": 10000
            }
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
