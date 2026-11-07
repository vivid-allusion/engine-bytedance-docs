---
title: "CloneDatabase"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/CloneDatabase"
---

Call the CloneDatabase API to clone an existing database.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only one clone database task can exist under an instance.

* A maximum of 2,000 databases can be created under one instance. When the number of database instances has reached 2,000, the database cannot be cloned.

* Only databases with no more than 1,000 cloned tables are supported.

* During the process of cloning a database, you cannot perform DDL operations on the database.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-a3e7eb2f\*\*\*\* |Instance ID. |
|SourceDBName |String |Yes |database |Source database name. |
|NewDBName |String |No |database_clone |Set the name of the new database. The Database name must follow these rules:<br><br><br>* The name is unique within the instance.<br><br>* The name length is limited to 2–63 characters.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* Some reserved words or keywords cannot be used in the database name. Refer to [Reserved keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords) for all reserved keywords.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not set, the new database is named by default with the <code>source database name</code> + <code>_clone_</code> + <code>timestamp</code>.</div><br> |
|DataOption |String |No |Metadata |Currently, only cloning the database structure is supported, and the value must be set to `Metadata`. |
|PLPGSQLOption |String |No |View,Procedure |PL/pgSQL options for cloning a database. Multiple values are allowed, separated by commas (,).<br><br><br>* `Views`: views.<br><br>* `Stored procedures`: stored procedures.<br><br>* `Functions`: functions.<br><br>* `Triggers`: triggers. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CloneDatabase&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-a3e7eb2f****",
    "SourceDBName": "database",
    "NewDBName": "database_clone",
    "DataOption": "Metadata",
    "PLPGSQLOption": "View,Procedure"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025050718082836C31DDC1C9EEA9716A6-2ac462",
        "Action": "CloneDatabase",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijijng"
    },
    "Result": null
}
```
