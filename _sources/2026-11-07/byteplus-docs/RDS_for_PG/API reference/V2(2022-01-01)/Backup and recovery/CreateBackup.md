---
title: "CreateBackup"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/createbackup"
---

Call the CreateBackup API to create a data backup.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|BackupScope |String |No |Database |Backup target. Values:<br><br><br>* `Entire instance`. Default value.<br><br>* `Database`: specified databases. |
|BackupMethod |String |No |Logical |Backup type. Values:<br><br><br>* `Physical`: Physical backup. Default value.<br><br>* `Logical`: Logical backup.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When BackupScope is set to <code>Database</code>, BackupMethod can only be set to <code>Logical</code>.</div><br> |
|BackupType |String |No |Full |Backup type, values:<br><br><br>* `Full`: full backup (default).<br><br>* `Increment`: incremental backup. |
|BackupDescription |String |No |This is a description of the backup set. |Add a description of the backup set for subsequent management of backups. Supports up to 256 characters. |
|BackupMeta |Array of [BackupMetaObject](https://docs.byteplus.com/en/docs/61/15719#backupmetaobject) |No |Refer to the request example. |Specify databases to back up.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only when BackupScope is set to <code>Database</code>.</div><br> |


<span id="backupmetaobject"></span>
### BackupMetaObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DBName |String |Yes |database1 |Name of the database to be backed up.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can choose up to 2000 databases.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A single backup can support up to 50,000 tables (the sum of all tables in the selected database).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Backing up databases with more than 1000 tables is not supported yet.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BackupId |String |20250512\-180204\-3157LD |Backup ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only when BackupMethod is set to <code>Logical</code>. When SlotType is set to <code>physical</code>, this field returns<code>null</code>。</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateBackup&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-21a3333b****",
    "BackupScope": "Database",
    "BackupMethod": "Logical",
    "BackupDescription": "This is a description of the backup set.",
    "BackupMeta": [
        {
            "DBName": "database1"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230804111113B068599C4088F905B8EB",
        "Action": "CreateBackup",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupId": "20250512-194654-3836LI"
    }
}
```
