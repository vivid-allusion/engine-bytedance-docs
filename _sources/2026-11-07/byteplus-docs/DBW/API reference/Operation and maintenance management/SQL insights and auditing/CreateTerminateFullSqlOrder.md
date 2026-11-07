---
title: "CreateTerminateFullSqlOrder"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/CreateTerminateFullSqlOrder"
---

Call the CreateTerminateFullSqlOrder API to create a termination order for the specified full SQL instance.

<span id="AGjn5BBC"></span>
## Request type

Synchronous request

<span id="1IBtLFi4"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|FollowInstanceID |String |Yes |mysql\-fcfc2c\*\*\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?lang=en">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br> |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL. |
|CloseType |String |Yes |CloseAuditCollectAndTls |Close method. The values are as follows:<br><br><br>* `OnlyCloseAuditCollect`: Indicates that only audit collection is closed.<br><br>* `CloseAuditCollectAndTls`: Indicates that TLS resources are deleted when audit collection is closed. |
|RegionId |String |Yes |cn\-beijing |Region ID. |


<span id="SlvNGh7f"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|AuditServiceID |String |DBW_FullSql_66\*\*\*\*\*\*\-39e1\-4139\-a785\-501a9d\*\*\*\*\*\* |Full SQL service instance ID. |
|OrderID |String |Order2001000022230\*\*\*\*\*\* |Unsubscribe order ID. |


<span id="CddFUrNe"></span>
## Request example

```JSON
POST /?Action=CreateTerminateFullSqlOrder&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
    "FollowInstanceID": "mysql-fcfc2c*******",
    "DSType": "MySQL",
    "CloseType": "CloseAuditCollectAndTls",
    "RegionId": "cn-beijing"
}
```


<span id="IWbTgtlr"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260824152138729B062387DAF96D4D9F-da74f2",
        "Action": "CreateTerminateFullSqlOrder",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "AuditServiceID": "DBW_FullSql_66******-39e1-4139-a785-501a9d******",
        "OrderID": "Order2001000022230******"
    }
}
```


<span id="6Kwu3ovp"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
