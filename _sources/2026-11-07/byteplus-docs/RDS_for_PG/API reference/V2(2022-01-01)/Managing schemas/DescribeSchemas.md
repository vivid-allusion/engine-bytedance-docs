---
title: "DescribeSchemas"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describeschemas"
---

Call the DescribeSchemas API to query a list of schemas.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|DBName |String |No |testdb |Database name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If no value or an empty value is provided, all schemas under the specified instance will be queried.</div><br> |
|PageNumber |Integer |No |1 |The query offset of the current page. The default value is 1. |
|PageSize |Integer |No |10 |The number of records on each page. The value must be greater than 0 and no more than 1,000. The default value is 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of schemas. |
|Schemas |Array of [SchemaObject](https://docs.byteplus.com/en/docs/61/15754#schemaobject) |Refer to the Sample response. |Schema list. |


<span id="schemaobject"></span>
### SchemaObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBName |String |testdb |Database name. |
|SchemaName |String |testschema |Schema name under the database. |
|Owner |String |testuser |Schema owner.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Instance read\-only accounts, super accounts or normal accounts with DDL privileges disabled cannot be used as database owners.</div><br> |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeSchemas&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "DBName": "testdb1",
    "InstanceId": "postgres-ca7b7019****",
    "PageSize": 10,
    "PageNumber": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308041039157B21482F51ABF9041021",
        "Action": "DescribeSchemas",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Schemas": [
            {
                "DBName": "testdb1",
                "Owner": "postgres",
                "SchemaName": "pg_catalog"
            },
            {
                "DBName": "testdb1",
                "Owner": "postgres",
                "SchemaName": "information_schema"
            },
            {
                "DBName": "testdb1",
                "Owner": "pg_rds_superuser",
                "SchemaName": "public"
            },
            {
                "DBName": "testdb1",
                "Owner": "yy_123",
                "SchemaName": "testschema"
            }
        ],
        "Total": 4
    }
}
```
