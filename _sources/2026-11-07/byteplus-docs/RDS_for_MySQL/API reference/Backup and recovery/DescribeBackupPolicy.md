---
title: "DescribeBackupPolicy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackuppolicy"
---

Call the DescribeBackupPolicy API to query the backup policy of a specified instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-d4942fd7\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|BinlogBackupAllRetention |Boolean |true |Whether to retain all log backups before releasing the instance. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|BinlogBackupEnabled |Boolean |true |Whether to enable log backup. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|BinlogBackupEncryptionEnabled |Boolean |true |Whether to enable encryption for log backups. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|BinlogFileCountsEnable |Boolean |true |Whether to enable the upper limit for local Binlog retention. Valid values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|BinlogLimitCount |Integer |10 |The number of local Binlog files to retain. Valid values: `6~1000`. When the number exceeds the specified limit, the oldest local logs will be automatically deleted. |
|BinlogLocalRetentionHour |Integer |7 |The retention period for local Binlog files. Valid values: `0~168`. When the retention period exceeds the specified limit, the oldest local logs will be automatically deleted. When set to `0`, local logs will not be automatically deleted. |
|BinlogSpaceLimitEnable |Boolean |true |Whether to enable automatic cleanup of Binlog when storage space is insufficient. When the total storage space usage of the instance exceeds 80% or the remaining space is less than 5 GiB, the system will automatically delete the oldest local Binlog files until the total space usage is below 80% and the remaining space is greater than 5 GiB. |
|BinlogStoragePercentage |Integer |30 |The maximum storage space usage percentage. Can be set between 20%~50%. When exceeded, the oldest Binlog files will be automatically deleted until the space usage falls below this percentage.<br><br>tip<br><br>Local Binlog space usage = Local Binlog size / Total available (purchased) space of the instance. |
|DataBackupAllRetention |Boolean |true |Whether to retain all data backups before releasing the instance. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|DataBackupEncryptionEnabled |Boolean |true |Whether to enable the encryption function for the data backup of the local disk instance. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No.<br><br><br>tip<br><br>This function is not currently supported for cloud disk instances. |
|DataBackupRetentionDay |Integer |7 |The retention period of the backup file. The value range of the backup retention days for different storage type instances is different:<br><br><br>* For local disk instances: the optional range is 7 to 3650 days, with a default of 7 days.<br><br>* For cloud disk instances: currently only 7 days of retention is supported. |
|DataFullBackupPeriods |String[] |["Monday","Wednesday","Friday",Sunday"] |Full backup cycle. Valid values:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday. |
|DataFullBackupStartUTCHour |Integer |16 |The start time (UTC) of the full backup window. The window length is 1 hour.<br><br>tip<br><br>Both DataFullBackupStartUTCHour and DataFullBackupTime can be used to specify the full backup time window for the instance. DataFullBackupStartUTCHour has higher priority. If both fields are returned, DataFullBackupStartUTCHour will be used. |
|DataFullBackupTime |String |18:00Z\-19:00Z |The time window for executing backup tasks. The window length is 1 hour. Format: HH:mmZ\-HH:mmZ (UTC time).<br><br>tip<br><br>Both DataFullBackupStartUTCHour and DataFullBackupTime can be used to specify the full backup time window for the instance. DataFullBackupStartUTCHour has higher priority. If both fields are returned, DataFullBackupStartUTCHour will be used. |
|DataKeepDaysAfterReleased |Integer |7 |The number of days to retain backups after the instance is released. Currently, only `7`is supported. |
|DataKeepPolicyAfterReleased |String |Last |The policy for retaining backups after the instance is released. Supported values are as follows.<br><br><br>* `Last`: Retain the last backup. This is the default value.<br><br>* `All`: Retain all backups of the instance.<br><br>* `None`: Do not retain any backups. |
|DataIncrBackupPeriods |String[] |["Monday","Wednesday","Friday","Sunday"] |The incremental backup cycle of local disk instances, with possible values:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday.<br><br><br>tip<br><br>This field is not returned when high\-frequency incremental backup is enabled (HourlyIncrBackupEnable is set to `true`). |
|HourlyIncrBackupEnable |Boolean |true |Whether the local disk instance enables the high\-frequency backup function. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|IncrBackupHourPeriod |Integer |2 |The frequency of high\-frequency incremental backup for local disk instances. Values:<br><br><br>* `0`: No high\-frequency incremental backup. HourlyIncrBackupEnable is set to `false`.<br><br>* `2`: Perform incremental backup every 2 hours.<br><br>* `4`: Perform incremental backup every 4 hours.<br><br>* `6`: Perform incremental backup every 6 hours.<br><br>* `12`: Perform incremental backup every 12 hours. |
|InstanceId |String |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|LockDDLTime |Integer |30 |The maximum waiting time for DDL. Default is 30, minimum is 10, maximum is 1440, in minutes. |
|LockDDLTimeSecond |Integer |1800 |The maximum waiting time for DDL. The maximum value is 86400, the minimum value is 1, the default value is 1800, the unit is seconds, and the step size is 1. |
|LogBackupRetentionDay |Integer |7 |Binlog backup retention period. The value range of the backup retention days for instances of different storage types is different:<br><br><br>* For local disk instances: The optional range is 7 to 3650 days, with a default of 7 days.<br><br>* For cloud disk instances: The optional range is 7 to 720 days, with a default of 7 days.<br><br><br>tip<br><br>This parameter is not returned when RetentionPolicySynced is set to `true`. |
|RetentionPolicySynced |Boolean |true |Whether the retention policy for log backups is consistent with that for data backups. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|PublicDownloadEnable |Boolean |true |Whether to allow downloading backup data of the instance from the public network. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|HighFrequencySnapshotBackupEnable |Boolean |true |Whether the high\-frequency incremental snapshot backup function of the cloud disk instance is enabled. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|HighFrequencySnapshotBackupSecondPeriod |Integer |3600 |The frequency of high\-frequency incremental snapshot backup for cloud disk instances, in seconds. Values:<br><br><br>* `3600`: Every 1 hour.<br><br>* `7200`: Every 2 hours.<br><br>* `10800`: Every 3 hours.<br><br>* `14400`: Every 4 hours.<br><br>* `19200`: Every 6 hours.<br><br>* `28800`: Every 8 hours.<br><br>* `38400`: Every 12 hours.<br><br><br>tip<br><br>When the value of HighFrequencySnapshotBackupEnable is `false`, the value of this field is 0. |
|KeepCrossBackupEnableAfterReleased |Boolean |true |Whether to retain cross \- region backups when releasing the instance. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |

## Sample request

```json
POST /?Action=DescribeBackupPolicy&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-d4942fd7****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308101124409984CE8C71ABEA55A2B8",
        "Action": "DescribeBackupPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "BinlogBackupAllRetention": false,
        "BinlogBackupEnabled": true,
        "BinlogBackupEncryptionEnabled": false,
        "BinlogFileCountsEnable": true,
        "BinlogLimitCount": 60,
        "BinlogLocalRetentionHour": 24,
        "BinlogSpaceLimitEnable": false,
        "BinlogStoragePercentage": 30,
        "DataBackupAllRetention": false,
        "DataBackupEncryptionEnabled": false,
        "DataBackupRetentionDay": 8,
        "DataFullBackupPeriods": [
            "Monday",
            "Tuesday",
            "Wednesday"
        ],
        "DataFullBackupStartUTCHour": 16,
        "DataFullBackupTime": "16:00Z-16:59Z",
        "DataKeepDaysAfterReleased": 7,
        "DataKeepPolicyAfterReleased": "All",
        "HourlyIncrBackupEnable": true,
        "IncrBackupHourPeriod": 4,
        "InstanceId": "mysql-d4942fd7****",
        "LockDDLTime": 30,
        "LogBackupRetentionDay": 7,
        "RetentionPolicySynced": false,
        "PublicDownloadEnable": false
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
