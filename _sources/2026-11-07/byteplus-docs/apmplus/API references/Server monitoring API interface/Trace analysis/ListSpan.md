---
title: "ListSpan"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ListSpan"
---

Obtains the Span list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=ListSpan&Version=2026\-01\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListSpan |The API name. The API name is `ListSpan`. |
|Version |String |Yes |2026\-01\-01 |The API version. The API version is `2026-01-01`. |
|StartTime |Long |Yes |1767196800 |The query start timestamp in seconds. |
|EndTime |Long |Yes |1767200400 |Query end timestamp in seconds. |
|Filters |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/84297#filtercondition) |Yes |\- |The general\-purpose filter criteria, which correspond to the filter boxes on the page.<br><br>An item consists of key, op, and value, such as `span_type,in,server`. If no filter is specified, an empty list can be passed in. |
|Order |String |Yes |DESC |The sorting order. Valid values:<br><br><br>* ASC: Ascending order. Data is sorted in ascending order based on the specified column value.<br><br>* DESC: Descending order. Data is sorted in descending order based on the specified column value.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be left empty. If this parameter is set to an empty string, the default value is DESC.</div><br> |
|OrderBy |String |Yes |duration_microseconds |A field for sorting. Valid values:<br><br><br>* start_time_millisecond: Start time<br><br>* duration_microseconds: Duration<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be left empty. If this parameter is set to an empty string, the default value is start_time_millisecond.</div><br> |
|Offset |Integer |Yes |10 |The start position of the query result. If this parameter is set to 10, it indicates that the first 10 data entries are skipped. |
|Limit |Integer |Yes |30 |The number of query results. |
|MinCallCostMillisecond |Long |Yes |100 |The minimum call duration. If this parameter is set to 0, it indicates that this filter is not used. |
|MaxCallCostMillisecond |Long |Yes |1,000 |The maximum call duration. If this parameter is set to 0, it indicates that this filter is not used. |
|ProjectName |String |No |default |The project name. |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/299/84297#tagfilter) |Yes |\- |Tag filter condition. It is set to a value in the format of key\-value pairs, which corresponds to the tag filter feature on the page. |
|BusinessCarrier |String |No |agentkit_runtime |The business carrier. Valid value: agentkit_runtime.<br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">If this parameter is set to <code>agentkit_runtime</code>, the values of the ProjectName and TagFilters parameters do not take effect.</div><br> |


<span id="filtercondition"></span>
### FilterCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Op |String |No |in |The operator in filter criteria. Valid values: in and not_in. |
|Key |String |No |call_service_type |Key of the filter condition. |
|Values |Array of String |No |['http'] |Value of the filter condition. |


<span id="tagfilter"></span>
### TagFilter


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |No |testKey |The tag key. |
|Values |Array of String |No |['testValue'] |The tag value. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=ListSpan&Version=2026-01-01
{
    "StartTime": 1767196800,
    "EndTime": 1767200400,
    "Filters": [
        {
            "Op": "in",
            "Key": "call_service_type",
            "Values": [
                ""
            ]
        }
    ],
    "Order": "DESC",
    "OrderBy": "duration_microseconds",
    "Offset": 10,
    "Limit": 30,
    "MinCallCostMillisecond": 100,
    "MaxCallCostMillisecond": 1000,
    "ProjectName": "default",
    "TagFilters": [
        {
            "Key": "testKey",
            "Values": [
                ""
            ]
        }
    ],
    "BusinessCarrier": "agentkit_runtime"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SpanList |Array of [Span](https://docs.byteplus.com/en/docs/299/84297#span) |\- |The Span list. |


<span id="span"></span>
### Span


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|PId |Long |0 |The process ID. |
|Sql |String |SELECT \* FROM test WHERE id = 233xxx |The SQL statement.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">Some parameters will be masked.</div><br> |
|Tags |JSON Map |{'db.user':'test','db.operation':'SELECT'} |The various tags of the Span. |
|CmdKey |String |get test_key |This parameter is used to identify the command for KV storage, such as get xx. |
|SpanId |String |df5f582b529xxxxx |The ID that corresponds to the Span. |
|Status |Integer |0 |The Span status code. |
|ApiName |String |DemoMethod |The API name. |
|ApiTime |Long |1767196800 |The server reception time, which corresponds to the report time on the page. |
|KeyInfo |Object of [KeyInfo](https://docs.byteplus.com/en/docs/299/84297#keyinfo) |\- |The core execution statement of the Span. If it is displayed for database operations, the value is an SQL statement. If it is used for KV storage operations, the value is a command. |
|Summary |String |GET /mysql \-\u003e demo\-http\-to\-grpc\-svc:port |The summary of the Span. |
|TraceId |String |58f56847851be99ea0ff3cxxxxxxxxxx |The trace ID that corresponds to the request. |
|Hostname |String |demo\-grpc\-server\-7f89c4677c\-xxxxx |The hostname. |
|SpanType |String |server |The Span type, such as server and client. |
|ErrorList |Array of [TraceErrorInfo](https://docs.byteplus.com/en/docs/299/84297#traceerrorinfo) |\- |The error in the Span, which corresponds to the error stack trace on the page. |
|EventList |Array of [Event](https://docs.byteplus.com/en/docs/299/84297#event) |\- |The event list in the Span, which corresponds to the event list on the page. |
|GenAIInput |String |Hello |The input for requesting the large language model. |
|InstanceId |String |demo\-grpc\-server\-7f89cxxx\-xxx.demo\-grpc\-server |Instance ID. |
|SqlPattern |String |SELECT \* FROM test WHERE id = ? |The SQL statement pattern. |
|CallApiName |String |DemoMethod2 |The downstream API name. |
|ContainerId |String |8c41415391508d5345e3c92bxxxx |The container ID. |
|GenAIOutput |String |Hello! How can I help you today? |The output of the large language model. |
|ServiceName |String |test\-grpc\-server |The service name. |
|ServiceType |String |rpc |The service type. |
|ParentSpanId |String |1b5430d4ddxxxxx |The parent Span ID. |
|OperationName |String |demoGrpc.DemoService/DemoMethod |The operation performed by the Span. |
|CallServiceName |String |test\-grpc\-server2 |The downstream service. |
|CallServiceType |String |rpc |The downstream service type. |
|CallResourceName |String |DemoMethod2 |The downstream resource name. It is equivalent to call_api_name, resource. |
|ProcessStartTime |Long |1767196800000000 |The time when the process started, which is create_time. |
|DurationMicroseconds |Long |1096 |The duration of the Span. Unit: microseconds. |
|StartTimeMicrosecond |Long |1767196800000000 |The time when the Span occurred, which corresponds to the start time on the page. This field is accurate to microseconds. |
|StartTimeMillisecond |Long |1767196800000 |The time when the Span occurred, which corresponds to the start time on the page. This field is accurate to the millisecond. |


<span id="keyinfo"></span>
### KeyInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Value |String |SELECT \* FROM test WHERE id = 233xxx |This parameter is used to identify the core execution statement. |


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


<span id="event"></span>
### Event


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Tags |JSON Map |{'message.id':'1.0','message.type':'RECEIVED'} |The event tag. |
|TraceId |String |58f56847851be99ea0ff3cxxxxxxxxxx |The ID of the trace to which the event belongs. |
|EventName |String |message |The event name. |
|ServiceName |String |demo\-service |The service to which the event belongs. |
|OperationName |String |Get |The event operation name. |
|EventTimeMillisecond |Long |1767196800000 |The event occurrence time. Unit: millisecond. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "SpanList": [
            {
                "PId": 0,
                "Sql": "SELECT * FROM test WHERE id = 233xxx", 
               "CmdKey": "get test_key",
                "SpanId": "df5f582b529xxxxx",
                "Status": 0,
                "ApiName": "DemoMethod",
                "ApiTime": 1767196800,
                "KeyInfo": {
                    "Value": "SELECT * FROM test WHERE id = 233xxx"
                },
                "Summary": "GET /mysql -\\u003e demo-http-to-grpc-svc:port",
                "TraceId": "58f56847851be99ea0ff3cxxxxxxxxxx",
                "Hostname": "demo-grpc-server-7f89c4677c-xxxxx",
                "SpanType": "server",
                "ErrorList": [
                    {
                        "IssueId": "b7d963c267c30e7c5ddexxxx",
                        "ErrorKind": "UncaughtException",
                        "ErrorStack": "java.lang.RuntimeException: Node not found\\n\\tat com.example.grpcserver.xxx.demoMethod(xxx.java:34)\\....",
                        "ErrorMessage": "Node not found",
                        "ErrorOccurTime": 1767196800
                    }
                ],
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
                "GenAIInput": "Hello",
                "InstanceId": "demo-grpc-server-7f89cxxx-xxx.demo-grpc-server",
                "SqlPattern": "SELECT * FROM test WHERE id = ?",
                "CallApiName": "DemoMethod2",
                "ContainerId": "8c41415391508d5345e3c92bxxxx",
                "GenAIOutput": "Hello! How can I help you today?",
                "ServiceName": "test-grpc-server",
                "ServiceType": "rpc",
                "ParentSpanId": "1b5430d4ddxxxxx",
                "OperationName": "demoGrpc.DemoService/DemoMethod",
                "CallServiceName": "test-grpc-server2",
                "CallServiceType": "rpc",
                "CallResourceName": "DemoMethod2",
                "ProcessStartTime": 1767196800000000,
                "DurationMicroseconds": 1096,
                "StartTimeMicrosecond": 1767196800000000,
                "StartTimeMillisecond": 1767196800000
            }
        ]
    },
    "ResponseMetadata": {
        "Action": "ListSpan",
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
