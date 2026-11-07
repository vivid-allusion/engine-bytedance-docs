---
title: "CreateSchema"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/createschema"
---

Call the CreateSchema API to create a schema.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|DBName |String |Yes |testdb1 |Database name. |
|SchemaName |String |Yes |ThisIsASchemaName |Schema name.<br><br><br>* The name length is limited to 2–63 characters.<br><br>* Consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* Must start with a letter and end with a letter or a digit.<br><br>* Reserved words cannot be used. For all disabled keywords, refer to [disabled keywords](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords).<br><br>* Cannot start the name with `pg_`. |
|Owner |String |Yes |User01 |Schema owner.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Instance read\-only accounts, super accounts or normal accounts with DDL privileges disabled cannot be used as schema owners.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateSchema&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "DBName": "testdb1",
    "SchemaName": "testschema",
    "Owner": "User01"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308041039157B21482F51ABF9040FDC",
        "Action": "CreateSchema",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
