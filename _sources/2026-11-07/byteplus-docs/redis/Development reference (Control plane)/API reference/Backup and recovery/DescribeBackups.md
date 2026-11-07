---
title: "DescribeBackups"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describebackups"
---

Call the DescribeBackups API to query the backup set list of the target Redis instance.

## Request type

Synchronous request.

## Precautions

Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) do not support backup and recovery operations and cannot call this API. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBackups&serviceCode=Redis&version=2020-12-07&groupName=备份恢复)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Scope |String |No |AccountInstances |Backup query range. Valid values:<br><br><br>* `OneInstance` (default value): Queries backups within a single instance.<br><br>* `AccountInstances`: Query backups for the current account. |
|InstanceId |String |No |redis\-cn0212gzmh2xsh2xs |Instance ID.<br><br>> **tip**<br><br><br><br>* > This parameter is required when the backup query scope is a single instance (i.e., `Scope` is `OneInstance`).<br><br><br>* > You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br><br><br>* > If this parameter is left blank, backup ID filtering is not applied.<br> |
|StartTime |String |No |2024\-08\-22T07:51:09Z |Query start time. Format is `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > If this parameter is set, the query end time (i.e., `EndTime`) parameter is also required.<br><br><br>* > If this parameter is left blank, time range filtering is not used.<br> |
|EndTime |String |No |2024\-08\-22T07:51:12Z |Query end time. Format is `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > If the query start time (i.e., `StartTime`) is set, this parameter is required.<br><br><br>* > The query end time must be later than the start time.<br><br><br>* > If this parameter is left blank, time range filtering is not used.<br> |
|BackupStrategyList |Array of String |No |[<br><br>"AutomatedBackup",<br><br>"ManualBackup"<br><br>] |List of backup methods. Valid values:<br><br><br>* `ManualBackup`: Manual backup.<br><br>* `AutomatedBackup`: Automatic backup.<br><br><br>> **tip**<br><br><br><br>* > Supports passing multiple backup methods simultaneously, separated by English commas (,).<br><br><br>* > If this parameter is left empty, backup methods will not be used for filtering.<br> |
|BackupPointName |String |No |testbackup |Backup name, supports fuzzy queries.<br><br>> **tip**<br><br><br><br>* > This parameter does not take effect when the backup query scope is a single instance (i.e., `Scope` is `OneInstance`).<br><br><br>* > If this parameter is left blank, no backup name filtering is applied.<br> |
|ProjectName |String |No |default |The project name that the backup file belongs to.<br><br>> **tip**<br><br><br><br>* > This parameter takes effect only when the query scope is the current account (i.e., `Scope` is set to `AccountInstances`).<br><br><br>* > If this parameter is left blank, filtering by project name is not used.<br> |
|PageSize |Integer |No |10 |Number of records per page. An integer with a value between 1 and 1000.<br><br>> **tip**<br><br><br><br>* > If the page number (`PageNumber`) is set, this parameter is required.<br><br><br>* > If this parameter is left blank, it means no per\-page record filter will be used.<br> |
|PageNumber |Integer |No |1 |The page number for the backup set information list. The value cannot exceed the maximum value of the Integer data type. The starting value is 1.<br><br>> **tip**<br><br><br><br>* > If this parameter is set, the number of records per page (i.e., `PageSize`) is also required.<br><br><br>* > If this parameter is left blank, page number range filtering is not applied.<br> |
|BackupPointId |String |No |b\-cn02xmmrp751i9cdzcphjmk4jmk4 |The backup ID of the backup file. Supports fuzzy search.<br><br>> **tip**<br><br><br><br>* > This parameter takes effect only when the query scope is the current account (i.e., `Scope` is set to `AccountInstances`).<br><br><br>* > If this parameter is left blank, backup ID filtering is not applied.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |The total number of backup files that meet the query criteria. |
|Backups |Array of [BackupInfo](https://docs.byteplus.com/en/docs/55/12500#backupinfo) |Refer to the Sample response. |Details of backup file information. |

### BackupInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BackupPointId |String |b\-cn02xmmrp751i9cdzcphjmk4\*\*\*\* |Backup ID. |
|BackupPointName |String |testbackup |Backup name. |
|BackupProgress |Integer |100 |Current completion progress for the backup. The unit is percentage. |
|BackupStrategy |String |ManualBackup |Backup method, values:<br><br><br>* `ManualBackup`: Manual backup.<br><br>* `AutomatedBackup`: Automatic backup. |
|BackupType |String |Full |Backup type. Currently, only `Full` is supported, which is a full backup. |
|StartTime |String |2024\-08\-22T07:51:09Z |Backup start time, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|EndTime |String |2024\-08\-22T07:51:12Z |Backup end time, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|InstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|InstanceInfo |Object of [DBInstance](https://docs.byteplus.com/en/docs/55/12500#dbinstance) |Refer to the Sample response. |Instance information list.<br><br>> **tip**<br><br><br>> If an instance's configuration is partially modified after a backup file is generated (e.g., by changing the billing type, renewing the instance, or upgrading instance specifications), the instance's latest information may be inconsistent with the instance information in the backup file.<br> |
|ProjectName |String |default |The project that the backup file belongs to. |
|Size |Long |486040 |Backup size. Unit: MiB. |
|Status |String |Available |Backup status. Valid values:<br><br><br>* `Creating`: The backup is being created.<br><br>* `Available`: The backup is available.<br><br>* `Unavailable`: The backup is unavailable.<br><br>* `Deleting`: The backup is being deleted.<br><br><br>> **tip**<br><br><br>> For more information on backup status, see [Backup status](https://docs.byteplus.com/en/docs/redis/view-backup#.5aSH5Lu954q25oCB).<br> |
|TTL |Integer |7 |Number of days for backup retention; defaults to 7 days. |

### DBInstance

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AccountId |Long |2100000311 |The account ID of the instance. |
|ArchType |String |Cluster |The architecture type of the instance. Valid values:<br><br><br>* `Standard`: Sharding cluster is not enabled (i.e., number of shards is 1).<br><br>* `Cluster`: Sharding cluster is enabled (i.e., number of shards is greater than 1).<br><br><br>> **tip**<br><br><br>> For more information about product architecture, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br> |
|ChargeType |String |PrePaid |Instance billing type. Valid values are as follows:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Subscription.<br><br><br>> **tip**<br><br><br>> For more information about billing types, see [Pay\-as\-you\-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go) and [Subscription](https://docs.byteplus.com/en/docs/redis/subscription).<br> |
|DeletionProtection |String |enabled |The status of instance deletion protection. Valid values:<br><br><br>* `enabled`: Enable.<br><br>* `disabled`: Disable.<br><br><br>> **tip**<br><br><br>> For more details, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection).<br> |
|EngineVersion |String |5.0 |Database version of the instance. |
|ExpiredTime |String |2024\-09\-01 23:59:59 |Instance expiration time, in the format of `yyyy-MM-dd HH:mm:ss` (UTC+8).<br><br>> **tip**<br><br><br>> Only for monthly or yearly subscription instances (that is, when `ChargeType` is `PrePaid`), this parameter will be returned.<br> |
|InstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|InstanceName |String |test |Instance name. |
|RegionId |String |cn\-beijing |The region ID of the instance's region. |
|ShardCapacity |Double |1024 |The memory capacity of each shard. Unit: MiB. |
|ShardNumber |Integer |2 |Number of shards in the instance. |
|VpcId |String |vpc\-rs5811nceqyov0x58x4\*\*\*\* |The instance's Virtual Private Cloud ID. |
|ZoneIds |Array of String |["cn\-beijing\-a"] |List of availability zones where the instance resides. |
|MaintenanceTime |String |02:00\-02:59 |Instance's maintenance period, in the format of `HH:mm-HH:mm` (UTC+8).<br><br>> **tip**<br><br><br>> For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
|NetworkType |String |VPC |The instance network type. Currently, only Virtual Private Cloud (VPC) type is supported. |
|Replicas |Integer |2 |Number of nodes per shard. |
|TotalCapacity |Long |2048 |Instance total capacity. Unit: MiB. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeBackups&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xsh2xs",
	"PageNumber": 1,
	"PageSize": 10,
	"BackupStrategyList": [
        "AutomatedBackup",
        "ManualBackup"
    ]
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "f3ffd83e-bef7-43b9-a803-e75b4f494f49",
        "Action": "DescribeBackups",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "Backups": [
           {
            "BackupPointId": "b-cn02xmmrp751i9cdzcphjmk4jmk4",
            "BackupPointName": "testbackup",
            "BackupProgress": 100,
            "BackupStrategy": "ManualBackup",
            "BackupType": "Full",
            "EndTime": "2024-08-22T07:51:12Z",
            "InstanceId": "redis-cn0212gzmh2xsh2xs",
            "InstanceInfo": {
               "AccountId": 2100000311,
               "ArchType": "Cluster",
               "ChargeType": "PostPaid",
               "DeletionProtection": "disabled",
               "EngineVersion": "5.0",
               "ExpiredTime": "",
               "InstanceId": "redis-cn0212gzmh2xsh2xs",
               "InstanceName": "test",
               "MaintenanceTime": "02:00-02:59",
               "NetworkType": "VPC",               
               "RegionId": "cn-beijing",
               "Replicas": 2,
               "ShardCapacity": 1024,
               "ShardNumber": 2,
               "TotalCapacity": 2048,
               "VpcId": "3tf2ofnsmi3vj0wtj0wt",
               "ZoneIds":[
                 "cn-beijing-a"
               ]
             },            
            "ProjectName": "default",
            "Size": 486040,
            "StartTime": "2024-08-22T07:51:09Z",
            "Status": "Available",
            "TTL": 7
            }
        ],
        "Total": 1
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
