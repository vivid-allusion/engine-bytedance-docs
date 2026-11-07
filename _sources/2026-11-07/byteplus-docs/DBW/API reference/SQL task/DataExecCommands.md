---
title: "DataExecCommands"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/dataexeccommands"
---

Call the DataExecCommands interfaceAPI to execute an SQL command.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This API does not support OnlineDDL actions. Using this API to execute DDL operations may cause DML, DQL, and other operations to be blocked. Use with caution.</div>


* <div data-tips="true" data-tips-type="tip">This API does not support RDS for PostgreSQL and RDS for SQL Server databases.</div>



<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronize request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Is it required? |Sample |Description |
|---|---|---|---|---|
|SessionId |String |Yes |MTU4MDg1MTE1NzM5ODQ3ODg0OC8xNTgwODUxMTU3NDQ0NjIw\*\*\*\* |Session ID<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/DBW/dataconnectinstance">DataConnectInstance</a> API to query the session ID.</div><br> |
|Commands |String |Yes |Select \* from func; |SQL text.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the database type is MySQL or veDBMySQL, if you need to execute multiple SQL statements, you can separate them with a semicolon (;).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the database type is Redis, if you need to execute multiple SQL statements, you can separate them with <code>\r\n</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the database type is Document Database for MongoDB, executing multiple SQL statements is not supported. Only one SQL statement can be included in the SQL text.</div><br> |
|DatabaseName |String |No |mysql |Database name. Specifies to execute SQL command in a database. If not specified, the SQL command is executed in the current database by default. |
|TimeOutSeconds |Integer |No |5 |SQL command timeout. Unit: seconds (s). The default is 300 seconds. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Results |Array of ResultObject |[ResultObject](https://docs.byteplus.com/en/docs/DBW/data-structure#result) |The result of executing the SQL command. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DataExecCommands&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
      "SessionId": "MTU4MDg1MTE1NzM5ODQ3ODg0OC8xNTgwODUxMTU3NDQ0NjIw****",
      "Commands" : "Select * from func;",
      "DatabaseName": "mysql",
      "TimeOutSeconds": 5
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202309221612539B33ED77F0A06214EB4A",
        "Action": "DataExecCommands",
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


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
