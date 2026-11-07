---
title: "DescribeBackupPolicy"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describebackuppolicy"
---

Call the DescribeBackupPolicy API to query the backup policy.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BackupRetentionPeriod |Integer |7 |Backup retention days. Value range: 7\-365. |
|DataIncrBackupPeriods |String |Tuesday,Thursday |Backup frequency when the backup method is normal frequency. Separate multiple values with commas (,). Values:<br><br><br>* `Monday`: Monday<br><br>* `Tuesday`: Tuesday<br><br>* `Wednesday`: Wednesday<br><br>* `Thursday`: Thursday<br><br>* `Friday`: Friday<br><br>* `Saturday`: Saturday<br><br>* `Sunday`: Sunday<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is not returned if incremental backup is not enabled on the instance.</div><br> |
|FullBackupTime |String |02:00Z\-03:00Z |The time to execute the backup task. Format: `HH:mmZ-HH:mmZ` (UTC time). |
|FullBackupPeriod |String |Monday,Wednesday,Friday,Sunday |Full backup cycle. At least one day must be specified per week. Separate multiple values with commas (,). Values:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday. |
|HourlyIncrBackupEnable |Boolean |false |Specifies whether to enable high\-frequency backup. Value:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|IncrementBackupFrequency |Integer |2 |Backup frequency when the incremental backup method is high\-frequency. Values can be `1`, `2`, `4`, `6` or `12`. Unit: hours.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is valid only when HourlyIncrBackupEnable is <code>true</code>.</div><br> |
|InstanceId |String |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|WALLogSpaceLimitEnable |Boolean |false |Local remaining available space protection state. After enabling this feature, the instance automatically clears the earliest local WAL log when the total storage space usage exceeds 80% or the remaining space is less than 5GB, until usage drops below 80% and the remaining space exceeds 5GB. value range:<br><br><br>* `true`: enable.<br><br>* `false`: disabled. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeBackupPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230804110353F956004F62ACD50597D6",
        "Action": "DescribeBackupPolicy",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupRetentionPeriod": 7,
        "DataIncrBackupPeriods": "Tuesday",
        "FullBackupPeriod": "Monday,Wednesday,Friday",
        "FullBackupTime": "18:00Z-19:00Z",
        "HourlyIncrBackupEnable": false,
        "IncrementBackupFrequency": 12,
        "InstanceId": "postgres-36cd1f06e9f3",
        "WALLogSpaceLimitEnable": false
    }
}
```
