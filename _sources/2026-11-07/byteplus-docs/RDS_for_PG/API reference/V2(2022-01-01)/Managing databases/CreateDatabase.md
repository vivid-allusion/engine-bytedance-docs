---
title: "CreateDatabase"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/createdatabase"
---

Call the CreateDatabase API to create a database.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) API to query a list of instances. |
|DBName |String |Yes |testdb1 |Database name. Naming rules are as follows:<br><br><br>* The name length is limited to 2–32 characters.<br><br>* It consists of letters, digits, underscores, or hyphens.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* Reserved words cannot be used. For the list of all disabled keywords, refer to [Disabled keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords). |
|CharacterSetName |String |No |utf8 |Database character set. Currently supported character sets include `utf8` (default), `latin1`, and `ascii`. |
|Collate |String |No |en_US.utf8 |Sorting rules. Value range: `C` (default), `C.UTF-8`, `en_US.utf8`, `zh_CN.utf8`, and `POSIX`. |
|Owner |String |No |testuser |Database owner.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Instance read\-only accounts, super accounts or normal accounts with DDL privileges disabled cannot be used as database owners.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If no value or an empty value is provided, the field takes the value rds superuser.</div><br> |
|CType |String |No |en_US.utf8 |Character category. Value range: `C` (default), `C.UTF-8`, `en_US.utf8`, `zh_CN.utf8`, and `POSIX`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateDatabase&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "DBName": "testdb1",
    "CharacterSetName": "utf8",
    "Collate": "en_US.utf8",
    "CType": "en_US.utf8"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023080216495255289C8C837799FC33DD",
        "Action": "CreateDatabase",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
