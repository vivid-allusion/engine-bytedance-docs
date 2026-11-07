---
title: "DescribeDBInstanceDetail"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbinstancedetail"
---

Call the DescribeDBInstanceDetail API to query details about the target Redis instance.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceDetail&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfkmh6uiii87hla |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RegionId |String |cn\-beijing |Region ID. |
|ZoneIds |Array of String |["cn\-beijing\-a"] |List of availability zone IDs. |
|ConfigureNodes |Array of [ConfigureNode](https://docs.byteplus.com/en/docs/55/12514#configurenode) |Refer to the Sample response. |List of availability zones for all nodes in the instance. |
|InstanceName |String |test |Instance name. |
|InstanceId |String |redis\-cnlfkmh6uiii87hla |Instance ID. |
|Status |String |Running |The current state of the instance.<br><br>> **tip**<br><br><br>> For more information on instance states, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).<br> |
|EngineVersion |String |5.0 |Database version of the Redis instance. |
|ShardedCluster |Integer |1 |Indicates whether the current instance has enabled sharding cluster. The value range is as follows:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|NodeNumber |Integer |2 |Number of nodes. |
|ShardNumber |Integer |2 |Number of shards in the instance. |
|ShardCapacityV2 |Long |1024 |Memory capacity of each shard in the instance. Unit: MiB. |
|Capacity |Object of [InstanceCapacity](https://docs.byteplus.com/en/docs/55/12514#instancecapacity) |Refer to the Sample response. |Instance capacity information. Unit: MiB. |
|VpcId |String |vpc\-rs5811nceqyov0x58x458x4 |ID of the Virtual Private Cloud. |
|SubnetId |String |subnet\-rrz4zdgdv20wv0x58hx58h |The subnet ID of the instance's subnet. |
|CreateTime |String |2021\-11\-09T14:02:14Z |The instance's creation time, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|VisitAddrs |Array of [VisitAddress](https://docs.byteplus.com/en/docs/55/12514#visitaddress) |Refer to the Sample response. |Connection address information. |
|MaintenanceTime |String |02:00\-02:59 |Instance maintenance period, in the format of `HH:mm-HH:mm` (UTC+8). |
|ExpiredTime |String |2021\-02\-28 23:59:59 |Instance expiration time, in the format of `yyyy-MM-dd HH:mm:ss` (UTC+8).<br><br>> **tip**<br><br><br>> Only for monthly or yearly subscription instances (that is, when `ChargeType` is `PrePaid`), this parameter will be returned.<br> |
|ProjectName |String |default |The name of the project to which the instance belongs. |
|DeletionProtection |String |enabled |The status of instance deletion protection. Valid values:<br><br><br>* `enabled`: Enabled.<br><br>* `disabled`: Disabled.<br><br><br>> **tip**<br><br><br>> For more information on deletion protection, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection).<br> |
|VpcAuthMode |String |close |Indicates whether password\-free access is enabled. Valid values:<br><br><br>* `open`: Password\-free access is enabled.<br><br>* `close`: Password\-free access is disabled.<br><br><br>> **tip**<br><br><br>> For more information on password\-free access, refer to [Password\-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).<br> |
|InstanceClass |String |PrimarySecondary |Instance type. Valid values:<br><br><br>* `PrimarySecondary`: primary\-secondary instance.<br><br>* `Standalone`: single node instance.<br><br><br>> **tip**<br><br><br>> For more information on instance type, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br> |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/55/12514#tag) |Refer to the Sample response. |Information about tags associated with the instance. |
|MultiAZ |String |disabled |Set the availability zone deployment plan for the instance. Valid values:<br><br><br>* `enabled`: Multi\-availability zone deployment plan.<br><br>* `disabled`: Single availability zone deployment plan.<br><br><br>> **tip**<br><br><br>> For more information on availability zone deployment solutions, refer to [Multi\-availability\-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution).<br> |
|ChargeType |String |PostPaid |Billing method. Valid values:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Subscription.<br><br><br>> **tip**<br><br><br>> For more information about billing types, see [Pay\-as\-you\-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go) and [Subscription](https://docs.byteplus.com/en/docs/redis/subscription).<br> |
|AutoRenew |Boolean |false |Indicates whether automatic renewal is enabled for the instance. Valid values are as follows:<br><br><br>* `false`: Automatic renewal is not enabled.<br><br>* `true`: Enable automatic renewal.<br><br><br>> **tip**<br><br><br>> Only for monthly or yearly subscription instances (that is, when `ChargeType` is `PrePaid`), this parameter will be returned.<br> |
|MaxConnections |Integer |10000 |Maximum current connections per single shard for the instance.<br><br>> **tip**<br><br><br>> The default connections per shard is 10,000, and you can adjust the maximum connections per shard via the [ModifyDBInstanceMaxConn](https://docs.byteplus.com/en/docs/redis/modifydbinstancemaxconn) API as needed.<br> |
|DataLayout |String |RAM |Instance data storage form.<br><br>> **tip**<br><br><br>> Community Edition instances (i.e., `ServiceType` is `Basic`) do not involve data storage forms, and `DataLayout` is fixed at `RAM`.<br> |
|Modules |Array of String |[<br><br>"exbloom",<br><br>"exstring",<br><br>"exts",<br><br>"valkey_json",<br><br>"valkey_search"<br><br>] |List of extension modules loaded for the instance. Values:<br><br><br>* `exbloom`: ExBloomFilter module.<br><br>* `exstring`: ExString module.<br><br>* `exts`: ExTimeSeries module.<br><br>* `valkey_json`: Valkey\-JSON module.<br><br>* `valkey_search`: Valkey\-Search module.<br><br><br>> **tip**<br><br><br>> This field is not returned if the instance does not have the extension module enabled.<br> |
|BlueGreenRole |String |Blue |Role of the instance in blue\-green deployment. Valid values:<br><br><br>* `Blue`: Blue instance.<br><br>* `Green`: Green instance.<br><br><br>> **tip**<br><br><br>> This parameter is returned only for Redis instances that have used the blue/green deployment feature. For more details, refer to [Upgrading major versions using blue\-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment).<br> |
|ShardCapacity |Double |1 |This field is reserved and will no longer be used. |

### ConfigureNode

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AZ |String |cn\-beijing\-a |The availability zone to which each node belongs. The returned information varies depending on the instance's availability zone deployment plan. Among them:<br><br><br>* When the instance is deployed in a single availability zone (i.e., `MultiAZ` is set to `disabled`), the `AZ` values of all nodes are consistent.<br><br>* When the instance is deployed in multiple availability zones (i.e., `MultiAZ` is set to `enabled`), it indicates the availability zone where each node in a single shard is located. |

### InstanceCapacity

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Used |Long |57 |Current instance used capacity. Unit: MiB. |
|Total |Long |2048 |Total memory capacity of the current instance. Unit: MiB. |

### VisitAddress

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Port |String |6379 |Port number. |
|EipId |String |eip\-2fef2qcfbfw8w5oxruw3w\*\*\*\* |The EIP ID bound to the instance's public network address.<br><br>> **tip**<br><br><br>> This parameter is returned only when the connection address type (i.e., `AddrType`) is a public network connection address (i.e., `Public`).<br> |
|Address |String |redis\-redis\-cnlfkmh6uiii8\*\*\*\*.redis.volcs.com |IP address or domain name. |
|AddrType |String |Public |Connection address type. Valid values are as follows:<br><br><br>* `Private`: Private network address.<br><br>* `Public`: Public network address.<br><br>* `DirectLink`: Direct connection address.<br><br><br>> **tip**<br><br><br>> Direct connection address information is returned only after Redis instances with sharding clusters enabled apply for a direct connection address. For more information about connection addresses, refer to [Connection address types](https://docs.byteplus.com/en/docs/redis/view-address).<br> |
|VIP |String |172.16.1.15 |The IPv4 address corresponding to the connection address. |
|VIPv6 |String |2408:4003:2027:ff0d:a86c:2529:8352:\*\*\*\* |The IPv6 address corresponding to the connection address.<br><br>> **tip**<br><br><br><br>* > This parameter is returned only when the instance uses an IPv6 address.<br><br><br>* > Only private network addresses and direct connection addresses support IPv6 addresses; public network addresses do not. Therefore, when the connection address type is a public network address (i.e., `AddrType` is `Public`), this parameter's value is always empty.<br> |

### Tag

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Key |String |department |The tag key bound to the current instance. |
|Value |String |game |The tag value of the tags associated with the current instance. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceDetail&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId":"redis-cnlfkmh6uiii87hla"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022041515423001021204401912651265",
          "Action": "DescribeDBInstanceDetail",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": {
          "Capacity": {
               "Total": 2048,
               "Used": 57
          },
          "ChargeType": "PostPaid",
          "CreateTime": "2021-11-09T14:02:14Z",
          "DeletionProtection": "enabled",
          "EngineVersion": "5.0",
          "ExpiredTime": "",
          "InstanceClass": "PrimarySecondary",
          "InstanceId": "redis-cnlfkmh6uiii87hla",
          "InstanceName": "test",
          "MaintenanceTime": "02:00-02:59",
          "MultiAZ": "disabled",
          "NodeNumber": 2,
          "ProjectName": "default",
          "RegionId": "cn-beijing",
          "ShardCapacity": 1,
          "ShardCapacityV2": 1024,
          "ShardNumber": 2,
          "ShardedCluster": 1,
          "Status": "Running",
          "SubnetId": "subnet-rrz4zdgdv20wv0x58hx58h",
          "VisitAddrs": [
               {
                   "AddrType": "Public",
                   "Address": "redis-redis-cnlfkmh6uiii8****.redis.volcs.com",
                   "EipId": "eip-2fef2qcfbfw8w5oxruw3wuw3w",
                   "Port": "6379",
                   "VIP": "172.16.1.15",
                   "VIPv6": ""
               }
          ],
          "VpcAuthMode": "close",
          "VpcId": "vpc-rs5811nceqyov0x58x458x4",
          "ZoneIds": [
               "cn-beijing-a"
          ],
          "Tags": [
            {
                "Key": "owner",
                "Value": "Alice"
            },
            {
                "Key": "department",
                "Value": "game"
            }
          ],
          "MaxConnections":10000,
          "DataLayout": "RAM",
           "BlueGreenRole": "Blue"
     }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
