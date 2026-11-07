---
title: "GetBackupDownloadLink"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/getbackupdownloadlink"
---

Call the GetBackupDownloadLink API to obtain the backup download link.

## Request type

Synchronous request.

## Precautions

* Only allows downloading backup files in the region where the request is sent.

* Downloading backups of cloud disk instances is not currently supported.

* If the fields returned after calling this API are empty, you need to first call the [DownloadBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloadbackup)API to trigger the preliminary work for downloading backup files.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-ce48081d\*\*\*\* |Instance ID. |
|BackupId |String |Yes |BackupId example: f1f2284117a344a38370c37b841fec75<br><br>FileName example: binlog\-1683420632178737071\-binlog.000044 |The BackupId or FileName of the backup file in the same region.<br><br><br>* If downloading a data backup, this field should be the BackupId of the backup file, which can be obtained by calling the [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) API.<br><br>* If downloading a Binlog backup, this field should be the FileName of the backup file, which can be obtained by calling the [DescribeBinlogFiles](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebinlogfiles) API.<br><br><br>tip<br><br>When batch obtaining Binlog backup links, separate multiple FileNames with English commas (,). |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|BackupDownloadLink |String |https://rds\-mysql\-inner\-fake.tos\-s3\-cn\-beijing.volces.com/rds/mysql\-c7a79d83\*\*\*\*/mysql\-c7a79d83\*\*\*\*\-sd211\-0/merge/full\-1720687620088031497.qp.xbstream?X\-Amz\-Algorithm=AWS4\-HMAC\-SHA256&X\-Amz\-Credential=AKLTMzI4MTNiZmQ5MzZiNDM1NmEzYmEyM2FmOTY4ODk\*\*\*\*%2F20240715%2Fcn\-beijing%2Fs3%2Faws4_request&X\-Amz\-Date=20240715T100901Z&X\-Amz\-Expires=604800&X\-Amz\-SignedHeaders=host&X\-Amz\-Signature=5ae5708c6dc628598e43eb037382af43724d19edae9b65dc5a3b75bee77e\*\*\*\* |The public network download URL of the backup. |
|BackupFileName |String |full\-16347766163043687\*\*\*\*.xbstream |Backup file name.<br><br>tip<br><br>This field returns a value when downloading log backup files but is empty when downloading data backup files. |
|BackupFileSize |Long |1024 |Backup file size, in bytes. |
|BackupId |String |BackupId example: f1f2284117a344a38370c37b841fec75<br><br>FileName example: binlog\-1683420632178737071\-binlog.000044 |Backup file name or backup ID, consistent with the value passed as the request parameter BackupId. |
|BackupType |String |Full |Backup method. Valid values:<br><br><br>* `Full`: Full backup under physical backup type.<br><br>* `Increment`: Incremental backup under physical backup type.<br><br>* `DumpAll`: Full database backup under logical backup type.<br><br>* `Log`: Log backup. |
|DownloadProgress |Long |10 |Backup file preparation progress, in %. |
|InnerBackupDownloadLink |String |https://rds\-mysql\-inner\-fake.tos\-cn\-beijing.ivolces.com/rds/mysql\-c7a79d83\*\*\*\*/mysql\-c7a79d83\*\*\*\*\-sd211\-0/merge/full\-1720687620088031497.qp.xbstream?X\-Amz\-Algorithm=AWS4\-HMAC\-SHA256&X\-Amz\-Credential=AKLTMzI4MTNiZmQ5MzZiNDM1NmEzYmEyM2FmOTY4ODk\*\*\*\*%2F20240715%2Fcn\-beijing%2Fs3%2Faws4_request&X\-Amz\-Date=20240715T100901Z&X\-Amz\-Expires=604800&X\-Amz\-SignedHeaders=host&X\-Amz\-Signature=e25826b29900310556dc2407ff495fbbc31856e8dfb564a7b67e7d791ec0\*\*\*\* |The private network download URL of the backup. |
|InstanceId |String |mysql\-ce48081d\*\*\*\* |Instance ID. |
|LinkExpiredTime |String |2022\-01\-01T10:10:59.000Z |Download link expiration time, format: `yyyy-MM-dd HH:mm:ss.sssZ`(UTC time). |

## Sample request

```json
POST /?Action=GetBackupDownloadLink&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-ce48081d****",
    "BackupId": "541631e5f0614267a04d63d096a3****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240715180900E9B7EB45E0B20729EC63-811ac0",
        "Action": "GetBackupDownloadLink",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "BackupDownloadLink": "https://rds-mysql-inner-fake.tos-s3-ap-southeast-1.volces.com/rds/mysql-c7a79d83****/mysql-c7a79d83****-sd211-0/merge/full-1720687620088031497.qp.xbstream?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKLTMzI4MTNiZmQ5MzZiNDM1NmEzYmEyM2FmOTY4ODk****%2F20240715%2Fap-southeast-1%2Fs3%2Faws4_request&X-Amz-Date=20240715T100901Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=5ae5708c6dc628598e43eb037382af43724d19edae9b65dc5a3b75bee77e****",
        "BackupFileName": "",
        "BackupFileSize": 0,
        "BackupId": "607da9fc51d042c89b1c17c9eac3006e",
        "BackupType": "Full",
        "DownloadProgress": 100,
        "InnerBackupDownloadLink": "https://rds-mysql-inner-fake.tos-ap-southeast-1.ivolces.com/rds/mysql-c7a79d83****/mysql-c7a79d83****-sd211-0/merge/full-1720687620088031497.qp.xbstream?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKLTMzI4MTNiZmQ5MzZiNDM1NmEzYmEyM2FmOTY4ODk****%2F20240715%2Fap-southeast-1%2Fs3%2Faws4_request&X-Amz-Date=20240715T100901Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=e25826b29900310556dc2407ff495fbbc31856e8dfb564a7b67e7d791ec0****",
        "InstanceId": "mysql-c7a79d83****",
        "LinkExpiredTime": "2024-07-22T10:08:59.000Z"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
