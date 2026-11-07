---
title: "DeleteDataBackup"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedatabackup"
---

Call the DeleteDataBackup API to delete manually created data backups.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This API only supports deleting manually created backup files (Executor: User); it cannot be used to delete automatic backup data (Executor: System).

* Backups in running status cannot be deleted.

* To ensure instance recoverability, the system prohibits deletion of the last full physical backup.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-321b4cbf\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance summary, including the Instance ID.</div><br> |
|BackupId |String |Yes |64f8c02a25324117bc537dc02ca7\*\*\*\* |Backup ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups">DescribeBackups</a> API to query the list of backup files for a specified instance, obtain the backup ID, and confirm the due time of the backup.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DeleteDataBackup&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-321b4cbf****",
    "BackupId": "64f8c02a25324117bc537dc02ca7****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230920150415526CE9EB684703477CC1",
        "Action": "DeleteDataBackup",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
