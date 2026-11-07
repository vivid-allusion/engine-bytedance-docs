---
title: "DescribeDatabases"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedatabases"
---

Call the DescribeDatabases API to query a list of databases.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|DBName |String |No |testdb1 |Database name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When no value or an empty value is passed, all databases under the specified instance will be queried.</div><br> |
|PageNumber |Integer |No |1 |The query offset of the current page. The default value is 1. |
|PageSize |Integer |No |10 |The number of records on each page. The value must be greater than 0 and no more than 1,000. The default value is 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of databases. |
|Databases |Array of [DatabaseObject](https://docs.byteplus.com/en/docs/61/15727#databaseobject) |Refer to the sample response. |Database list. |


<span id="databaseobject"></span>
### DatabaseObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CharacterSetName |String |utf8 |Database character set. |
|Collate |String |en_US.utf8 |Sorting rules. Default value: `C`. Range:<br><br>`C`, `C.UTF-8`, `en_US.utf8`, and `zh_CN.utf8`. |
|CType |String |en_US.utf8 |Character category. Default value: `C`. Range:<br><br>`C`, `C.UTF-8`, `en_US.utf8`, and `zh_CN.utf8`. |
|DBName |String |db1 |Database name. |
|DBStatus |String |Available |Database state:<br><br><br>* `Not available`: not available.<br><br>* `Available`: available. |
|Owner |String |testuser |Database owner.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Read\-only accounts, super or normal accounts with DDL privileges disabled, cannot serve as the owner of a database.</div><br> |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDatabases&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
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
        "RequestId": "2023080216495355289C8C837799FC33EF",
        "Action": "DescribeDatabases",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Databases": [
            {
                "CType": "en_US.utf8",
                "CharacterSetName": "utf8",
                "Collate": "en_US.utf8",
                "DBName": "testdb1",
                "DBStatus": "Available",
                "Owner": "pg_rds_superuser"
            }
        ],
        "Total": 1
    }
}
```
