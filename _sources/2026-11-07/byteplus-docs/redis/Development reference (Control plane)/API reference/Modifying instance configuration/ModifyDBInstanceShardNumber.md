---
title: "ModifyDBInstanceShardNumber"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardnumber"
---

Call the ModifyDBInstanceShardNumber API to modify the number of shards of the target Redis instance.

## Request type

Asynchronous request.

## Limits For sharding cluster enabled instances with an applied direct connection address, the instance's shard count cannot exceed 8 during configuration changes (that is, the value of `ShardNumber` cannot be greater than `8`). If you need to increase the number of shards while direct connection is enabled, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

## Precautions

* Only instances with sharding clusters enabled (i.e., `ShardedCluster` is `1`) support modifying the number of shards. Instances for which sharding cluster is disabled (that is, `ShardedCluster` is `0`) contain only one shard and do not support modifying the number of shards. For more details, see [Modifying number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number).

* When changing the number of shards, the instance might return the `-TRYAGAIN The specific keys are being migrated.\r\n` error, or experience 1 to 2 temporary disconnections, each lasting less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism. For more details about configuration change solutions supported by different instance types, refer to [Solutions for modification of instance specifications](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You need to call the [StartContinuousBackup](https://docs.byteplus.com/en/docs/redis/startcontinuousbackup) API to enable data flashback after the configuration change is complete. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceShardNumber&serviceCode=Redis&version=2020-12-07&groupName=变更实例配置)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ApplyImmediately |Boolean |Yes |true |Whether to execute the configuration modification immediately. Valid values:<br><br><br>* `true`: Execute now.<br><br>* `false`: Execute modification within the maintenance period.<br><br><br>> **tip**<br><br><br>> For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
|ShardNumber |Integer |Yes |3 |Number of shards in the instance. Value range: 2 to 256.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the details of a specified instance, including whether sharding cluster is enabled and the number of shards.<br><br><br>* > To reduce the number of shards, ensure that the instance's current used memory does not exceed 85% of the new total memory capacity (total capacity = single shard capacity x shard count).<br> |
|CreateBackup |Boolean |No |false |Whether to create a backup before the change. Valid values:<br><br><br>* `true`: Create a backup.<br><br>* `false` (default value): Do not create.<br><br><br>> **tip**<br><br><br><br>* > This parameter is only effective for primary\-secondary instances (i.e., `InstanceClass` is `PrimarySecondary`). Single node instances (i.e., when `InstanceClass` is `Standalone`) do not support the backup feature, so this parameter does not need to be set.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the details of a specified instance, including its instance type.<br> |
|BackupPointName |String |No |testbackup |Set the backup name for the full backup created before the change. The backup name must satisfy the following conditions:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > This parameter takes effect only when the need to create a backup before the change is selected (that is, `CreateBackup` is `true`).<br><br><br>* > If no backup name is set, the backup ID is used as the name by default.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order716986992383818\*\*\*\* |Order ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceShardNumber&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs****",
	"ShardNumber": 3,
	"ApplyImmediately": true
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202211251651380102251460630500xxxx",
        "Action": "ModifyDBInstanceShardNumber",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
 "Result": {
          "OrderNO": "Order716986992383818****"
     }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
