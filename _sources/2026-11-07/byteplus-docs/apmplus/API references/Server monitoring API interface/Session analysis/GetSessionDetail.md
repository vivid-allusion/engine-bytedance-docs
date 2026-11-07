---
title: "GetSessionDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetSessionDetail"
---

Gets session details.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=GetSessionDetail&Version=2026\-01\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetSessionDetail |The API name. The API name is `GetSessionDetail`. |
|Version |String |Yes |2026\-01\-01 |The API version. The API version is `2026-01-01`. |
|StartTime |Long |Yes |1767196800000 |The query start timestamp in milliseconds. |
|EndTime |Long |Yes |1767200400000 |The query start timestamp in milliseconds. |
|SessionId |String |Yes |sess_001 |The session ID. |
|Workspace |String |No |default |Workspace. Workspaces are a data management and isolation method provided by Server\-side Monitoring. Each workspace has independent data reporting credentials and can centrally manage traces, logs, and metrics for different application ownership scenarios. |
|Service |String |No |runtime\-id.runtime\-name |The service to which the session belongs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=GetSessionDetail&Version=2026-01-01
{
    "StartTime": 1767196800000,
    "EndTime": 1767200400000,
    "SessionId": "sess_001",
    "Workspace": "default",
    "Service": "runtime-id.runtime-name"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|UserId |String |u123 |The user ID. |
|TraceIds |Array of String |["trace_001","trace_002"] |A list of trace IDs for the session arranged in the same order as `SessionTraces`. |
|SessionId |String |sess_001 |The session ID. |
|TotalTokens |Integer |420 |The number of tokens for the session. |
|SessionTraces |Array of [SessionTrace](https://docs.byteplus.com/en/docs/299/106043#sessiontrace) |[{"trace_id":"trace_001","user_id":"u123","total_tokens":180,"model_input_tokens":{"doubao\-seed\-1\-6":80},"model_output_tokens":{"doubao\-seed\-1\-6":100},"model_total_tokens":{"doubao\-seed\-1\-6":180},"duration":7000,"start_time":1767196802000,"input":"Please summarize this text","output":"This text mainly describes the execution process of the system call link"}] |List of traces associated with the session, sorted in ascending order by the trace start time. |
|SessionEndTime |Long |1767196815000 |The timestamp of the last call in the session, in milliseconds. |
|ModelInputTokens |JSON Map |{"doubao\-seed\-1\-6":180} |The number of input tokens aggregated by model at the session level. |
|ModelTotalTokens |JSON Map |{"doubao\-seed\-1\-6":420} |The total number of tokens aggregated by model at the session level. |
|SessionStartTime |Long |1767196801000 |The start timestamp of the session, in milliseconds. |
|ModelOutputTokens |JSON Map |{"doubao\-seed\-1\-6":240} |The number of output tokens aggregated by model at the session level. |


<span id="sessiontrace"></span>
### SessionTrace


|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|Input |String |Please summarize this text |The input of the trace.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The input of the AI root span is used preferentially. If the input of the AI root span is missing, the input of the first non\-empty span within the trace is used.</div><br> |
|Output |String |This text mainly describes the execution process of the system call link |The output of the trace.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The output of the AI root span is used preferentially. If the output of the AI root span is missing, the output of the last non\-empty span within the trace is used.</div><br> |
|UserId |String |u123 |The user ID. |
|TraceId |String |trace_001 |Trace ID. |
|Duration |Long |7000 |The duration of the trace, in milliseconds.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The duration of the AI root span is used preferentially. If the duration of the AI root span is missing, this parameter value is calculated based on the time range of spans within the trace.</div><br> |
|StartTime |Long |1767196802000 |The start time of the trace, in milliseconds.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The start time of the AI root span is used preferentially. If the start time of the AI root span is missing, the start time of the earliest span within the trace is used.</div><br> |
|TotalTokens |Integer |180 |The total token count for the trace, aggregated by LLM spans of the trace. |
|ModelInputTokens |JSON Map |{"doubao\-seed\-1\-6":80} |The number of input tokens aggregated by model. |
|ModelTotalTokens |JSON Map |{"doubao\-seed\-1\-6":180} |The total number of tokens aggregated by model. |
|ModelOutputTokens |JSON Map |{"doubao\-seed\-1\-6":100} |The number of output tokens aggregated by model. |


<span id="modelinputtokens"></span>
### ModelInputTokens


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |doubao\-seed\-1\-6 |Model name. |
|value |Integer |80 |Input token count. |


<span id="modeltotaltokens"></span>
### ModelTotalTokens


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |doubao\-seed\-1\-6 |Model name. |
|value |Integer |180 |Total token count. |


<span id="modeloutputtokens"></span>
### ModelOutputTokens


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |doubao\-seed\-1\-6 |Model name. |
|value |Integer |100 |Output token count. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "SessionId": "sess_001",
        "TotalTokens": 420,
        "TraceIds": [
            "trace_001"
        ],
        "UserId": "u123",
        "SessionStartTime": 1767196801000,
        "SessionEndTime": 1767196815000,
        "ModelInputTokens": {
            "doubao-seed-1-6": 180
        },
        "ModelOutputTokens": {
            "doubao-seed-1-6": 240
        },
        "ModelTotalTokens": {
            "doubao-seed-1-6": 420
        },
        "SessionTraces": [
            {
                "TraceId": "trace_001",
                "UserId": "u123",
                "TotalTokens": 180,
                "Duration": 7000,
                "StartTime": 1767196802000
            }
        ]
    },
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSessionDetail",
        "Version": "2026-01-01",
        "Service": "apmplus_server",
        "Region": "cn-north-1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
