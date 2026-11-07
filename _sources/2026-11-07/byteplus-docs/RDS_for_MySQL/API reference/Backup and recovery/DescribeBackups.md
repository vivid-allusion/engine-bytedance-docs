---
title: "DescribeBackups"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups"
---

Call the DescribeBackups API to query the data backup list.

## Request type

Synchronous request.

## Precautions

MySQL 8.4 instances do not support backup encryption.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBackups&serviceCode=rds_mysql&version=2022-01-01&groupName=)

## Request parameters

|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |No |mysql\-603e30e6\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> This field can be omitted when querying backups of deleted instances (i.e., when ResultFilter is set to `DeletedInstanceBackupOnly`). This field is required in other query scenarios.<br> |
|BackupId |String |No |06797d5eff774e339d6cbbefa2aa\*\*\*\* |Backup ID.<br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all backups limited by other query conditions are returned.<br> |
|BackupStartTime |String |No |2022\-01\-01T10:10:10.000Z |Earliest backup creation time. Accepts UTC time in the following format:<br><br><br>* `2022-01-02T15:04:05Z` will be converted to the local time `2022-01-02 15:04:05`.<br><br>* If the provided time is not in the specified UTC format, it is returned as is. |
|BackupEndTime |String |No |2022\-01\-01T20:10:10.000Z |Latest backup creation time. Accepts UTC time in the following format:<br><br><br>* `2022-01-02T15:04:05Z` will be converted to the local time `2022-01-02 15:04:05`.<br><br>* If the provided time is not in the specified UTC format, it is returned as is. |
|BackupStatus |String |No |Success |Backup status, values:<br><br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `In progress`: in progress.<br><br><br>> **tip**<br><br><br>> Default value. If this field is not specified, backups in all statuses that match the other query conditions are returned.<br> |
|BackupType |String |No |Full |Backup method, values:<br><br><br>* `Full`: a full backup for a physical backup, or a database & table backup for a logical backup.<br><br>* `Increment`: an incremental backup for the physical backup.<br><br>* `DumpAll`: full database backup of the logical backup type.<br><br><br>> **tip**<br><br><br>> Default value. If this parameter is not specified, backups for all backup methods that meet the query conditions defined by other parameters are returned.<br> |
|CreateType |String |No |System |Backup creator. Values:<br><br><br>* `System`: system.<br><br>* `User`: user.<br><br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all types of backups that meet the query conditions of other fields are returned.<br> |
|BackupMethod |String |No |Physical |Backup type, values:<br><br><br>* `Physical`: physical backup.<br><br>* `Logical`: logical backup.<br><br>* `Snapshot`: snapshot backup.<br><br><br>> **tip**<br><br><br>> Default value. If this field is not specified, backups in all statuses that match the other query conditions are returned.<br> |
|PageNumber |Integer |No |1 |Current page number. The minimum value is 1. Default value: 1. |
|PageSize |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 1,000. The default value is 10. |
|Option |Object of [BackupExtraOption](https://docs.byteplus.com/en/docs/40/15430#backupextraoption) |No |See the request example. |Extended query configuration. |
|ProjectName |String |No |default |Project name. Used to query the backups of deleted instances in a specified project when the Instance ID is not specified. |
|BackupName |String |No |Manual backup 001 |The name of the backup. If you do not specify a backup name, the backup ID will be returned instead. |

### BackupExtraOption

|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|ResultFilter |String |No |CrossRegionOnly |Query condition. Values:<br><br><br>* `Default`: Queries basic backups and cross\-regional backups.<br><br>* `BasicBackupOnly`: Queries basic backups only.<br><br>* `CrossRegionOnly`: Queries cross\-regional backups only.<br><br>* `DeletedInstanceBackupOnly`: Queries backups of deleted instances only.<br><br><br>> **tip**<br><br><br>> When the value is `DeletedInstanceBackupOnly`:<br><br><br><br>* > The InstanceId field is optional.<br><br><br>* > Pass the ProjectName field to query backups of deleted instances by project.<br> |
|BriefResultOnly |Boolean |No |true |Specifies whether to return only summary information. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br>> If the value is `true`, the DBTableInfos field is not returned.<br> |
|ResultSorter |String |No |SortByFileSizeAsc |Supports sorting by a specified condition. Values:<br><br><br>* `Default`: Data backups are sorted by start time in descending order, and log backups are sorted by backup time in descending order.<br><br>* `SortByTimeAsc`: Data backups are sorted by start time in ascending order, and log backups are sorted by backup time in ascending order.<br><br>* `SortByTimeDesc`: Data backups are sorted by start time in descending order, and log backups are sorted by backup time in descending order.<br><br>* `SortByFileSizeAsc`: Sorts by file size in ascending order.<br><br>* `SortByFileSizeDesc`: Sorts by file size in descending order. |

## Response parameters

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Integer |1 |Total number of backups. |
|Backups |Array of [BackupObject](https://docs.byteplus.com/en/docs/40/15430#backupobject) |Null |Backup list. |

### BackupObject

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|BackupEndTime |String |2023\-12\-26T06:24:45.000Z |Backup end time, in the format `yyyy-MM-ddTHH:mm:ss.sssZ` format (UTC time). |
|BackupFileName |String |full\-1638021415869047766\-163802160043687\*\*\*\*.xbstream |Backup filename. |
|BackupFileSize |Long |1024 |Backup file size in bytes. |
|BackupId |String |06797d5eff774e339d6cbbefa2aa\*\*\*\* |Backup ID. |
|BackupMethod |String |Physical |Backup type, values:<br><br><br>* `Physical`: physical backup.<br><br>* `Logical`: logical backup.<br><br>* `Snapshot`: snapshot backup. |
|BackupName |String |Manual backup 001 |The name of the backup. |
|BackupRegion |String |cn\-shanghai |The region where the backup is located. |
|BackupStartTime |String |2023\-12\-26T06:24:43.000Z |Backup start time, in the format `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|BackupStatus |String |Success |Backup status, values:<br><br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `In progress`: in progress. |
|BackupType |String |Full |Backup method. The value can be:<br><br><br>* `Full`: Full backup for the physical backup type or database & table backup for the logical backup type.<br><br>* `Increment`: Incremental backup for the physical backup type (created by the system).<br><br>* `DumpAll`: full database backup of the logical backup type.<br><br><br>> **tip**<br><br><br>> Default value. If this field is not specified, all types of backups that meet the query conditions of other fields are returned.<br> |
|ConsistentTime |String |2022\-01\-01T10:10:10Z |The time point of the consistent snapshot. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` format (UTC). |
|CreateType |String |System |Backup creator. Values:<br><br><br>* `System`: system.<br><br>* `User`: user. |
|DBEngineVersion |String |MySQL_8_0 |Compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0.<br><br>* `MySQL 8.4`: MySQL 8.4. |
|DBTableInfos |Array of [DBTableInfoObject](https://docs.byteplus.com/en/docs/40/15430#dbtableinfoobject) |[{<br><br>"Database": "database1",<br><br>"Tables":<br><br>[<br><br>"table1"<br><br>]<br><br>}] |The information about the database tables in the backup set, which includes information for up to 10,000 tables.<br><br>> **tip**<br><br><br><br>* > This field is not returned when the database is empty.<br><br><br>* > This field is not returned when BriefResultOnly is set to `true`.<br> |
|DownloadStatus |String |NotDownload |Download status. Values:<br><br><br>* `NotDownload`: Not downloaded.<br><br>* `Success`: Downloaded.<br><br>* `Failed`: Download failed.<br><br>* `Running`: Downloading. |
|ExpiredTime |String |2024\-01\-02T06:24:45.000Z |Backup expiration time, in the format `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|IsEncrypted |Boolean |true |Indicates whether the data backup is encrypted. Values:<br><br><br>* `true`: encrypted.<br><br>* `false`: not encrypted. |
|IsExpired |Boolean |false |Indicates whether the backup has expired. Values:<br><br><br>* `true`: expired.<br><br>* `false`: not expired. |
|ErrorMessage |String |\- |Error message for the failed backup.<br><br>> **tip**<br><br><br>> This field is returned only when the backup failed.<br> |
|EngineType |String |RocksDB |Database engine type. Values:<br><br><br>* `InnoDB`: InnoDB engine.<br><br>* `RocksDB`: RocksDB engine.<br><br><br>> **tip**<br><br><br>> When used as a request parameter, the default value is `InnoDB`.<br> |

### DBTableInfoObject

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Database |String |db1 |Database name. |
|Tables |Array of String |["table1","table2","table3"] |The name of the data table. |

## Sample

### Sample request

```json
POST /?Action=DescribeBackups&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-ce48081d****"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240708123429B0632E8A17E7206934CE-44fd0d",
        "Action": "DescribeBackups",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Backups": [
            {
                "BackupEndTime": "2024-07-08T04:34:09.000Z",
                "BackupFileName": "full-1720413240726014861.xbstream",
                "BackupFileSize": 183100084,
                "BackupId": "c3331a5996ca4103b98376a153fadb14",
                "BackupMethod": "Physical",
                "BackupName": "手动备份001",
                "BackupRegion": "cn-shanghai",
                "BackupStartTime": "2024-07-08T04:34:01.000Z",
                "BackupStatus": "Success",
                "BackupType": "Full",
                "CanDelete": true,
                "ConsistentTime": "",
                "CreateType": "System",
                "DBEngineVersion": "MySQL_5_7",
                "DBTableInfos": [
                    {
                        "Database": "testdb1",
                        "Tables": [
                            ""
                        ]
                    },
                    {
                        "Database": "testdb2",
                        "Tables": [
                            ""
                        ]
                    },
                    {
                        "Database": "testdb3",
                        "Tables": [
                            "t3",
                            "t2",
                            "t1"
                        ]
                    }
                ],
                "DownloadStatus": "NotDownload",
                "ExpiredTime": "2024-07-15T04:34:09.000Z",
                "IsEncrypted": false,
                "IsExpired": false
            },
            {
                "BackupEndTime": "2024-07-08T04:34:03.000Z",
                "BackupFileName": "full-1720413240726014861.xbstream",
                "BackupFileSize": 183100084,
                "BackupId": "18a414f362a74349a63de3fb2df113c5",
                "BackupMethod": "Physical",
                "BackupRegion": "cn-beijing",
                "BackupStartTime": "2024-07-08T04:34:01.000Z",
                "BackupStatus": "Success",
                "BackupType": "Full",
                "CanDelete": true,
                "ConsistentTime": "",
                "CreateType": "User",
                "DBTableInfos": [
                    {
                        "Database": "testdb1",
                        "Tables": [
                            ""
                        ]
                    },
                    {
                        "Database": "testdb2",
                        "Tables": [
                            ""
                        ]
                    },
                    {
                        "Database": "testdb3",
                        "Tables": [
                            "t3",
                            "t2",
                            "t1"
                        ]
                    }
                ],
                "DownloadStatus": "Success",
                "ExpiredTime": "2024-07-15T04:34:03.000Z",
                "IsEncrypted": false,
                "IsExpired": false
            }
        ],
        "Total": 2
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
