---
title: "DescribeSQLConcurrencyControlRules"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeSQLConcurrencyControlRules"
---

Call the DescribeSQLConcurrencyControlRules API to query SQL concurrency control rules.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API only supports operations on workspaces using the PostgreSQL engine.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSQLConcurrencyControlRules&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |Workspace ID。 |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|DatabaseName |String |Yes |test\-db |Name of the database. |
|MatchType |String |No |keywords |Filter by runtime matching Type. Values:<br><br><br>* `query_id`<br><br>* `keywords`<br><br>* `all` |
|QueryId |Long |No |12345 |Filter by `query_id`. |
|QueryString |String |No |SELECT \* FROM |Filter by SQL text, minimum length is 1 character. |
|Keywords |Array of String |No |["slow_query"] |Filter by keyword. |
|LimitType |String |No |concurrency |Filter by limit type. Values:<br><br><br>* `concurrency`: concurrency limit.<br><br>* `qps`: QPS limit. |
|OverLimitAction |String |No |reject |Handling method when the rate limiting rule exceeds the limit. Values:<br><br><br>* `reject`: reject request. Only QPS rate limiting is supported.<br><br>* `queue`: waiting in line. Supports concurrency limiting only. |
|NodeType |String |No |Primary |Rule effective node scope. Values:<br><br><br>* `Primary`: primary node.<br><br>* `Standby`: secondary node.<br><br>* `All`: all nodes. |
|Enabled |Boolean |No |true |Filter by enabled status. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|Offset |Integer |No |0 |Paging offset, default value is 0. |
|Limit |Integer |No |20 |Items per page. Value range: 1~100. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Code |Integer |0 |Return status code. 0 indicates succeeded. |
|Message |String |success |return message. |
|TotalCount |Long |5 |Total number of rules that meet the conditions. |
|Rules |Array of [SQLConcurrencyControlRuleInfo](https://docs.byteplus.com/en/docs/330/119150#sqlconcurrencycontrolruleinfo) |[{"RuleId":136734987028564\*\*\*\*,"MatchType":"keywords","LimitType":"concurrency","Enabled":true}] |Rate limit rule details list. |


<span id="sqlconcurrencycontrolruleinfo"></span>
### SQLConcurrencyControlRuleInfo


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|QPS |Integer |100 |The number of requests allowed per second. |
|Burst |Integer |200 |Token bucket capacity. |
|RuleId |Long |136734987028564\*\*\*\* |ID of the rate limiting rule. |
|Comment |String |Limit slow query concurrency |Rule notes. |
|Enabled |Boolean |true |Whether to enable the rule. |
|QueryId |Long |12345 |Final matching value of the query_id rule. |
|Keywords |Array of String |["slow_query"] |Array of keywords for the keywords rule. |
|NodeType |String |All |Rule effective node scope. Values:<br><br><br>* `Primary`: primary node.<br><br>* `Standby`: secondary node.<br><br>* `All`: all nodes. |
|CreatedAt |String |2026\-01\-01T00:00:00Z |Rule creation time. |
|LimitType |String |concurrency |Type of limit rule. Values:<br><br><br>* `concurrency`: concurrency limit.<br><br>* `qps`: QPS limit. |
|MatchType |String |keywords |Runtime matching type. Values:<br><br><br>* `query_id`<br><br>* `keywords`<br><br>* `all` |
|MaxWaitMs |Integer |1000 |Maximum wait time for concurrency limiting, in milliseconds. 0 means no limit on wait time. |
|UpdatedAt |String |2026\-01\-01T00:00:00Z |Rule update time. |
|MaxWaiting |Integer |20 |Maximum wait number for concurrency and rate limiting. |
|SearchPath |String |public |When the flow control rule matches by SQL text, the search_path used to calculate the queryId corresponding to the SQL text has a maximum length of 256 characters. |
|QueryString |String |SELECT \* FROM orders |The original SQL when the user creates a rule via SQL text, used only for audit and recalculation. |
|MaxConcurrency |Integer |10 |Max concurrency for concurrency limit. |
|OverLimitAction |String |reject |Handling method when the rate limiting rule exceeds the limit. Values:<br><br><br>* `reject`: reject request. Only QPS rate limiting is supported.<br><br>* `queue`: waiting in line. Supports concurrency limiting only. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeSQLConcurrencyControlRules&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "DatabaseName": "test-db"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSQLConcurrencyControlRules",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "TotalCount": 5,
        "Rules": [
            {
                "QPS": 100,
                "Burst": 200,
                "RuleId": 136734987028564,
                "Comment": "限制慢查询并发",
                "Enabled": true,
                "QueryId": 12345,
                "Keywords": [
                    "slow_query"
                ],
                "NodeType": "All",
                "CreatedAt": "2026-01-01T00:00:00Z",
                "LimitType": "concurrency",
                "MatchType": "keywords",
                "MaxWaitMs": 1000,
                "UpdatedAt": "2026-01-01T00:00:00Z",
                "MaxWaiting": 20,
                "SearchPath": "public",
                "QueryString": "SELECT * FROM orders",
                "MaxConcurrency": 10,
                "OverLimitAction": "reject"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
