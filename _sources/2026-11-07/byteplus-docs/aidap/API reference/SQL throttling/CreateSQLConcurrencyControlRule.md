---
title: "CreateSQLConcurrencyControlRule"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateSQLConcurrencyControlRule"
---

Call the CreateSQLConcurrencyControlRule API to create SQL concurrency control rules.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API only supports operations on workspaces using the PostgreSQL engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateSQLConcurrencyControlRule&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|DatabaseName |String |Yes |test\-db |Name of the database. |
|Match |Object of [RuleMatch](https://docs.byteplus.com/en/docs/330/119147#rulematch) |Yes |{"Type":"query_string","QueryString":"SELECT \* FROM orders"} |Rate limiting rule matching conditions. Supports matching by SQL text, keyword, or all SQL. |
|LimitConfig |Object of [RuleConfig](https://docs.byteplus.com/en/docs/330/119147#ruleconfig) |Yes |{"Type":"concurrency","MaxConcurrency":10,"MaxWaiting":20,"MaxWaitMs":1000} |Limit configuration. Supports concurrency limit and QPS limit. |
|OverLimitAction |String |Yes |reject |Handling method when the rate limiting rule exceeds the limit. Values:<br><br><br>* `reject`: reject request. Only QPS rate limiting is supported.<br><br>* `queue`: waiting in line. Supports concurrency limiting only. |
|NodeType |String |Yes |All |Rule effective node scope. Values:<br><br><br>* `Primary`: primary node.<br><br>* `Standby`: secondary node.<br><br>* `All`: all nodes. |
|Enabled |Boolean |No |true |Whether to enable after creating the rule. Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no. |
|Comment |String |No |Limit slow query concurrency |Rate limiting rule note. Maximum length is 256 characters. |
|SearchPath |String |No |public |When the flow control rule matches by SQL text, the search_path used to calculate the queryId corresponding to the SQL text has a maximum length of 256 characters. |
|EffectType |String |No |NextWakeUp |Effective method. Values:<br><br><br>* `Immediate`: takes effect immediately if the Workspace is Running; if the Workspace is Suspending, it takes effect upon waking up. Default value.<br><br>* `NextWakeUp`: takes effect at the next wake\-up. |
|CreateMode |String |No |Overwrite |Create mode for SQL rate limiting rules. Values:<br><br><br>* `ErrorIfExists`: error if already exists. Default value.<br><br>* `Overwrite`: overwrite existing rules. |


<span id="rulematch"></span>
### RuleMatch


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |query_string |Match type. Values:<br><br><br>* `query_string`: match by SQL text.<br><br>* `keywords`: match by keywords.<br><br>* `all`: match all SQL. |
|Keywords |Array of String |No |["slow_query"] |Keyword. Used when Type is `keywords`. |
|QueryString |String |No |SELECT \* FROM orders |SQL text. used when Type is `query_string`. |


<span id="ruleconfig"></span>
### RuleConfig


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |concurrency |Rate limiting type. Values:<br><br><br>* `concurrency`: concurrency limit.<br><br>* `qps`: QPS limit. |
|QPS |Integer |No |100 |The number of requests allowed per second. Used when Type is `qps`. |
|Burst |Integer |No |200 |Token bucket capacity. Used when Type is `qps`. |
|MaxWaitMs |Integer |No |1000 |Maximum wait time in milliseconds. 0 means no limit on wait time. Used when Type is `concurrency`. |
|MaxWaiting |Integer |No |20 |Maximum waiting queue length. Used when Type is `concurrency`. |
|MaxConcurrency |Integer |No |10 |Maximum concurrency. Used when Type is `concurrency`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Code |Integer |0 |Return status code. 0 indicates succeeded. |
|Message |String |success |return message. |
|RuleId |Long |136734987028564\*\*\*\* |ID of the rate limiting rule. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

Create concurrency limiting rule by SQL text matching

```JSON
POST /?Action=CreateSQLConcurrencyControlRule&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "DatabaseName": "test-db",
    "Match": {
        "Type": "query_string",
        "QueryString": "select 1"
    },
    "LimitConfig": {
        "Type": "concurrency",
        "MaxConcurrency": 10,
        "MaxWaiting": 5,
        "MaxWaitMs": 5000
    },
    "OverLimitAction": "reject",
    "NodeType": "Primary"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSQLConcurrencyControlRule",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "RuleId": 100001
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Sample request 2

Create QPS limiting rule by keyword matching

```JSON
POST /?Action=CreateSQLConcurrencyControlRule&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "DatabaseName": "test-db",
    "Match": {
        "Type": "keywords",
        "Keywords": [
            "insert",
            "orders"
        ]
    },
    "LimitConfig": {
        "Type": "qps",
        "QPS": 500,
        "Burst": 1000
    },
    "OverLimitAction": "reject",
    "NodeType": "Primary"
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Sample response 2

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSQLConcurrencyControlRule",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "RuleId": 100001
    }
}
```


<span id=".6K-35rGC56S65L6LLTM="></span>
### Sample request 3

Create QPS limiting rule by all SQL matching (default ErrorIfExists)

```JSON
POST /?Action=CreateSQLConcurrencyControlRule&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "DatabaseName": "test-db",
    "Match": {
        "Type": "all"
    },
    "LimitConfig": {
        "Type": "qps",
        "QPS": 1000,
        "Burst": 2000
    },
    "OverLimitAction": "reject",
    "NodeType": "All"
}
```


<span id=".6L-U5Zue56S65L6LLTM="></span>
### Sample response 3

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSQLConcurrencyControlRule",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "RuleId": 100001
    }
}
```


<span id=".6K-35rGC56S65L6LLTQ="></span>
### Sample request 4

Create QPS limiting rule by all SQL matching (specify Overwrite to allow repeated setting)

```JSON
POST /?Action=CreateSQLConcurrencyControlRule&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "DatabaseName": "test-db",
    "Match": {
        "Type": "all"
    },
    "LimitConfig": {
        "Type": "qps",
        "QPS": 100,
        "Burst": 200
    },
    "OverLimitAction": "reject",
    "NodeType": "All",
    "Enabled": true,
    "Comment": "account upgrade",
    "SearchPath": "public",
    "EffectType": "Immediate",
    "CreateMode": "Overwrite"
}
```


<span id=".6L-U5Zue56S65L6LLTQ="></span>
### Sample response 4

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSQLConcurrencyControlRule",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "RuleId": 100001
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
