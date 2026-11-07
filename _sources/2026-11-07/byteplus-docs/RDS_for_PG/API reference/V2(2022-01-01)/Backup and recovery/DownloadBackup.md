---
title: "DownloadBackup"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadBackup"
---

Call the DownloadBackup API to download a backup.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After calling this API, the preparation for downloading the target backup file is completed. Then, you need to call the [GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_PG/GetBackupDownloadLink) API to obtain the download link, and finally download the file using that link.

* Only downloading logical backups is supported.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-a3e7eb2f\*\*\*\* |Instance ID. |
|BackupId |String |Yes |20250512\-194654\-3836LI |ID of the logical backup to download |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DownloadBackup&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-a3e7eb2f****",
    "BackupId": "20250512-194654-3836LI"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250512220201C4DF75445E6A5077C0C9-02b7b8",
        "Action": "DownloadBackup",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
