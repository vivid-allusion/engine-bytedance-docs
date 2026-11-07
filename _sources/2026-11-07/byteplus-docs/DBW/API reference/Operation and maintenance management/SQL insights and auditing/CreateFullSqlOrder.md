---
title: "CreateFullSqlOrder"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/CreateFullSqlOrder"
---

Call the CreateFullSqlOrder API to create a full SQL subscription order for the specified instance.

<span id="M6BoYOgB"></span>
## Request type

Synchronous request

<span id="grzZroua"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|FollowInstanceID |String |Yes |mysql\-cf8d83\*\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?lang=en">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL. |
|Ttl |Integer |Yes |30 |The total number of days to retain Full SQL data. The value is the sum of the `HotStorageDays` and `ColdStorageDays` parameters. |
|LogProductType |String |Yes |FullSqlLog |The source type of the log. Valid values:<br><br><br>* `FullSqlLog`: Full SQL log.<br><br>* `ProxyFullSqlLog`: Proxy full SQL log. |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|CustomStorageSqlMethods |Array of string<br><br> |Yes |```JSON```<br>```[```<br>```    "SELECT",```<br>```    "INSERT",```<br>```    "UPDATE",```<br>```    "DELETE",```<br>```    "ALTER",```<br>```    "CREATE",```<br>```    "DROP",```<br>```    "RENAME",```<br>```    "TRUNCATE",```<br>```    "OTHER"```<br>```]```<br> |SQL types that are collected and stored.<br><br>Values include: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `ALTER`, `CREATE`, `DROP`, `RENAME`, `TRUNCATE`, `OTHER`.<br><br> |
|LabelType |String |Yes |ConsumeTls |Deployment tag type, currently only supports `ConsumeTls` values. |
|DefaultCloseType |String |No |CloseAuditCollectAndTls |Close method. Currently, only the `CloseAuditCollectAndTls` value is supported. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#q8Dcvm5A) |No |```JSON```<br>```[```<br>```    {```<br>```        "Key": "env",```<br>```        "Value": "prod"```<br>```    }```<br>```]```<br> |Tags are used to mark resources to facilitate searching and resource aggregation. |
|EnableFunctions |RegionEnableFunctions<br><br> |No |```JSON```<br>```{```<br>```    "SQLAuditDetail": true,```<br>```    "SQLInsight": true,```<br>```    "EnableHierarchicalStorage": true```<br>```}```<br> |Function switches supported in the current region.<br><br> |
|HotStorageDays |Integer |No |7 |Standard storage days. The value range is 1 to 1095. |
|ColdStorageDays |Integer |No |23 |Infrequent\-access retention period, ranging from 30 to 3648 days. Default value: 30. |


<span id="EVLGJHIh"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|AuditServiceID |String |DBW_FullSql_66\*\*\*\*\*\*\-39e1\-4139\-a785\-501a9d\*\*\*\*\*\* |Full SQL service instance ID. |
|OrderID |String |Order2001000022227\*\*\*\*\*\* |Billing order ID. |


<span id="a0xrgDeO"></span>
## Request example

```JSON
POST /?Action=CreateFullSqlOrder&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
    "FollowInstanceID": "mysql-cf8d83******",
    "InstanceType": "MySQL",
    "RegionId": "cn-beijing",
    "Ttl": 31,
    "LabelType": "ConsumeTls",
    "DefaultCloseType": "CloseAuditCollectAndTls",
    "LogProductType": "FullSqlLog",
    "CustomStorageSqlMethods": [
        "SELECT",
        "INSERT",
        "UPDATE",
        "DELETE",
        "ALTER",
        "CREATE",
        "DROP",
        "RENAME",
        "TRUNCATE",
        "OTHER"
    ],
    "Tags": [
        {
            "Key": "dbw_auto_team",
            "Value": "qa"
        }
    ],
    "EnableFunctions": {
        "SQLAuditDetail": true,
        "SQLInsight": true,
        "EnableHierarchicalStorage": true
    },
    "HotStorageDays": 1,
    "ColdStorageDays": 30
}
```


<span id="h1QLYwDg"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260824144406F0D34313ECD148E4432A-d95d25",
        "Action": "CreateFullSqlOrder",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "AuditServiceID": "DBW_FullSql_66******-39e1-4139-a785-501a9d******",
        "OrderID": "Order2001000022227******"
    }
}
```


<span id="5pEK9Cqm"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
