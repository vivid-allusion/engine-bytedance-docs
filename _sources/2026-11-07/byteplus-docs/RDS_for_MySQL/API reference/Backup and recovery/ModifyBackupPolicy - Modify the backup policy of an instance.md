---
title: "ModifyBackupPolicy - Modify the backup policy of an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackuppolicy"
---

Call the ModifyBackupPolicy API to modify the backup policy of an instance.

## Request type

Synchronous request.

## Precautions

MySQL 8.4 instances do not support backup encryption.

## Request parameters

|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-46609cf2\*\*\*\* |Instance ID. |
|DataFullBackupPeriods |Array of String |No |["Monday","Wednesday","Friday","Sunday"] |Full backup cycle. We recommend performing a full backup at least two days a week. Separate multiple values with a comma (,). Values:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday. |
|DataBackupRetentionDay |Integer |No |7 |The length of time for retaining backup files after instance release. The range of backup retention days for different storage type instances is different:<br><br><br>* For local disk instances: the optional range is 7 to 3650 days, and the default is 7 days.<br><br>* For cloud disk instances: currently only supports retention for 7 days. |
|DataFullBackupTime |String |No |18:00Z\-19:00Z |The time window to perform backup tasks is 1 hour. Format: `HH:mmZ-HH:mmZ` (UTC time).<br><br>> **tip**<br><br><br><br>* > DataFullBackupStartUTCHour and DataFullBackupTime can both be used to specify the full backup period of an instance. DataFullBackupStartUTCHour has a higher priority. If both of these fields are returned, the value of DataFullBackupStartUTCHour is used.<br><br><br>* > To set a time window starting at 15:00 (UTC), set the end time to 15:59.<br> |
|DataIncrBackupPeriods |Array of String |No |["Monday","Wednesday","Friday","Sunday"] |Incremental backup cycle. Separate multiple values with a comma (,). Values:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday.<br><br><br>> **tip**<br><br><br>> The incremental backup cycle cannot conflict with the full backup cycle.<br> |
|BinlogFileCountsEnable |Boolean |No |true |Whether to enable the local binlog retention limit. Values:<br><br><br>* `true`: enable.<br><br>* `false`: disabled. |
|BinlogLimitCount |Integer |No |10 |The number of local binlogs to retain, with a value from 6 to 1000. Automatically deletes local logs that exceed the retention count. |
|BinlogLocalRetentionHour |Integer |No |7 |The retention period for local binlogs, ranging from 0 to 168 hours. Local logs older than this period are automatically deleted. When set to 0, local logs will not be automatically deleted. |
|BinlogSpaceLimitEnable |Boolean |No |true |Indicates whether to automatically clean up binlogs when storage space usage is excessive. When the total storage space usage of the instance exceeds 80% or the remaining space is less than 5 GiB, the system automatically starts cleaning up the oldest local Binlog files until the total space usage falls below 80% and the remaining space is greater than 5 GiB.<br><br><br>* `true`: enable.<br><br>* `false`: disabled. |
|BinlogStoragePercentage |Integer |No |30 |The maximum storage usage ratio, which can be set from 20% to 50%. If this ratio is exceeded, the earliest Binlog files are automatically deleted until the storage usage is lower than this ratio.<br><br>> **tip**<br><br><br>> Local Binlog space utilization rate = Local Binlog size / Total available (purchased) space of the instance.<br> |
|LogBackupRetentionDay |Integer |No |7 |Binlog backup retention period. The range of backup retention days for different storage type instances is different:<br><br><br>* For local disk instances: the optional range is 7 to 3650 days, and the default is 7 days.<br><br>* For cloud disk instances: the optional range is 7 to 720 days, and the default is 7 days.<br><br><br>> **tip**<br><br><br>> LogBackupRetentionDay does not take effect when RetentionPolicySynced is set to `true`.<br> |
|LockDDLTime |Integer |No |30 |DDL maximum wait time. The default value is 30, the minimum value is 10, and the maximum value is 1440. The unit is minutes. |
|LockDDLTimeSecond |Integer |No |3600 |DDL maximum wait time. The maximum value is 86400, the minimum value is 1, and the default value is 1800. The unit is seconds, and the step is 1.<br><br>> **tip**<br><br><br>> The backup process blocks DDL. If the blocking time exceeds the specified time, the backup automatically stops.<br> |
|DataFullBackupStartUTCHour |Integer |No |16 |The start time of the full backup window in UTC. The time window is 1 hour.<br><br>> **tip**<br><br><br>> DataFullBackupStartUTCHour and DataFullBackupTime can both be used to specify the full backup period of an instance. DataFullBackupStartUTCHour has a higher priority. If both of these fields are returned, the value of DataFullBackupStartUTCHour is used.<br> |
|HourlyIncrBackupEnable |Boolean |No |true |Whether to enable the high frequency back up feature for local disk instances. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|IncrBackupHourPeriod |Integer |No |2 |The high\-frequency incremental backup frequency for local disk instances. Values:<br><br><br>* `2`: Performs an incremental backup every 2 hours.<br><br>* `4`: Performs an incremental backup every 4 hours.<br><br>* `6`: Performs an incremental backup every 6 hours.<br><br>* `12`: Performs an incremental backup every 12 hours.<br><br><br>> **tip**<br><br><br><br>* > When HourlyIncrBackupEnable is set to `true`, IncrBackupHourPeriod is required.<br><br><br>* > IncrBackupHourPeriod is valid only when HourlyIncrBackupEnable is `true`.<br> |
|DataBackupEncryptionEnabled |Boolean |No |true |Specifies whether to enable encryption for data backup for local disk instances. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br>> This feature is not supported for cloud disk instances.<br> |
|BinlogBackupEncryptionEnabled |Boolean |No |true |Specifies whether to enable encryption for log backups. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|DataKeepPolicyAfterReleased |String |No |Last |The policy for retaining instance backups after an instance is released. Values are:<br><br><br>* `Last`: Retain the final backup. Default value.<br><br>* `All`: Retain all instance backups.<br><br>* `None`: Do not retain backups. |
|DataKeepDaysAfterReleased |Integer |No |7 |Number of days to retain the backup after the instance is released. The value must be an integer between 7 and 3650. The default value is 7. |
|DataBackupAllRetention |Boolean |No |true |Whether to retain all data backups before releasing the instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|BinlogBackupAllRetention |Boolean |No |true |Whether to retain all log backups before releasing the instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br>> BinlogBackupAllRetention does not take effect when RetentionPolicySynced is set to `true`.<br> |
|BinlogBackupEnabled |Boolean |No |true |Indicates whether the log backup feature is enabled. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|RetentionPolicySynced |Boolean |No |true |Whether the retention policy for log backups is the same as the retention policy for data backups.<br><br>> **tip**<br><br><br>> When the value is`true`, the system ignores LogBackupRetentionDay and BinlogBackupAllRetention.<br> |
|HighFrequencySnapshotBackupEnable |Boolean |No |false |Indicates whether to enable the high frequency back up feature for the cloud disk instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|HighFrequencySnapshotBackupSecondPeriod |Integer |No |3600 |The frequency of high\-frequency incremental snapshot backups for the cloud disk instance, in seconds. Values:<br><br><br>* `3600`: Every 1 hour.<br><br>* `7200`: Every 2 hours.<br><br>* `10800`: Every 3 hours.<br><br>* `14400`: Every 4 hours.<br><br>* `19200`: Every 6 hours.<br><br>* `28800`: Every 8 hours.<br><br>* `38400`: Every 12 hours. |
|KeepCrossBackupEnableAfterReleased |Boolean |No |false |Specifies whether to enable cross\-regional backup. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br>> This feature is not supported for cloud disk instances.<br> |

## Response parameters

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|BinlogBackupAllRetention |Boolean |true |Whether to retain all log backups before releasing the instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|BinlogBackupEnabled |Boolean |true |Indicates whether the log backup feature is enabled. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|BinlogBackupEncryptionEnabled |Boolean |true |Specifies whether to enable encryption for log backup. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|BinlogFileCountsEnable |Boolean |true |Whether to enable the local binlog retention limit. Values:<br><br><br>* `true`: enable.<br><br>* `false`: disabled. |
|BinlogLimitCount |Integer |10 |Local binlog reservation number, with a value range of `6~1000`. When the number of local logs exceeds the specified retention count, the excess logs are automatically deleted. |
|BinlogLocalRetentionHour |Integer |7 |Local binlog retention period. The value range is `0~168`. Local logs that exceed the retention period will be automatically deleted. When set to `0`, local logs will not be automatically deleted. |
|BinlogSpaceLimitEnable |Boolean |true |Indicates whether to automatically clean up binlogs when storage space usage is excessive. When the total storage space usage of the instance exceeds 80% or the remaining space is less than 5 GiB, the system automatically starts cleaning up the oldest local Binlog files until the total space usage falls below 80% and the remaining space is greater than 5 GiB. |
|BinlogStoragePercentage |Integer |30 |Maximum storage usage ratio, which can be set from 20% to 50%. After this ratio is exceeded, the earliest Binlog files are automatically deleted until the storage usage is lower than this ratio.<br><br>> **tip**<br><br><br>> Local Binlog storage usage = Local Binlog size / Total available (purchased) storage space of the instance.<br> |
|DataBackupAllRetention |Boolean |true |Whether to retain all data backups before releasing the instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|DataBackupEncryptionEnabled |Boolean |true |Specifies whether to enable encryption for data backups for local disk instances. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br>> Cloud disk instances currently do not support this feature.<br> |
|DataBackupRetentionDay |Integer |7 |Number of days to retain data backups, value range: 7~3650. The default retention period is 7 days. |
|DataFullBackupPeriods |Array of String |["Monday","Wednesday","Friday",Sunday"] |Full backup cycle. Values:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday. |
|DataFullBackupStartUTCHour |Integer |16 |The start time of the full backup window in UTC. The time window is 1 hour.<br><br>> **tip**<br><br><br>> DataFullBackupStartUTCHour and DataFullBackupTime can both be used to specify the full backup period of an instance. DataFullBackupStartUTCHour has a higher priority. If both of these fields are returned, the value of DataFullBackupStartUTCHour is used.<br> |
|DataFullBackupTime |String |18:00Z\-19:00Z |The time window to perform backup tasks is 1 hour. Format: HH:mmZ\-HH:mmZ (UTC time).<br><br>> **tip**<br><br><br>> Both DataFullBackupStartUTCHour and DataFullBackupTime can be used to specify the full backup period for the instance. DataFullBackupStartUTCHour has a higher priority. If both of these fields are returned, the value of DataFullBackupStartUTCHour is used.<br> |
|DataKeepDaysAfterReleased |Integer |7 |Number of days to retain the backup after the instance is released. |
|DataKeepPolicyAfterReleased |String |Last |The policy for retaining instance backups after the instance is released. Values are:<br><br><br>* `Last`: Retain the final backup. Default value.<br><br>* `All`: Retain all instance backups.<br><br>* `None`: Do not retain backups. |
|DataIncrBackupPeriods |Array of String |["Monday","Wednesday","Friday","Sunday"] |The cycle for incremental backups for local disk instances. The values are:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday.<br><br><br>> **tip**<br><br><br>> This field is not returned when high frequency incremental backup is enabled (when HourlyIncrBackupEnable is `true`).<br> |
|HighFrequencySnapshotBackupEnable |Boolean |false |Indicates whether high frequency incremental snapshot backup is enabled for the cloud disk instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br>> If the instance is a local disk instance, this field returns `false`.<br> |
|HighFrequencySnapshotBackupSecondPeriod |Integer |3600 |The frequency of high\-frequency incremental snapshot backups for the cloud disk instance, in seconds. Values:<br><br><br>* `3600`: Every 1 hour.<br><br>* `7200`: Every 2 hours.<br><br>* `10800`: Every 3 hours.<br><br>* `14400`: Every 4 hours.<br><br>* `19200`: Every 6 hours.<br><br>* `28800`: Every 8 hours.<br><br>* `38400`: Every 12 hours.<br><br><br>> **tip**<br><br><br>> If the instance is a local disk instance or the high\-frequency incremental snapshot backup feature for the cloud disk instance is disabled, this field returns `0`.<br> |
|HourlyIncrBackupEnable |Boolean |true |Specifies whether to enable high frequency back up for local disk instances. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|IncrBackupHourPeriod |Integer |2 |The high\-frequency incremental backup frequency for local disk instances. Values:<br><br><br>* `0`: Don't perform high frequency incremental backup. In this case, HourlyIncrBackupEnable is `false`.<br><br>* `2`: Performs an incremental backup every 2 hours.<br><br>* `4`: Performs an incremental backup every 4 hours.<br><br>* `6`: Performs an incremental backup every 6 hours.<br><br>* `12`: Performs an incremental backup every 12 hours. |
|InstanceId |String |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|KeepCrossBackupEnableAfterReleased |Boolean |false |Specifies whether to enable cross\-regional backup. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|LockDDLTime |Integer |30 |DDL maximum wait time. The default value is 30, the minimum value is 10, and the maximum value is 1440. The unit is minutes. |
|LockDDLTimeSecond |Integer |3600 |DDL maximum wait time. The default value is 1800, the minimum value is 1, and the maximum value is 86400. The unit is seconds.<br><br>> **tip**<br><br><br><br>* > The backup process blocks DDL. If the blocking time exceeds the specified time, the backup automatically stops.<br><br><br>* > Only MySQL 8.0 instances support this setting.<br> |
|LogBackupRetentionDay |Integer |7 |Binlog backup retention period. Value range: 7\-3650 days.<br><br>> **tip**<br><br><br>> This parameter is not returned when RetentionPolicySynced is `true`.<br> |
|PublicDownloadEnable |Boolean |true |Specifies whether to allow downloading instance backup data from the public network. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|RetentionPolicySynced |Boolean |true |Whether the retention policy for log backup is consistent with the retention policy for data backup. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |

## Sample

### Sample request

```json
POST /?Action=ModifyBackupPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-cf4f3ddc****",
    "BinlogBackupAllRetention": false,
    "BinlogBackupEnabled": true,
    "BinlogBackupEncryptionEnabled": true,
    "BinlogFileCountsEnable": true,
    "BinlogLimitCount": 600,
    "BinlogLocalRetentionHour": 128,
    "BinlogSpaceLimitEnable": false,
    "BinlogStoragePercentage": 20,
    "DataBackupAllRetention": true,
    "DataBackupEncryptionEnabled": false,
    "DataBackupRetentionDay": 10,
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
    "IncrBackupHourPeriod": 6,
    "LockDDLTimeSecond": 1800,
    "LogBackupRetentionDay": 10,
    "RetentionPolicySynced": true
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241015210719E87A7B5DA6C5F6BD7795-eab62a",
        "Action": "ModifyBackupPolicy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "BinlogBackupAllRetention": true,
        "BinlogBackupEnabled": true,
        "BinlogBackupEncryptionEnabled": true,
        "BinlogFileCountsEnable": true,
        "BinlogLimitCount": 600,
        "BinlogLocalRetentionHour": 128,
        "BinlogSpaceLimitEnable": false,
        "BinlogStoragePercentage": 20,
        "DataBackupAllRetention": true,
        "DataBackupEncryptionEnabled": false,
        "DataFullBackupPeriods": [
            "Monday",
            "Tuesday",
            "Wednesday"
        ],
        "DataFullBackupStartUTCHour": 16,
        "DataFullBackupTime": "16:00Z-16:59Z",
        "DataKeepDaysAfterReleased": 7,
        "DataKeepPolicyAfterReleased": "All",
        "HighFrequencySnapshotBackupEnable": false,
        "HighFrequencySnapshotBackupSecondPeriod": 0,
        "HourlyIncrBackupEnable": true,
        "IncrBackupHourPeriod": 6,
        "InstanceId": "mysql-cf4f3ddc****",
        "LockDDLTimeSecond": 1800,
        "LogBackupRetentionDay": 7,
        "PublicDownloadEnable": true,
        "RetentionPolicySynced": true
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
