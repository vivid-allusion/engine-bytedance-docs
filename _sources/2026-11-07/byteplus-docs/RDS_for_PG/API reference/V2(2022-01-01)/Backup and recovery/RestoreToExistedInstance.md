---
title: "RestoreToExistedInstance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/RestoreToExistedInstance"
---

Call the RestoreToExistedInstance API to restore data to an existing instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Currently, you can only restore data to an existing instance from a logical backup

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|BackupId |String |Yes |20250512\-194554\-792LD |Backup ID used for restoration. |
|SourceDBInstanceId |String |Yes |postgres\-a3e7eb2f\*\*\*\* |Instance ID to which the backup belongs. |
|TargetDBInstanceId |String |Yes |postgres\-a3e7eb2f\*\*\*\* |Target instance ID for restoration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The values of SourceDBInstanceId and TargetDBInstanceId can be the same. If the values of SourceDBInstanceId and TargetDBInstanceId are the same, data will be restored to the source instance.</div><br> |
|TargetDBInstanceAccount |String |Yes |Admin |The account that will serve as the owner of the newly restored database in the target instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only super accounts that are not disabled from DDL operations can be selected.</div><br> |
|Databases |Array of [RestoreDatabaseObject](https://docs.byteplus.com/en/docs/61/48143#restoredatabaseobject) |Yes |Refer to the sample response. |Information about the database to restore.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can choose up to 50 databases for recovery at a time.</div><br> |


<span id="restoredatabaseobject"></span>
### RestoreDatabaseObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DBName |String |Yes |DatabaseName |Original database name. |
|NewDBName |String |Yes |DatabaseName_restored |New database name. The database name must meet the following rules. If not met, the restoration task cannot be initiated.<br><br><br>* The name is unique within the instance.<br><br>* The name length is limited to 2–63 characters.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* Some reserved words or keywords cannot be used in the database name. Refer to [Reserved keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords) for all reserved keywords. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=RestoreToExistedInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "BackupId": "20250512-194554-792LD",
    "SourceDBInstanceId": "postgres-a3e7eb2f****",
    "TargetDBInstanceId": "postgres-a3e7eb2f****",
    "TargetDBInstanceAccount": "Admin",
    "Databases": [
        {
            "DBName": "DatabaseName",
            "NewDBName": "DatabaseName_restored"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202505122228285485938EED274336A199-20bd59",
        "Action": "RestoreToExistedInstance",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
