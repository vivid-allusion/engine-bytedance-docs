---
title: "DescribeBackups"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups"
---

Call the DescribeBackups API to query a list of backups.

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|BackupId |String |No |20231101\-021\*\*\*\*_20231101\-101\*\*\*\* |Backup ID.<br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|BackupStartTime |String |No |2023\-10\-19T06:20:06.000Z |Earliest backup creation time, in the format `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br>> **tip**<br><br><br><br>* > Based on the backup start time.<br><br><br>* > Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|BackupEndTime |String |No |2023\-10\-19T06:20:08.000Z |Latest backup creation time, in the format `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br>> **tip**<br><br><br><br>* > Based on the backup start time.<br><br><br>* > Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|BackupStatus |String |No |Success |Backup status, values:<br><br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `In progress`: in progress. |
|BackupType |String |No |Full |Backup type, values:<br><br><br>* `Full backup`: full backup.<br><br>* `Incremental backup method`: incremental backup.<br><br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|PageNumber |Integer |No |1 |The query offset of the current page. The default value is 1. |
|PageSize |Integer |No |10 |The number of records on each page. The value must be greater than 0 and no more than 1,000. The default value is 10. |
|DownloadStatus |String |No |NotAllowed |download status of the backup and recovery Values:<br><br><br>* `NotAllowed`: download is not supported.<br><br>   > Note<br>   <br><br><br>> The current physical backup does not support download.<br><br><br><br>* `NeedToPrepare`: backup and recovery are ready, require background preparation of backup (that is, BackupStatus is Success and a "Retrieve" task needs to be initiated).<br><br>* `LinkReady`: backup and recovery are prepared, and the download link is still valid. |
|BackupMethod |String |No |Logical |Backup type. Values:<br><br><br>* `Physical`: Physical backup. Default value.<br><br>* `Logical`: Logical backup.<br><br><br>> **tip**<br><br><br>> When BackupScope is set to `Database`, BackupMethod can only be set to `Logical`.<br> |
|BackupDatabaseName |String |No |database1 |Database name included in the backup and recovery. When this field is specified, it will be used as a keyword to search database names included in the backup and recovery.<br><br>> **tip**<br><br><br>> Effective only when BackupMethod value is `Logical`.<br> |
|BackupDescription |String |No |This is a description of the backup set. |Backup set description. |
|CreateType |String |No |System |Create type. Value range:<br><br><br>* `System`: system.<br><br>* `User`: user.<br><br><br>> **tip**<br><br><br>> Default value. If not specified, return backups limited by other query conditions.<br> |
|BackupScope |String |No |Database |Backup target. Values:<br><br><br>* `Entire instance`. Default value.<br><br>* `Database`: specified databases. |

## Response parameters

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of backups. |
|Backups |Array of [BackupObject](https://docs.byteplus.com/en/docs/61/15715#backupobject) |Refer to the sample response. |Backup list. |

### BackupObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BackupDataSize |Long |1024 |The original size of the data contained in the backup. Unit is Byte. |
|BackupDescription |String |This is a description of the backup set. |Description information of the backup. |
|BackupEndTime |String |2025\-05\-12T11:45:55.000Z |Backup end time. Time format is `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|BackupFileName |String |20250512\-194554\-792LD |Name of the backup file. |
|BackupFileSize |Long |512 |Backup file size in bytes. |
|BackupId |String |20250512\-194554\-792LD |Backup ID. |
|BackupMeta |Array of [BackupMetaObject](https://docs.byteplus.com/en/docs/61/15715#backupmetaobject) |Refer to the sample response. |Information on the databases included in the backup. |
|BackupMethod |String |Logical |Backup type. Values:<br><br><br>* `Physical`: Physical backup. Default value.<br><br>* `Logical`: Logical backup.<br><br><br>> **tip**<br><br><br>> When BackupScope is set to `Database`, BackupMethod can only be set to `Logical`.<br> |
|BackupProgress |Integer |100 |Backup progress. The unit is percentage. |
|BackupScope |String |Database |Backup target. Values:<br><br><br>* `Entire instance`. Default value.<br><br>* `Database`: specified databases. |
|BackupStartTime |String |2025\-05\-12T11:45:55.000Z |Backup start time. Time format is `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|BackupStatus |String |Success |Backup status. Values:<br><br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `In progress`: in progress. |
|BackupType |String |Full |Backup type, values:<br><br><br>* `Full backup`: full backup. Default value.<br><br>* `Increment`: incremental backup.<br><br><br>> **tip**<br><br><br>> This parameter is supported only when BackupMethod is set to Physical.<br> |
|CreateType |String |System |Backup creator. Values:<br><br><br>* `System`: system.<br><br>* `User`: user. |
|DownloadStatus |String |NotAllowed |download status of the backup and recovery Values:<br><br><br>* `NotAllowed`: download is not supported.<br><br>   > Note<br>   <br><br><br>> The current physical backup does not support download.<br><br><br><br>* `NeedToPrepare`: backup and recovery are ready, require background preparation of backup (that is, BackupStatus is Success and a "Retrieve" task needs to be initiated).<br><br>* `LinkReady`: backup and recovery are prepared, and the download link is still valid. |
|InstanceInfo |Object of [InstanceInfoObject](https://docs.byteplus.com/en/docs/61/15715#instanceinfoobject) |Refer to the sample response. |Detailed information of the instance to which the backup belongs. |

### BackupMetaObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBName |String |database1 |Name of the database to be backed up. |

### InstanceInfoObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListIds |Array of String |[<br><br>"acl\-fdd6293f300143f2a4932bb483c8\*\*\*\*",<br><br>"acl\-ded4c0b707e44efd8f0dbc4e88f5\*\*\*\*"<br><br>] |Information about the allowlist associated with the instance to which the backup belongs. |
|ChargeDetail |Object of [ChargeDetailObject](https://docs.byteplus.com/en/docs/61/15715#chargedetailobject) |Refer to the sample response. |Instance billing information. |
|DBEngineVersion |String |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|InstanceName |String |test\-instance\-name |Storage type. |
|InstanceStatus |String |Running |Instance state, values:<br><br><br>* `Running`: running.<br><br>* `Creating`: creating.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: Restarting.<br><br>* `Restoring`: recovering.<br><br>* `Updating`: modifying.<br><br>* `Upgrading`: upgrading.<br><br>* `Error`: error.<br><br>* `Released`: released.<br><br>* `CreateError`: create error.<br><br>* `MasterChanging`: primary node switching.<br><br>* `Deleted`: Deleted.<br><br>* `Recycled`: recycled. |
|InstanceType |String |HA |Instance type. Value: `HA` (High\-availability Edition). |
|Memory |Integer |2 |Memory size. Unit: GB. |
|Nodes |Array of [NodeObject](https://docs.byteplus.com/en/docs/61/15715#nodeobject) |Refer to the sample response. |Instance node information. |
|ProjectName |String |testProject |Project name. |
|StorageSpace |Integer |200 |The storage space for the instance. Unit: GB. |
|StorageType |String |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk). |
|SubnetId |String |subnet\-30vhlwb1el0qo7r2qr2c5\*\*\*\* |Subnet ID. |
|VCPU |Integer |1 |CPU size. For example: 1 indicates 1U. |
|VpcId |String |vpc\-3rebt5uf5fr405zsk2if9\*\*\*\* |Virtual private cloud (VPC) ID. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |

### ChargeDetailObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ChargeType |String |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go.<br><br>* `PrePaid`: subscription (default). |
|AutoRenew |Boolean |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `yes`: automatic renewal.<br><br>* `false`: no automatic renewal (default). |
|Number |Integer |1 |Number of instances. |
|PeriodUnit |String |Month |Purchase period for prepaid scenarios.<br><br><br>* `Month`: monthly (default).<br><br>* `Year`: subscription. |
|Period |Integer |1 |Subscription duration in a prepaid scenario. default value: 1. |
|ChargeStatus |String |Normal |Payment status. Values:<br><br><br>* `Normal`: normal.<br><br>* `Overdue`: overdue.<br><br>* `Overdue`: waiting for payment. |
|ChargeStartTime |String |2023\-01\-10T11:13:30.000Z |Instance billing start time. |
|ChargeEndTime |String |2023\-01\-10T11:13:34.000Z |Subscription instance expiration time. |
|OverdueTime |String |2023\-01\-10T11:13:30.000Z |Overdue shutdown time of the instance. |
|OverdueReclaimTime |String |2023\-01\-15T16:00:00.000Z |Estimated release time after the instance is suspended due to overdue payments. |
|TempModifyStartTime |String |2023\-12\-01T10:10:10.000Z |Start time of temporary upgrade.<br><br>> **tip**<br><br><br><br>* > Return when the instance is under temporary upgrade.<br><br><br>* > If multiple consecutive temporary upgrades are performed on the instance, this returns the start time of the first temporary upgrade.<br> |
|TempModifyEndTime |String |2023\-12\-07T10:10:09.000Z |Restoration time of temporary upgrade.<br><br>> **tip**<br><br><br>> Return when the instance is under temporary upgrade.<br> |

### NodeObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|NodeId |String |postgres\-ca7b7019\*\*\*\*\-zgqy |Node ID. |
|RegionId |String |cn\-beijing |Region ID. You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_PG/describeregions) API to query the list of available regions. Use this parameter to specify the region where you want to create the instance. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|NodeType |String |Primary |Node type, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: indicates the secondary node.<br><br>* `ReadOnly`: Read\-only node. |
|NodeStatus |String |Running |Node status. |
|NodeSpec |String |rds.postgres.1c2g |Node specification. |
|VCPU |Integer |4 |CPU size. For example: 1 means 1U. |
|Memory |Integer |16 |Memory size. Unit is GB. |
|CreateTime |String |2022\-01\-01T10:10:10Z |Node creation time. Format is yyyy\-MM\-ddTHH:mm:ss.sssZ (UTC time). |
|UpdateTime |String |2022\-01\-01T10:10:10Z |Node update time. Format is yyyy\-MM\-ddTHH:mm:ss.sssZ (UTC time). |

## Sample

### Sample request

```json
POST /?Action=DescribeBackups&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-a3e7eb2f****"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308041100439000B4A38D7086052659",
        "Action": "DescribeBackups",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Backups": [
            {
                "BackupDataSize": 16785668,
                "BackupDescription": "",
                "BackupEndTime": "2025-05-12T12:21:15.000Z",
                "BackupFileName": "20250512-194637F_20250512-202111I",
                "BackupFileSize": 16785668,
                "BackupId": "20250512-194637F_20250512-202111I",
                "BackupMethod": "Physical",
                "BackupProgress": 100,
                "BackupScope": "Instance",
                "BackupStartTime": "2025-05-12T12:21:11.000Z",
                "BackupStatus": "Success",
                "BackupType": "Increment",
                "CreateType": "System",
                "DownloadStatus": "NotAllowed",
                "InstanceInfo": {
                    "AllowListIds": [
                        "acl-fdd6293f300143f2a4932bb483c8****",
                        "acl-ded4c0b707e44efd8f0dbc4e88f5****"
                    ],
                    "ChargeDetail": {
                        "AutoRenew": false,
                        "ChargeEndTime": "",
                        "ChargeStartTime": "2023-09-11T06:43:34.000Z",
                        "ChargeStatus": "Normal",
                        "ChargeType": "PostPaid",
                        "Number": 1,
                        "OverdueReclaimTime": "",
                        "OverdueTime": "",
                        "Period": 1,
                        "PeriodUnit": "Month"
                    },
                    "DBEngineVersion": "PostgreSQL_12",
                    "InstanceId": "postgres-da8f12d3****",
                    "InstanceName": "测试实例",
                    "InstanceStatus": "Running",
                    "InstanceType": "HA",
                    "Memory": 2,
                    "Nodes": [
                        {
                            "InstanceId": "postgres-da8f12d3****",
                            "NodeId": "postgres-da8f12d3****",
                            "NodeSpec": "rds.postgres.1c2g",
                            "NodeType": "Primary",
                            "ZoneId": "cn-beijing-b"
                        },
                        {
                            "InstanceId": "postgres-da8f12d3****",
                            "NodeId": "postgres-da8f12d3****-fkoh",
                            "NodeSpec": "rds.postgres.1c2g",
                            "NodeType": "Secondary",
                            "ZoneId": "cn-beijing-a"
                        }
                    ],
                    "ProjectName": "rds-pg",
                    "StorageSpace": 20,
                    "StorageType": "LocalSSD",
                    "SubnetId": "subnet-30uhx4w39n75s7r2qr0lq****",
                    "VCPU": 1,
                    "VpcId": "vpc-2gdgzrrl5icjk50ztyz6b****",
                    "ZoneId": "cn-beijing-b"
                }
            }
        ],
        "Total": 1
    }
}
```
