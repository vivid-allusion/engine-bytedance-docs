---
title: "GetBackupDownloadLink"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/GetBackupDownloadLink"
---

Call the GetBackupDownloadLink API to obtain the download link of the backup.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only backups in the region to which the download request is sent are allowed for download.

* If all returned field values are empty after calling this interface, call the [DownloadBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadBackup) API to trigger the prerequisite for download.

* Currently, only logical backups can be downloaded.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-a3e7eb2f\*\*\*\* |Instance ID. |
|BackupId |String |Yes |20250512\-194654\-3836LI |ID of the logical backup to download |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BackupDescription |String |This is a description of the backup set. |Backup set description. |
|BackupDownloadLink |String |Refer to the sample response. |Public network download URL of the backup. |
|BackupFileName |String |postgres\-a3e7eb2f\*\*\*\*\-20250512\-194654\-3836LI.zip |Backup filename. |
|BackupFileSize |Long |1024 |Backup file size in bytes. |
|BackupId |String |20250512\-194654\-3836LI |Backup ID. |
|BackupMethod |String |Logical |Backup type. Values:<br><br><br>* `Physical`: Physical backup. Default value.<br><br>* `Logical`: Logical backup.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When BackupScope is set to <code>Database</code>, BackupMethod can only be set to <code>Logical</code>.</div><br> |
|InnerBackupDownloadLink |String |Refer to the sample response. |Private network download URL of backup. |
|InstanceId |String |postgres\-a3e7eb2f\*\*\*\* |Instance ID. |
|LinkExpiredTime |String |2025\-05\-19T14:03:27.603Z |Download URL expiration time, in the format `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|PrepareProgess |Integer |100 |Backup file preparation progress. After calling [downloadBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadBackup) to start pre\-download, use this parameter to check the backup file preparation progress. Unit: %. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=GetBackupDownloadLink&Version=2022-01-01 HTTP/1.1
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
        "RequestId": "20250512220327F839DCF033BA01385243-18218e",
        "Action": "GetBackupDownloadLink",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupDescription": "",
        "BackupDownloadLink": "https://for-cq-boe-rdspg-backup.tos-s3-cn-beijing.volces.com/backrestrepo/postgres-a3e7eb2f****-backrest-shared-repo/logical-backup/20250512-194654-3836LI/postgres-a3e7eb2f****-20250512-194654-3836LI.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKLTYThjOGU3ZmYwMTFlNGQ5YmEwMGI5ZTdmZWIzMTA****%2F20250512%2Fcn-beijing%2Fs3%2Faws4_request&X-Amz-Date=20250512T140327Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=18bd7c43d730771444a6778fff78ae44beeac7f69f981c393e3622e8f0ec****",
        "BackupFileName": "postgres-a3e7eb2f****-20250512-194654-3836LI.zip",
        "BackupFileSize": 32093,
        "BackupId": "20250512-194654-3836LI",
        "BackupMethod": "Logical",
        "InnerBackupDownloadLink": "https://for-cq-boe-rdspg-backup.s3.cn-beijing.amazonaws.com/backrestrepo/postgres-a3e7eb2f****-backrest-shared-repo/logical-backup/20250512-194654-3836LI/postgres-a3e7eb2f****-20250512-194654-3836LI.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKLTYThjOGU3ZmYwMTFlNGQ5YmEwMGI5ZTdmZWIzMTA****%2F20250512%2Fcn-beijing%2Fs3%2Faws4_request&X-Amz-Date=20250512T140327Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=aa896c51b45ccc307c5b1d7d432e42781b8f96950852b97207d6e767f30c****",
        "InstanceId": "postgres-a3e7eb2f****",
        "LinkExpiredTime": "2025-05-19T14:03:27.603Z",
        "PrepareProgess": 100
    }
}
```
