---
title: "ListSession"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ListSession"
---

Lists sessions.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=ListSession&Version=2026\-01\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListSession |The API name. The API name is `ListSession`. |
|Version |String |Yes |2026\-01\-01 |The API version. The API version is `2026-01-01`. |
|StartTime |Long |Yes |1767196800000 |The start timestamp of the query in milliseconds. |
|EndTime |Long |Yes |1767200400000 |The end timestamp of the query in milliseconds. |
|Filters |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/106044#filtercondition) |Yes |[{"key":"user_id","op":"in","values":["u123"]}] |Session filter condition. Values:<br><br><br>* session_id: Session ID<br><br>* user_id: User ID<br><br>* service: Service to which the session belongs<br><br>* trace_count: Trace count<br><br>* input_tokens: Number of input tokens for the session<br><br>* output_tokens: Number of output tokens for the session<br><br>* total_tokens: Total number of tokens for the session<br><br>* duration: Session duration<br><br>* session_start_time: Session start time |
|ProjectName |String |No |default |The project name. |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/299/106044#tagfilter) |Yes |[{"key":"env","values":["prod"]}] |Tag filter condition. |
|PageNo |Integer |Yes |1 |Page number. Pagination starts from page 1. This parameter does not have a default value. Specify a positive integer. |
|PageSize |Integer |Yes |20 |Number of sessions per page. This parameter does not have a default value. Specify a positive integer. |
|OrderBy |String |No |session_start_time |A field for sorting. Value<br><br><br>* session_start_time (default): Session start time<br><br>* duration: Session duration<br><br>* trace_count: Trace count<br><br>* input_tokens: Number of input tokens for the session<br><br>* output_tokens: Number of output tokens for the session<br><br>* total_tokens: Total number of tokens for the session<br><br>* session_id: Session ID<br><br>* user_id: User ID<br><br>* service: Service to which the session belongs |
|Order |String |No |desc |Sorting order. Values:<br><br><br>* asc: Ascending order<br><br>* desc: Descending order (default value) |
|BusinessCarrier |String |No |agentkit_runtime |Business carrier. It is used to filter for associated services. Sample value:<br><br><br>* agentkit_runtime<br><br>* arkclaw_enterprise<br><br>* arkclaw_personal<br><br>* arkclaw_omni |
|Workspace |String |No |default |Workspace. Workspaces are a data management and isolation method provided by Server\-side Monitoring. Each workspace has independent data reporting credentials and can centrally manage traces, logs, and metrics for different application ownership scenarios. |


<span id="filtercondition"></span>
### FilterCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Op |String |No |in |The operator. Values:<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|Key |String |No |call_service_type |Key of the filter condition. |
|Values |Array of String |No |["http"] |Value of the filter condition. |


<span id="tagfilter"></span>
### TagFilter


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |No |testKey |The tag key. |
|Values |Array of String |No |["testValue"] |The tag value. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=ListSession&Version=2026-01-01
{
    "StartTime": 1767196800000,
    "EndTime": 1767200400000,
    "Filters": [
        {
            "key": "user_id",
            "op": "in",
            "values": [
                "u123"
            ]
        }
    ],
    "ProjectName": "default",
    "TagFilters": [
        {
            "key": "env",
            "values": [
                "prod"
            ]
        }
    ],
    "PageNo": 1,
    "PageSize": 20,
    "OrderBy": "session_start_time",
    "Order": "desc",
    "BusinessCarrier": "agentkit_runtime",
    "Workspace": "default"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TotalCount |Integer |128 |Total number of query results. It is used for pagination. |
|SessionBriefs |Array of [SessionBrief](https://docs.byteplus.com/en/docs/299/106044#sessionbrief) |[{"session_id":"sess_001","input_tokens":120,"output_tokens":300,"total_tokens":420,"trace_ids":["trace_001"],"user_id":"u123","session_start_time":1767196801000,"session_end_time":1767196815000,"workspace":"default"}] |A list of session summaries. |


<span id="sessionbrief"></span>
### SessionBrief


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|UserId |String |u123 |The user ID. |
|TraceIds |Array of String |["trace_001","trace_002"] |A list of trace IDs. |
|SessionId |String |sess_001 |The session ID. |
|Workspace |String |default |Workspace. |
|InputTokens |Integer |120 |The number of input tokens for the session. |
|TotalTokens |Integer |420 |The number of tokens for the session. |
|OutputTokens |Integer |300 |The number of output tokens for the session. |
|SessionEndTime |Long |1767196815000 |The timestamp of the last call in the session, in milliseconds. |
|SessionStartTime |Long |1767196801000 |The start timestamp of the session, in milliseconds. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "SessionBriefs": [
            {
                "SessionId": "sess_001",
                "InputTokens": 120,
                "OutputTokens": 300,
                "TotalTokens": 420,
                "TraceIds": [
                    "trace_001"
                ],
                "UserId": "u123",
                "SessionStartTime": 1767196801000,
                "SessionEndTime": 1767196815000,
                "Workspace": "default"
            }
        ],
        "TotalCount": 128
    },
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListSession",
        "Version": "2026-01-01",
        "Service": "apmplus_server",
        "Region": "cn-north-1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
