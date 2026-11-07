---
title: "DescribeDetachedBackups"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups"
---

Call the DescribeDetachedBackups API to query the backup of a deleted instance.

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|BackupId |String |No |20231016\-024\*\*\*\* |Backup ID. |
|InstanceId |String |No |postgres\-5704170c\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|InstanceName |String |No |Test instance |Storage type.<br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|BackupStartTime |String |No |2022\-01\-01T10:10:10.000Z |Earliest backup creation time. Based on backup start time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|BackupEndTime |String |No |2022\-01\-01T10:10:10.000Z |Latest backup creation time. Based on backup start time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|ProjectName |String |No |Test |The project to which the instance belongs.<br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|BackupStatus |String |No |Success |Backup status. Optional. Default value is `Success`, which means querying backups with a successful status. |
|BackupType |String |No |Full |Backup type. Optional. Default value is `Full`, which means full backups are queried. |
|PageNumber |Integer |No |1 |The query offset of the current page. The default value is 1. |
|PageSize |Integer |No |10 |The number of records on each page. The value must be greater than 0 and no more than 1,000. The default value is 10. |

## Response parameters

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of backups. |
|Backups |Array of [BackupsInfo](https://docs.byteplus.com/en/docs/61/15716#backupsinfo) |Refer to the sample response. |Backup list. |

### BackupsInfo

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BackupId |String |20231016\-024\*\*\*\*_20231017\-125\*\*\*\* |Backup ID. |
|BackupFileName |String |20230508\-021\*\*\*\*_20230511\-141\*\*\*\* |Backup file name. |
|BackupStatus |String |Success |Backup status, values:<br><br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `In progress`: in progress. |
|BackupProgress |Integer |70 |Backup progress percentage.<br><br><br>* When `BackupStatus` is `Success`, `BackupProgress` is 100.<br><br>* When `BackupStatus` is `Running`, `BackupProgress` ranges from 0 to 100. |
|BackupType |String |Full |Backup type, values:<br><br><br>* `Full`: full backup (default).<br><br>* `Increment`: incremental backup. |
|CreateType |String |System |Create type. Value range:<br><br><br>* `System`: system.<br><br>* `User`: user.<br><br><br>> **tip**<br><br><br>> Default value. If not specified, return backups limited by other query conditions.<br> |
|BackupFileSize |Long |41750219 |Backup file size in bytes. |
|BackupStartTime |String |2022\-01\-01T10:10:10.000Z |Backup start time, in the format `yyyy-MM-dd HH:mm:ss.sssZ` (UTC time). |
|BackupEndTime |String |2022\-01\-01T10:10:10.000Z |Backup end time, in the format `yyyy-MM-dd HH:mm:ss.sssZ` (UTC time). |
|InstanceInfo |Object of [InstanceInfoObject](https://docs.byteplus.com/en/docs/61/15716#instanceinfoobject) |Refer to the sample response. |Summary. |

### InstanceInfoObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListIds |Array of String |[<br><br>"acl\-fdd6293f300143f2a4932bb483c8\*\*\*\*",<br><br>"acl\-ded4c0b707e44efd8f0dbc4e88f5\*\*\*\*"<br><br>] |Information about the allowlist associated with the instance to which the backup belongs. |
|ChargeDetail |Object of [ChargeDetailObject](https://docs.byteplus.com/en/docs/61/15716#chargedetailobject) |Refer to the Sample response. |Instance billing information. |
|DBEngineVersion |String |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|InstanceName |String |test\-instance\-name |Storage type. |
|InstanceStatus |String |Running |Instance state, values:<br><br><br>* `Running`: running.<br><br>* `Creating`: creating.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: Restarting.<br><br>* `Restoring`: recovering.<br><br>* `Updating`: modifying.<br><br>* `Upgrading`: upgrading.<br><br>* `Error`: error.<br><br>* `Released`: released.<br><br>* `CreateError`: create error.<br><br>* `MasterChanging`: primary node switching.<br><br>* `Deleted`: Deleted.<br><br>* `Recycled`: recycled. |
|InstanceType |String |HA |Instance type. Value: `HA` (High\-availability Edition). |
|Memory |Integer |2 |Memory size. Unit: GB. |
|Nodes |Array of [NodeObject](https://docs.byteplus.com/en/docs/61/15716#nodeobject) |Refer to the sample response. |Instance node information. |
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

## Example

### Sample request

```json
POST /?Action=DescribeDetachedBackups&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "BackupId": "20231018-211218F",
    "InstanceId": "postgres-5704170c****",
    "InstanceName": "测试实例",
    "BackupStartTime": "2023-10-18T13:12:18.000Z",
    "BackupEndTime": "2023-10-18T13:17:47.000Z",
    "BackupType": "Full"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023101821494419338B706183F9C58CA9",
        "Action": "DescribeDetachedBackups",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Backups": [
            {
                "BackupEndTime": "2023-10-18T13:17:47.000Z",
                "BackupFileName": "",
                "BackupFileSize": 67509779278,
                "BackupId": "20231018-211218F",
                "BackupProgress": 0,
                "BackupStartTime": "2023-10-18T13:12:18.000Z",
                "BackupStatus": "Success",
                "BackupType": "Full",
                "CreateType": "System",
                "InstanceInfo": {
                    "AllowListIds": [
                        "acl-fdd6293f300143f2a4932bb483c8****",
                        "acl-ded4c0b707e44efd8f0dbc4e88f5****"
                    ],
                    "ChargeDetail": {
                        "AutoRenew": false,
                        "ChargeEndTime": "",
                        "ChargeStartTime": "",
                        "ChargeStatus": "Normal",
                        "ChargeType": "PostPaid",
                        "Number": 0,
                        "OverdueReclaimTime": "",
                        "OverdueTime": "",
                        "Period": 0,
                        "PeriodUnit": "Month"
                    },
                    "DBEngineVersion": "PostgreSQL_12",
                    "InstanceId": "postgres-5704170c****",
                    "InstanceName": "测试实例",
                    "InstanceStatus": "Deleted",
                    "InstanceType": "HA",
                    "Memory": 8,
                    "Nodes": [
                        {
                            "InstanceId": "postgres-5704170c****",
                            "NodeId": "postgres-5704170c****",
                            "NodeSpec": "rds.postgres.1c2g",
                            "NodeType": "Primary",
                            "ZoneId": "cn-beijing-c"
                        },
                        {
                            "InstanceId": "postgres-5704170c****",
                            "NodeId": "postgres-5704170c****-zgqy",
                            "NodeSpec": "rds.postgres.1c2g",
                            "NodeType": "Secondary",
                            "ZoneId": "cn-beijing-a"
                        },
                        {
                            "InstanceId": "postgres-5704170c****",
                            "NodeId": "postgres-5704170c****-ro2341",
                            "NodeSpec": "rds.postgres.1c2g",
                            "NodeType": "ReadOnly",
                            "ZoneId": "cn-beijing-b"
                        }
                    ],
                    "ProjectName": "default",
                    "StorageSpace": 100,
                    "StorageType": "LocalSSD",
                    "StorageUse": 100,
                    "SubnetId": "subnet-3jhi4ozzmj6dc3pncmejx****",
                    "VCPU": 4,
                    "VpcId": "vpc-2gdku6nvnp1xc50ztz0py****"
                }
            }
        ],
        "Total": 1
    }
}
```
