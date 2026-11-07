---
title: "GetTraceDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetTraceDetail"
---

Obtain trace details.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=GetTraceDetail&Version=2026\-01\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetTraceDetail |The API name. The API name is `GetTraceDetail`. |
|Version |String |Yes |2026\-01\-01 |The API version. The API version is `2026-01-01`. |
|TraceId |String |Yes |b7d963cxxxx30e7c5ddexxxx |The trace ID to query. |
|SuggestTime |Long |Yes |1767196800 |Limit the search time range to one hour before and after SuggestTime to accelerate the query. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=GetTraceDetail&Version=2026-01-01
{
    "TraceId": "b7d963cxxxx30e7c5ddexxxx",
    "SuggestTime": 1767196800
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Msg |String |No data was found in the query |The prompt message. It is returned based on the actual situation. |
|Trace |Object of [Trace](https://docs.byteplus.com/en/docs/299/84298#trace) |\- |The Trace details to query. This configuration is the core returned data. |
|Summary |Object of [TraceSummaryInfo](https://docs.byteplus.com/en/docs/299/84298#tracesummaryinfo) |\- |The summary statistics of the Trace. |


<span id="trace"></span>
### Trace


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |Integer |0 |The Trace status code.<br><br><br>* In non\-HTTP add\-ons, 0 indicates normal, and 1 indicates abnormal.<br><br>* In HTTP add\-ons, it is equivalent to http_status_code, such as 404 and 500. |
|ApiName |String |DemoMethod |The starting API of the Trace. |
|TraceId |String |b7d963c267c30e7c5ddexxxx |The trace ID to query. |
|SpanList |Array of [SpanBrief](https://docs.byteplus.com/en/docs/299/84298#spanbrief) |\- |The summary of the Spans. |
|ServiceName |String |test\-grpc\-server |The starting service of the Trace. |
|ServiceType |String |rpc |The starting service type of the Trace. |
|DurationMicroseconds |Long |1873 |The overall duration. Unit: microseconds. |
|StartTimeMillisecond |Long |1767196800000 |Start time. |


<span id="spanbrief"></span>
### SpanBrief


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Env |String |prod |The environment to which the current Span belongs. |
|SpanId |String |4374f05fb9axxxxx |The Span ID information. |
|Status |Integer |0 |The Span status code.<br><br><br>* In non\-HTTP add\-ons, 0 indicates normal, and 1 indicates abnormal.<br><br>* In HTTP add\-ons, it is equivalent to http_status_code, such as 404 and 500. |
|ApiName |String |DemoMethod |The API name. |
|ApiTime |Long |1767196800 |The server\-side receiving time. |
|Hostname |String |demo\-grpc\-server\-7f89c4677c\-xxxxx |The hostname. |
|SpanType |String |server |The Span type. |
|EventList |Array of [Event](https://docs.byteplus.com/en/docs/299/84298#event) |\- |The event list. |
|InputTokens |Long |16 |The number of input tokens for the generated AI Span. |
|ServiceName |String |test\-grpc\-server |Service name. |
|ServiceType |String |rpc |The service type. |
|TotalTokens |Long |166 |The total number of tokens for the generated AI Span. |
|OutputTokens |Long |150 |The number of output tokens for the generated AI Span. |
|ParentSpanId |String |4ce724e472axxxx |The parent Span ID. |
|ErrorInfoList |Array of [TraceErrorInfo](https://docs.byteplus.com/en/docs/299/84298#traceerrorinfo) |\- |The error information list. You can view multiple errors in one Span. |
|GenAISpanKind |String |llm |The type of the generated AI Span. |
|OperationName |String |redis.command |The operation name. |
|CacheReadTokens |Long |100 |The number of cache read tokens for the generated AI Span. |
|CallServiceType |String |rpc |The downstream service type. |
|DurationMicroseconds |Long |1096 |The duration. Unit: microseconds. |
|StartTimeMicrosecond |Long |1767196800000000 |The start time. Unit: microseconds. |
|StartTimeMillisecond |Long |1767196800000 |The start time. Unit: milliseconds. |
|RelativeStartTimeMillisecond |Long |100 |The relative time from the start of the request call to the start of the current Span. Unit: milliseconds. |


<span id="event"></span>
### Event


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Tags |JSON Map |{'message.id':'1.0','message.type':'RECEIVED'} |The event tag. |
|TraceId |String |58f56847851be99ea0ff3cxxxxxxxxxx |The ID of the trace to which the event belongs. |
|EventName |String |message |The event name. |
|ServiceName |String |demo\-service |The service to which the event belongs. |
|OperationName |String |Get |The event operation name. |
|EventTimeMillisecond |Long |1767196800000 |The event occurrence time. Unit: milliseconds. |


<span id="tags"></span>
### Tags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |message.type |The key of the event tag. |
|value |String |RECEIVED |The value of the event tag. |


<span id="traceerrorinfo"></span>
### TraceErrorInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|IssueId |String |b7d963c267c30e7c5ddexxxx |The error ID. |
|ErrorKind |String |UncaughtException |The error type. |
|ErrorTags |JSON Map |{'error_tag_key':'error_tag_value'} |The error tag. |
|ErrorStack |String |java.lang.RuntimeException: Node not found\n\tat com.example.grpcserver.xxx.demoMethod(xxx.java:34).... |The error stack trace. |
|ErrorMessage |String |Node not found |Error message. |
|ErrorOccurTime |Long |1767196800 |The time when the error occurred. |


<span id="errortags"></span>
### ErrorTags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |error_tag_key |The key of the error tag. |
|value |String |error_tag_value |The value of the error tag. |


<span id="tracesummaryinfo"></span>
### TraceSummaryInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SpanNums |Integer |10 |The total number of Spans. |
|ServiceNums |Integer |5 |The total number of involved services. |
|ErrorSpanIds |Array of String |['4374f05fb9axxxxx','4ce724e472axxxx'] |The error Span IDs. |
|ComponentSpanIds |JSON Map |{'kitex':['4374f05fb9axxxxx','4ce724e472axxxx'],'redis':['4374f05fb9axxxxx']} |The add\-ons and add\-on Span IDs. The key is the add\-on, including middleware and service calls, and the value is the Span ID list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different add\-ons may contain duplicate Spans.</div><br> |
|LLMComponentSpanIds |JSON Map |{'OpenAI':['4374f05fb9axxxxx','4ce724e472axxxx']} |The statistics of large language model add\-ons. key is the span.kind and gen_ai.system of the large language model add\-on, and the value is the Span ID list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different add\-ons may contain duplicate Spans.</div><br> |


<span id="componentspanids"></span>
### ComponentSpanIds


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |kitex |The key of the general add\-on. |
|value |Array of String |['4374f05fb9axxxxx','4ce724e472axxxx'] |The value of the general add\-on. |


<span id="llmcomponentspanids"></span>
### LLMComponentSpanIds


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |OpenAI |The key of the large language model add\-on. |
|value |Array of String |['4374f05fb9axxxxx','4ce724e472axxxx'] |The value of the large language model add\-on. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "Msg": "No data was found in the query",
        "Trace": {
            "Status": 0,
            "ApiName": "DemoMethod",
            "TraceId": "b7d963c267c30e7c5ddexxxx",
            "SpanList": [
                {
                    "Env": "prod",
                    "SpanId": "4374f05fb9axxxxx",
                    "Status": 0,
                    "ApiName": "DemoMethod",
                    "ApiTime": 1767196800,
                    "Hostname": "demo-grpc-server-7f89c4677c-xxxxx",
                    "SpanType": "server",
                    "EventList": [
                        {
                            "TraceId": "58f56847851be99ea0ff3cxxxxxxxxxx",
                            "Tags": "{'message.id':'1.0','message.type':'RECEIVED'}",
                            "EventName": "message",
                            "ServiceName": "demo-service",
                            "OperationName": "Get",
                            "EventTimeMillisecond": 1767196800000
                        }
                    ],
                    "ServiceName": "test-grpc-server",
                    "ServiceType": "rpc",
                    "TotalTokens": 166,
                    "OutputTokens": 150,
                    "ParentSpanId": "4ce724e472axxxx",
                    "ErrorInfoList": [
                        {
                            "IssueId": "b7d963c267c30e7c5ddexxxx",
                            "ErrorKind": "UncaughtException",
                            "ErrorTags": "{'error_tag_key':'error_tag_value'}",
                            "ErrorStack": "java.lang.RuntimeException: Node not found\\n\\tat com.example.grpcserver.xxx.demoMethod(xxx.java:34)\\....",
                            "ErrorMessage": "Node not found",
                            "ErrorOccurTime": 1767196800
                        }
                    ],
                    "GenAISpanKind": "llm",
                    "OperationName": "redis.command",
                    "CacheReadTokens": 100,
                    "CallServiceType": "rpc",
                    "DurationMicroseconds": 1096,
                    "StartTimeMicrosecond": 1767196800000000,
                    "StartTimeMillisecond": 1767196800000,
                    "RelativeStartTimeMillisecond": 100
                }
            ],
            "ServiceName": "test-grpc-server",
            "ServiceType": "rpc",
            "DurationMicroseconds": 1873,
            "StartTimeMillisecond": 1767196800000
        },
        "Summary": {
            "SpanNums": 10,
            "ServiceNums": 5,
            "ErrorSpanIds": [
                ""
            ]
        }
    },
    "ResponseMetadata": {
        "Action": "GetTraceDetail",
        "Region": "cn-north-1",
        "Service": "apmplus_server",
        "Version": "2026-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the API call returns an exception, you can troubleshoot by referring to the API error codes and the [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) below.


|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|500 |ErrInternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
