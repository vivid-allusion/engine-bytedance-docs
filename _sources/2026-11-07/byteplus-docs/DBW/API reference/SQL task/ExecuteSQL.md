---
title: "ExecuteSQL"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ExecuteSQL"
---

Call the ExecuteSQL API to execute SQL statements.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This API does not support OnlineDDL actions. Using this API to execute DDL operations may cause DML, DQL, and other operations to be blocked. Use with caution.</div>


* <div data-tips="true" data-tips-type="default">This API does not support RDS for PostgreSQL and RDS for SQL Server databases.</div>



<span id="UcUAok1W"></span>
## Request type

Synchronize request.

<span id="Nbef1OZQ"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceID |String |Yes |mysql\-bf120f\*\*\*\*\*\* |Database instance ID<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of veDB for MySQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Mongo`: Document Database for MongoDB.<br><br>* `Redis`: Cache for Redis. |
|Database |String |Yes |mysql |Database name. Specifies to execute SQL command in a database. If not specified, the SQL command is executed in the current database by default. |
|Commands |String |Yes |select \* from func; |SQL text.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the database type is <code>MySQL</code> or <code>veDBMySQL</code>, if you need to execute multiple SQL statements, you can separate them with a semicolon (;).</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the database type is Redis, if you need to execute multiple SQL statements, you can separate them with <code>\r\n.</code></div><br><br><br>* <div data-tips="true" data-tips-type="default">When the database type is Document Database for MongoDB, executing multiple SQL statements is not supported. Only one SQL statement can be included in the SQL text.</div><br> |
|TimeOutSeconds |Integer |No |300 |SQL command timeout. Unit: seconds (s). The default is 300 seconds. |


<span id="unDsW6Bn"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Results |Array of ResultObject |[ResultObject](https://docs.byteplus.com/en/docs/DBW/data-structure#result) |The result of executing the SQL command. |


<span id="ViIoguuy"></span>
## Request example

```JSON
POST /?Action=ExecuteSQL&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.volcengineapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGYyM******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341861******

{
  "InstanceID": "mysql-bf120f******",
  "InstanceType": "MySQL",
  "Database": "company",
  "Commands": "select * from func;"
}
```


<span id="KoakzrG2"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202309221612539B33ED77F0A06214EB4A",
        "Action": "ExecuteSQL",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Results": [
            {
                "ColumnNames": [
                    "opid",
                    "opcode",
                    "opname",
                    "ophref",
                    "opseq"
                ],
                "CommandStr": "Select * from auth_operation",
                "ReasonDetail": "",
                "RowCount": 2,
                "Rows": [
                    {
                        "Cells": [
                            "87",
                            "01",
                            "权限管理",
                            "/admin/auth",
                            "1"
                        ]
                    },
                    {
                        "Cells": [
                            "98",
                            "010205",
                            "角色权限管理页面",
                            "/admin/role/bindOperPage/{roleid}",
                            "1"
                        ]
                    }
                ],
                "RunTime": 1695370373000,
                "State": "Success"
            }
        ]
    }
}
```


<span id="69CSj8PK"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
