---
title: "DownloadBackup"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloadbackup"
---

Call the DownloadBackup API to download a backup.

## Request type

Asynchronous request.

## Precautions

* After calling this API, the preliminary work for downloading the target backup file is completed. Subsequently, you need to call the [GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_MySQL/getbackupdownloadlink)API to obtain the download link for the target backup file, and finally use the download link to perform the file download.

* Downloading backups of cloud disk instances is not currently supported.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-ce48081d\*\*\*\* |Instance ID. |
|BackupId |String |Yes |BackupId example: f1f2284117a344a38370c37b841fec75FileName example: binlog\-1683420632178737071\-binlog.000044 |* If downloading a data backup, this field's value is the BackupId of the backup file, which can be obtained by calling the [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) API.<br><br>* If downloading a Binlog backup, this field's value is the FileName of the backup file, which can be obtained by calling the [DescribeBinlogFiles](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebinlogfiles) API.<br><br><br>tip<br><br>When batch downloading Binlog backups, separate multiple FileNames with English commas (,). |

## Response parameters

null

## Sample request

```json
POST /?Action=DownloadBackup&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-ce48081d****",
    "BackupId": "af04547b456d4ec8aa6055d760c4****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230111114055BB2E1564F40B9F6C932F",
        "Action": "DownloadBackup",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
