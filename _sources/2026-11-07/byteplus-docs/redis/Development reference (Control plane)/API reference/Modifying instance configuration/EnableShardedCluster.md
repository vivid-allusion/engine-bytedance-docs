---
title: "EnableShardedCluster"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/enableshardedcluster"
---

Call the EnableShardedCluster API to change an instance with sharding cluster disabled to an instance with sharding cluster enabled.

## Request type

Asynchronous request.

## Precautions

* Once instance is changed from sharding cluster disabled to sharding cluster enabled, it cannot be reversed.

* Changing the sharding cluster status from disabled to enabled only alters the architecture of the instance, with the instance type, availability zone, connection address, and other attributes remaining unchanged.

* After changing instance with sharding cluster disabled to sharding cluster enabled, the instance architecture changes, and there will be differences in limits concerning Lua script usage, multi\-key commands, transaction commands, and other commands. For more information about command limits, refer to [Command limits](https://docs.byteplus.com/en/docs/redis/command-limit).

* During the change process, the instance might prompt the error `-TRYAGAIN The specific keys are being migrated.\r\n`, or experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism.

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

* Only instances of sharding clusters that are not enabled (i.e. `0` `for ShardedCluster) need to call this API.` For more details, see [Modifying sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnableShardedCluster&serviceCode=Redis&version=2020-12-07&groupName=变更实例配置)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ApplyImmediately |Boolean |Yes |true |Whether to execute the configuration modification immediately. Valid values:<br><br><br>* `true`: Execute now.<br><br>* `false`: Execute modification within the maintenance period.<br><br><br>> **tip**<br><br><br>> For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
|ShardedCluster |Integer |Yes |1 |Whether to enable sharding cluster. Valid values:<br><br><br>* `0`: Disable.<br><br>* `1`: Enable.<br><br><br>> **tip**<br><br><br>> You can only change an instance with sharding cluster disabled to an instance with sharding cluster enabled. Therefore, the value must be `1`.<br> |
|ShardNumber |Integer |Yes |2 |Number of shards in the instance. Value range: 2 to 256. |
|ShardCapacity |Integer |No |1024 |Memory capacity of each shard, unit: MiB. Value range: 1024, 2048, 4096, 8192, 16384.<br><br>> **tip**<br><br><br><br>* > If this parameter is empty, the original single\-shard capacity will be used as the `ShardCapacity` after enabling the sharding cluster by default. However, the single\-shard capacity specifications supported by Redis instances with sharding cluster disabled and enabled are different. If a single\-shard capacity not supported by the instances with sharding cluster enabled is used, an error will occur when calling this API. For more details about Redis instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the detailed information of a specified instance, including the current number of nodes in each shard.<br><br><br>* > To reduce the number of shards, ensure that the instance's current used memory does not exceed 85% of the new total memory capacity (total capacity = single shard capacity x shard count).<br><br><br>* > Each instance specification has its corresponding supported shard capacity and bandwidth. When modifying the instance shard capacity, the instance bandwidth and type are modified as well. For more information on Redis instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br> |
|CreateBackup |Boolean |No |true |Whether to create a full backup before the change. Valid values:<br><br><br>* `true`: Create a backup.<br><br>* `false` (default value): Do not create.<br><br><br>> **tip**<br><br><br><br>* > This parameter is only effective for primary\-secondary instances (i.e., `InstanceClass` is `PrimarySecondary`). Single node instances (i.e., when `InstanceClass` is `Standalone`) do not support the backup feature, so this parameter does not need to be set.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the detailed information of the specified instance, including the instance type.<br> |
|BackupPointName |String |No |testbackup |Set the backup name for the full backup created before the change. If no backup name is set, the backup ID is used as the name by default. <br><br>If you need to set a backup name, it must meet the following conditions:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br>> This parameter takes effect only when the need to create a backup before the change is selected (that is, `CreateBackup` is `true`).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order716986589022527\*\*\*\* |Order ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=EnableShardedCluster&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ApplyImmediately": true,
        "ShardedCluster":1,
        "ShardNumber":2,
        "CreateBackup": true
}
```

## Response example

```JSON
{
        "ResponseMetadata": {
                "RequestId": "20230509153711EDF4F0D1DBEFA625xxxx",
                "Action": "EnableShardedCluster",
                "Version": "2020-12-07",
                "Service": "Redis",
                "Region": "cn-beijing"
        },
        "Result": {
                "OrderNO": "Order723108288213844****"
        }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
