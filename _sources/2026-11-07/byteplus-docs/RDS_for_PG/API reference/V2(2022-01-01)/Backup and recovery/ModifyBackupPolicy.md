---
title: "ModifyBackupPolicy"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifybackuppolicy"
---

Call the ModifyBackupPolicy API to modify the backup policy.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* To disable incremental backup, set the request parameter DataIncrBackupPeriods to an empty string and set the request parameter HourlyIncrBackupEnable to `false`.

* If a non\-empty valid value is passed to the request parameter DataIncrBackupPeriods and `true` is passed to the request parameter HourlyIncrBackupEnable at the same time, the instance’s incremental backup method will be high\-frequency incremental backup.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|BackupRetentionPeriod |Integer |No |7 |Backup retention days, with a range of 7 to 365.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Default value. If this parameter is not provided, the original setting remains unchanged.</div><br> |
|FullBackupTime |String |No |00:00Z\-01:00Z |The time to execute the backup task. Format: `HH:mmZ-HH:mmZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Default value. If this parameter is not provided, the original setting remains unchanged.</div><br> |
|FullBackupPeriod |String |No |Monday |Full backup cycle. Multiple values separated by commas (,). Values:<br><br><br>* `Monday`: Monday<br><br>* `Tuesday`: Tuesday<br><br>* `Wednesday`: Wednesday<br><br>* `Thursday`: Thursday<br><br>* `Friday`: Friday<br><br>* `Saturday`: Saturday<br><br>* `Sunday`: Sunday<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">No default value. If this parameter is not provided, the original setting remains unchanged.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Select at least one day a week for full backup.</div><br> |
|WALLogSpaceLimitEnable |Boolean |No |false |Local remaining available space protection state. After enabling this feature, the instance automatically clears the earliest local WAL log when the total storage space usage exceeds 80% or the remaining space is less than 5GB, until usage drops below 80% and the remaining space exceeds 5GB. value range:<br><br><br>* `true`: enable.<br><br>* `false`: disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Default value. If this parameter is not provided, the original setting remains unchanged.</div><br> |
|DataIncrBackupPeriods |String |No |Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday |The backup frequency when the incremental backup method is normal frequency. Multiple values are separated by commas (,). Values:<br><br><br>* `Monday`: Monday<br><br>* `Tuesday`: Tuesday<br><br>* `Wednesday`: Wednesday<br><br>* `Thursday`: Thursday<br><br>* `Friday`: Friday<br><br>* `Saturday`: Saturday<br><br>* `Sunday`: Sunday<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The value cannot overlap with the full backup cycle.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can select up to six days per week for incremental backup.</div><br> |
|HourlyIncrBackupEnable |Boolean |No |true |Specifies whether to enable high\-frequency backup. Value:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">No default value. If this parameter is not provided, the original setting remains unchanged.</div><br> |
|IncrementBackupFrequency |Integer |No |2 |Backup frequency when the incremental backup method is high\-frequency. Values can be `1`, `2`, `4`, `6` or `12`. Unit: hours.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Default value. If this parameter is not provided, the original setting remains unchanged.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is valid only when HourlyIncrBackupEnable is <code>true</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyBackupPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "BackupRetentionPeriod": 8,
    "FullBackupPeriod": "Monday,Wednesday,Friday",
    "FullBackupTime": "02:00Z-03:00Z",
    "HourlyIncrBackupEnable": true,
    "IncrementBackupFrequency": 4,
    "WALLogSpaceLimitEnable": false
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023080411191113E74BF9DC0908068A0B",
        "Action": "ModifyBackupPolicy",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
