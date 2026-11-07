---
title: "DescribeWALLogBackups"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeWALLogBackups"
---

Call the DescribeWALLogBackups API to obtain the list of backed\-up WAL logs for the specified instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-08f97473\*\*\*\* |Instance ID. |
|BackupId |String |No |00000005000000010000000C |Backup file ID. |
|StartTime |String |No |2025\-12\-01T13:00:00Z |Start time of the query time range, formatted as `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Based on the backup end time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Default value. If this field is not specified, all backups limited by other query conditions are returned.</div><br> |
|EndTime |String |No |2025\-12\-01T14:03:19Z |End time of the query time range, formatted as `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Based on the backup end time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Default value. If this field is not specified, all backups limited by other query conditions are returned.</div><br> |
|PageSize |Integer |No |5 |The number of records on each page. The value must be greater than 0 and no more than 1,000. The default value is 10. |
|PageNumber |Integer |No |2 |Page number. Default value: 1. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |123 |Total number of WAL backups matching the query conditions. |
|WALLogBackups |Array of [WALLogBackupObject](https://docs.byteplus.com/en/docs/61/78964#wallogbackupobject) |Refer to the sample response. |WAL backup list. |


<span id="wallogbackupobject"></span>
### WALLogBackupObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BackupFileSize |Long |74628 |WAL backup file size. Unit: Byte. |
|BackupId |String |00000005000000010000000F |WAL backup ID. |
|BackupStatus |String |Success |WAL backup state. |
|Checksum |String |c2001709ecf649523647ed33ebf8748a |Checksum value in ETag format using the crc64 algorithm. |
|DownloadStatus |String |Success |Downloadable state of WAL backup, currently fixed as `LinkReady`, meaning it is ready for immediate download. |
|ProjectName |String |default |Project to which the WAL backup instance belongs. |
|WALLogBackupEndTime |String |2025\-12\-01T13:49:17Z |End time of WAL backup, formatted as `yyyy-MM-ddTHH:mm:ssZ` (UTC time). |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeWALLogBackups&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-08f97473****",
    "StartTime": "2025-12-01T13:00:00Z",
    "EndTime": "2025-12-01T14:03:19Z",
    "PageSize": 5,
    "PageNumber": 2
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20251201220740ADE6D1BCB10B962FA0FF-71630a",
        "Action": "DescribeWALLogBackups",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "Total": 14,
        "WALLogBackups": [
            {
                "BackupFileSize": 77466,
                "BackupId": "00000005000000010000000C",
                "BackupStatus": "Success",
                "Checksum": "f75a840de3df79b9e0a04695448578f2",
                "DownloadStatus": "LinkReady",
                "ProjectName": "test01",
                "WALLogBackupEndTime": "2025-12-01T13:34:17Z"
            },
            {
                "BackupFileSize": 71018,
                "BackupId": "00000005000000010000000B",
                "BackupStatus": "Success",
                "Checksum": "0e25006939f856ed0883294d92bb272d",
                "DownloadStatus": "LinkReady",
                "ProjectName": "test01",
                "WALLogBackupEndTime": "2025-12-01T13:29:17Z"
            },
            {
                "BackupFileSize": 71006,
                "BackupId": "00000005000000010000000A",
                "BackupStatus": "Success",
                "Checksum": "8b848a7f356df12e6153a085789c4c17",
                "DownloadStatus": "LinkReady",
                "ProjectName": "test01",
                "WALLogBackupEndTime": "2025-12-01T13:24:17Z"
            },
            {
                "BackupFileSize": 71036,
                "BackupId": "000000050000000100000009",
                "BackupStatus": "Success",
                "Checksum": "b062ddaa03400f9f749f1a7f53c37b79",
                "DownloadStatus": "LinkReady",
                "ProjectName": "test01",
                "WALLogBackupEndTime": "2025-12-01T13:19:18Z"
            },
            {
                "BackupFileSize": 70728,
                "BackupId": "000000050000000100000008",
                "BackupStatus": "Success",
                "Checksum": "bd096a95530e1083168ea39e8b6332c6",
                "DownloadStatus": "LinkReady",
                "ProjectName": "test01",
                "WALLogBackupEndTime": "2025-12-01T13:14:18Z"
            }
        ]
    }
}
```
