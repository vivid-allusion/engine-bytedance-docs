---
title: "PreCheckCreateFullSql"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/PreCheckCreateFullSql"
---

Call the PreCheckCreateFullSql API to enable full SQL insight.

<span id="1OhLLW17"></span>
## Request type

Synchronous request

<span id="dOWWKqPC"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|FollowInstanceID |String |Yes |mysql\-cf8d83\*\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?lang=en">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br> |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL. |
|RegionId |String |Yes |cn\-beijing |Region ID. |


<span id="PvpwxptQ"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|PreCheckEnable |Boolean |true |Is full SQL insight enabled? The values are as follows:<br><br><br>* `true`: Indicates that full SQL is enabled.<br><br>* `false`: Indicates that full SQL is not enabled. |
|PreCheckFailReason |String |Sql insight services are not available in this region |Reason for pre\-check failure. Usually empty and not displayed when the pre\-check passes. |
|RegionEnableFunctions<br><br> |[RegionEnableFunctions](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#QrMPk3Uq) |```JSON```<br>```{```<br>```    "SQLAuditDetail": true,```<br>```    "SQLInsight": true,```<br>```    "EnableHierarchicalStorage": true```<br>```}```<br> |Function switches supported in the current region.<br><br> |


<span id="o81oGA6K"></span>
## Request example

```JSON
POST /?Action=PreCheckCreateFullSql&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "FollowInstanceID": "mysql-cf8d83******",
    "DSType": "MySQL",
    "RegionId": "cn-beijing"
}
```


<span id="tX3krrSz"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260824103224D22523DC654D4EAAD927-e4f168",
        "Action": "PreCheckCreateFullSql",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "PreCheckEnable": true,
        "RegionEnableFunctions": {
            "EnableHierarchicalStorage": true,
            "SQLAuditDetail": true,
            "SQLInsight": true
        }
    }
}
```


<span id="3iiB5HAT"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
