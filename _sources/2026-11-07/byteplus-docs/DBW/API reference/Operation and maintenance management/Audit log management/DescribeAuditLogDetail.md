---
title: "DescribeAuditLogDetail"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/describeauditlogdetail"
---

Calls the DescribeAuditLogDetail API to query the detailed information of audit logs.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID. |
|InstanceId |String |Yes |mysql\-71dffd\*\*\*\*\*\*<br><br> |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.1926_7610615829733918244&lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?_vtm_=a106466.b106468.0_0.0_0.0.1926_7610615829733918244&lang=en">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/redis/describedbinstances?lang=en">DescribeDBInstances</a> API to query basic information about Redis instances.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of Document Database for MongoDB.</div><br> |
|InstanceType |String |Yes |MySQL |Database type. The current value can only be:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB MySQL.<br><br>* `Postgres`: RDS for PostgreSQL.<br><br>* `Redis`: Cache for Redis. |
|StartTime |Integer |Yes |1782111588 |The start time for querying database audit logs, in Unix timestamp (seconds) format. |
|EndTime |Integer |Yes |1782197988 |The end time for querying database audit logs, in second timestamp format. |
|LogVersion |String<br><br> |No |V2 |The version of the database audit log. Valid values include **V1** (Default value) and **V2**.<br><br>When calling database audit for MySQL, NDB for MySQL, and RDS for PostgreSQL instances, this parameter supports V2. |
|SearchParam |[SqlAuditSearchParam](https://docs.byteplus.com/en/docs/DBW/data-structure?_vtm_=a106466.b106468.0_0.0_0.0.1941_7610615829733918244&lang=en#searchparam)<br><br> |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "DisplaySqlTemplate": true,```<br>```    "NodeId": "mysql-06c387******-m8353-0"```<br>```}```<br> |Filter criteria for database audit logs. |
|MaxResults |Integer |No |10 |Page size, default value is 10. |
|NextToken |String |No |885000,1782144054187,1125899906842923,17723951 |Pagination cursor, passed through to downstream detail queries. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DescribeAuditLogDetailRows |Array of [DescribeAuditLogDetailRow](https://docs.byteplus.com/en/docs/DBW/data-structure?_vtm_=a106466.b106468.0_0.0_0.0.1941_7610615829733918244&lang=en#describeauditlogdetailrow)<br><br> |&nbsp;<br><br>```SQL```<br>```[```<br>```    {```<br>```        "AffectRow": 0,```<br>```        "DB": "-",```<br>```        "Duration": 77,```<br>```        "ExecTime": 1782200733,```<br>```        "LogLevel": "",```<br>```        "LogType": "",```<br>```        "NodeId": "mysql-06c387******-m8353-0",```<br>```        "OriSql": "",```<br>```        "ReturnRows": 0,```<br>```        "ScanRows": 0,```<br>```        "SessionId": "860422",```<br>```        "SourceIP": "100.67.229.221",```<br>```        "SqlFingerprint": "d41d8cd98f00b204e9800998ecf******",```<br>```        "SqlMethod": "Connect",```<br>```        "Table": "-",```<br>```        "User": "-"```<br>```    }```<br>```]```<br><br><br> |Detailed list of database audit logs<br><br> |
|TotalCount |Integer |1 |The total number of database audit logs queried within the specified time range. |
|NextToken |String |885000,1782144054187,1125899906842923,17723951 |Pagination cursor; it may be an empty string or omitted when there is no next page. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DescribeAuditLogDetail&Version=2018-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20250626T033433Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250626/cn-beijing/dbw/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
    "InstanceID": "mysql-06c387******",
    "InstanceType": "MySQL",
    "StartTime": 1782120343,
    "EndTime": 1782206743,
    "LogVersion":"V2",
    "SearchParam": {
        "DisplaySqlTemplate": true,
        "NodeId": "mysql-06c387******-m8353-0"
    },
    "RegionId": "cn-beijing"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2026062317273102F819CE458DA1050F46-dfe4e5",
        "Action": "DescribeAuditLogDetail",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DescribeAuditLogDetailRows": [
            {
                "AffectRow": 0,
                "DB": "-",
                "Duration": 77,
                "ExecTime": 1782200733,
                "LogLevel": "",
                "LogType": "",
                "NodeId": "mysql-06c387******-m8353-0",
                "OriSql": "",
                "ReturnRows": 0,
                "ScanRows": 0,
                "SessionId": "860422",
                "SourceIP": "100.67.229.221",
                "SqlFingerprint": "d41d8cd98f00b204e9800998ecf******",
                "SqlMethod": "Connect",
                "Table": "-",
                "User": "-"
            }
        ],
        "NextToken": "",
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
