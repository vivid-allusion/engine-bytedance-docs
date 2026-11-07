---
title: "ModifyDBInstanceShardCapacity"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardcapacity"
---

Call the ModifyDBInstanceShardCapacity API to modify the single shard memory of target Redis instance.

## Request type

Asynchronous request.

## Precautions

* During the process of changing the single shard memory capacity, the instance may experience up to one temporary connection disconnection, lasting within 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism. For more details about configuration change solutions supported by different instance types, refer to [Solutions for modification of instance specifications](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You need to call the [StartContinuousBackup](https://docs.byteplus.com/en/docs/redis/startcontinuousbackup) API to enable data flashback after the configuration change is complete. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceShardCapacity&serviceCode=Redis&version=2020-12-07&groupName=变更实例配置)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ApplyImmediately |Boolean |Yes |true |Whether to execute the configuration modification immediately. Valid values:<br><br><br>* `true`: Execute now.<br><br>* `false`: Execute modification within the maintenance period.<br><br><br>> **tip**<br><br><br>> For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
|ShardCapacity |Long |Yes |1024 |Memory capacity of each shard, unit: MiB. Valid values:<br><br><br>* When sharding cluster is disabled (`ShardedCluster` value is `0`): 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 24576, 65536.<br><br>* When sharding cluster is enabled (`ShardedCluster` value is `1`): 1024, 2048, 4096, 8192, 16384.<br><br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the detailed information of the specified instance, including whether sharding is enabled and the memory capacity in each shard.<br><br><br>* > To reduce the number of shards, ensure that the instance's current used memory does not exceed 85% of the new total memory capacity (total capacity = single shard capacity x shard count).<br><br><br>* > Each instance specification has its corresponding supported shard capacity and bandwidth. When modifying the instance shard capacity, the instance bandwidth and type are modified as well. For more information on Redis instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br> |
|CreateBackup |Boolean |No |false |Whether to create a backup before the change. Valid values:<br><br><br>* `true`: Create backup.<br><br>* `false` (default value): Do not create backup.<br><br><br>> **tip**<br><br><br><br>* > This parameter is only effective for primary\-secondary instances (i.e., `InstanceClass` is `PrimarySecondary`). Single node instances (i.e., when `InstanceClass` is `Standalone`) do not support the backup feature, so this parameter does not need to be set.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the detailed information of the specified instance, including the instance type.<br> |
|BackupPointName |String |No |testbackup |Set the backup name for the full backup created before the change. The backup name must satisfy the following conditions:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > This parameter is effective only when creating a backup before the change is selected (i.e., `CreateBackup` is `true`).<br><br><br>* > If no backup name is set, the backup ID is used as the name by default.<br> |
|ReserveAdditionalBandwidth |Boolean |No |false |Set whether to reserve additional bandwidth. Valid values:<br><br><br>* `true` (default): Retain additional bandwidth.<br><br>* `false`: Do not retain additional bandwidth.<br><br><br>> **tip**<br><br><br><br>* > This parameter only takes effect when additional bandwidth exists in the instance. You can call the [DescribeDBInstanceBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/describedbinstancebandwidthpershard) API to query the single\-shard bandwidth details of the target Redis, including default bandwidth and additional bandwidth.<br><br><br>* > The following rules apply when retaining additional bandwidth:<br><br><br>   * > Total bandwidth per shard of the instance = Default bandwidth of the changed node specification + Additional bandwidth.<br><br><br>   * > Additional bandwidth = min[ Current additional bandwidth per shard, Maximum additional bandwidth allowed by the changed node specification ].<br><br><br>* > For more details about additional bandwidth, refer to [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order716987014301057\*\*\*\* |Order ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceShardCapacity&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs****",
	"ShardCapacity": 16384,
	"ApplyImmediately": true
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202211251645030101742511840602xxxx",
        "Action": "ModifyDBInstanceShardCapacity",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderNO": "Order716987014301057****"
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
