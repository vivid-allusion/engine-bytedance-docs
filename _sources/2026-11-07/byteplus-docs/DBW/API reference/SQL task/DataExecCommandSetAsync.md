---
title: "DataExecCommandSetAsync"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/dataexeccommandsetasync"
---

Call the DataExecCommandSetAsync API to asynchronously execute a set of commands.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Calling the `DataExecCommandSetAsync` API is a synchronous request that can only obtain a request ID (i.e., the command set ID). If you want to obtain the execution result of the command set, you need to call the [DataGetCommandSetResult](https://docs.byteplus.com/en/docs/DBW/datagetcommandsetresult) API for a query.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronize request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SessionId |String |Yes |MTc4ODg3NTA1Mjg1NTM0NTE1Mi8xNzg4ODc1MDUyODYz\*\*\*\*\*\*\* |Session ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/DBW/dataconnectinstance">DataConnectInstance</a> API to query the session ID.</div><br> |
|CommandSetContent |String |Yes |show databases;show processlist |Content of the command set. If the command set contains multiple commands, separate the commands with semicolons (;). |
|DatabaseName |String |No |sys |Database name. The command set will be executed in the specified database. If not specified, the SQL command will be executed in the current database by default |
|AutoOnlineDDL |Bool |No |true |Specifies whether to enable OnlineDDL for DDL statements in the conversion command set. The values are as follows:<br><br><br>* `false`: (Default) Indicates that this feature is disabled.<br><br>* `true`: Indicates that this feature is `enabled`. |
|Force |Boolen |No |true |The execution method of DDL statements when DDL statements exist in the command set and conversion to OnlineDDL is not supported. The values are as follows:<br><br><br>* `false`: (Default value) When a DDL statement existing in the command set does not support conversion to OnlineDDL, the system refuses to execute the SQL statement and prompts you that the SQL statement contains a DDL statement that OnlineDDL does not support.<br><br>* `true`: When a DDL statement existing in the command set does not support conversion to OnlineDDL, it is still executed as a normal DDL.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can configure this parameter when you call DataExecCommandSetAsync to asynchronously execute the command set of the RDS for MySQL instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>AutoOnlineDDL</code> is set to <code>true</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|CommandSetId |String |178887541272244\*\*\*\* |Command set ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DataExecCommandSetAsync&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
     "SessionId": "MTc4ODg3NTA1Mjg1NTM0NTE1Mi8xNzg4ODc1MDUyODYz********",
     "CommandSetContent": "show databases;show processlist",
     "AutoOnlineDDL":true,
     "Force":true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202405101815074D6C61C22FD7E479870C-e62012",
        "Action": "DataExecCommandSetAsync",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "CommandSetId": "178887541272244****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
