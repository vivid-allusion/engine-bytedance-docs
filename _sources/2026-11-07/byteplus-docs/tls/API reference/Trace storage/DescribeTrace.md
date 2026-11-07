---
title: "DescribeTrace"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeTrace"
---

Call the DescribeTrace API to query the list of spans under a trace using the specified trace instance ID and TraceID

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: POST

* Request URL: https://{tls\-endpoint}/DescribeTrace


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API and some common parameters For more details, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters)

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TraceId |String |Yes |`ef97a7****` |Trace ID. |
|TraceInstanceId |String |Yes |0fdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |Trace instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below only lists the response parameters specific to this API. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Trace |Object of [Trace](https://docs.byteplus.com/en/docs/38/83201#trace) |/ |Trace details, including the list of all Spans under this Trace. |


<span id="trace"></span>
### Trace


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Spans |Array of [Span](https://docs.byteplus.com/en/docs/38/83201#span) |/ |Contains the list of all spans under this trace. Each span represents an operation or event and includes details such as operation type, name, and timestamp. |


<span id="span"></span>
### Span


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Kind |String |SPAN_KIND_SERVER |The type of Span, used to identify the role of this Span in distributed tracing. The supported values are as follows.<br><br><br>* `SPAN_KIND_UNSPECIFIED`: Unspecified type;<br><br>* `SPAN_KIND_INTERNAL`: internal operation<br><br>* `SPAN_KIND_SERVER`: server receives request<br><br>* `SPAN_KIND_CLIENT`: client sends request<br><br>* `SPAN_KIND_PRODUCER`: message producer<br><br>* `SPAN_KIND_CONSUMER`: message consumer |
|Name |String |HTTP GET /api/users |`The name of the Span` identifies the operation or event represented by this `Span`. |
|Links |Array of [SpanLink](https://docs.byteplus.com/en/docs/38/83201#spanlink) |[{"SpanId":"3e4f5a6b7c8d9e0f","TraceId":"1a2b3c4d5e6f7g8h","Attributes":[{"Key":"link.type","Value":"child"}],"TraceState":"vendor1=value1,vendor2=value2"}] |`Link list of the Span` shows the associations between the current `Span` and other `Spans`. Each link contains the target `Span`’s `TraceId` and `SpanId`, as well as optional attributes and trace states. |
|Events |Array of [SpanEvent](https://docs.byteplus.com/en/docs/38/83201#spanevent) |[{"Name":"cache.hit","Timestamp":1622548800000000,"Attributes":[{"Key":"cache.key","Value":"user_123"}]}] |`Span` event list, used to record specific events in the `Span` lifecycle. Each event contains a name, timestamp, and an optional list of attributes. |
|SpanId |String |3e4f5a6b7c8d\*\*\*\* |ID that uniquely identifies a `Span` within a `Trace`, used to distinguish different operations or events. |
|Status |Object of [Status](https://docs.byteplus.com/en/docs/38/83201#status) |{"Code":"OK","Message":"Operation successful"} |`Status information for the Span` includes a status code and error message. Status codes are as follows.<br><br><br>* `UNSET`: Status not set<br><br>* `OK`: Operation succeeded<br><br>* `ERROR`: Operation failed. |
|EndTime |Integer |1622548800000000 |End time of `Span`, measured in microseconds, indicating when the operation or event was completed. |
|TraceId |String |ef97a7\*\*\*\* |Trace ID. |
|Resource |Object of [Resource](https://docs.byteplus.com/en/docs/38/83201#resource) |/ |Resource information associated with `Span`, including a list of attributes describing the resource. |
|StartTime |Integer |1622548800000000 |Start time of the `Span` in microseconds, representing when the operation or event began. |
|Attributes |Array of [KeyValue](https://docs.byteplus.com/en/docs/38/83201#keyvalue) |[{"Key":"http.method","Value":"GET"},{"Key":"http.status_code","Value":"200"}] |Property list of `Span`, used to store additional information related to `Span`. Each property consists of a key\-value pair. |
|TraceState |String |vendor1=value1,vendor2=value2 |`Trace` status information that follows the W3C Trace Context specification `tracestate` header format. It is used to pass vendor\-specific tracing status information. Separate multiple key\-value pairs with commas. Each pair consists of the vendor name and its corresponding value. |
|ParentSpanId |String |1a2b3c4d5e6f\*\*\*\* |Unique identifier of the parent `Span`, representing the direct parent `Span` of the current `Span`. If the current `Span` is the root node, this field is empty. |
|InstrumentationLibrary |Object of [InstrumentationLibrary](https://docs.byteplus.com/en/docs/38/83201#instrumentationlibrary) |{"Name":"opentelemetry\-java","Version":"1.0.0"} |`Span` detection library information, including the name and version of the detection library that generated this `Span`. |


<span id="spanlink"></span>
### SpanLink


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|SpanId |String |3e4f5a6b7c8d\*\*\*\* |An ID that uniquely identifies a `Span` within a `Trace`. It is used to distinguish different operations or events. |
|TraceId |String |ef97a7\*\*\*\* |Trace ID. |
|Attributes |Array of [KeyValue](https://docs.byteplus.com/en/docs/38/83201#keyvalue) |[{"Key":"http.method","Value":"GET"},{"Key":"http.status_code","Value":"200"}] |`Span` attribute list, used to store additional information related to the `Span`. Each attribute is a key\-value pair. |
|TraceState |String |vendor1=value1,vendor2=value2 |Status information of `Trace`, following the `tracestate` header format in the W3C Trace Context specification, used to transmit vendor\-specific trace state information. Separate multiple key\-value pairs with commas. Each pair consists of a vendor name and the corresponding value. |


<span id="spanevent"></span>
### SpanEvent


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Name |String |cache.hit |`Span` event name used to identify specific events that occur in a `Span`'s lifecycle, such as cache hits or database queries. |
|Timestamp |Integer |1622548800000000 |Timestamp of the `Span` event in microseconds, indicating the exact time when the event occurred. |
|Attributes |Array of [KeyValue](https://docs.byteplus.com/en/docs/38/83201#keyvalue) |[{"Key":"http.method","Value":"GET"},{"Key":"http.status_code","Value":"200"}] |`Span` attribute list, used to store additional information related to the `Span`. Each attribute is made up of a key\-value pair. |


<span id="status"></span>
### Status


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Code |String |OK |The status code of `Span` indicates the result of the operation or event represented by this `Span`. Supported values are as follows.<br><br><br>* `UNSET`: Status not set.<br><br>* `OK`: Operation successful.<br><br>* `ERROR`: Operation failed. |
|Message |String |/ |Error message in `Span` status, describing the specific cause or details of an operation failure. |


<span id="resource"></span>
### Resource


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Attributes |Array of [KeyValue](https://docs.byteplus.com/en/docs/38/83201#keyvalue) |[{"Key":"service.name","Value":"user\-service"},{"Key":"service.version","Value":"1.0.0"},{"Key":"deployment.environment","Value":"production"}] |`Span` attribute list for linked resources, used to describe additional information about the resource. Each attribute consists of a key\-value pair. |


<span id="keyvalue"></span>
### KeyValue


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Key |String |http.method |The key of the `Span` attribute is used to identify the attribute name, usually to store additional information related to `Span`, such as HTTP methods or status codes. |
|Value |String |GET |Specific values of the `Span` attribute are used to store additional information related to the `Span`, such as HTTP method and status code. |


<span id="instrumentationlibrary"></span>
### InstrumentationLibrary


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Name |String |opentelemetry\-java |The name of the detection library that generated this `span`, used to identify the library or framework that created the `span`. |
|Version |String |1.0.0 |The version number of the detection library for this `Span` identifies the specific library or framework version that created the `Span`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://{tls-endpoint}/DescribeTrace HTTP/1.1
Content-Type: application/json
{
    "TraceId": "ef97a7****",
    "TraceInstanceId": "0fdaa6b6-3c9f-424c-8664-fc0d222c****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "Trace": {
        "Spans": [
            {
                "Kind": "SPAN_KIND_SERVER",
                "Name": "HTTP GET /api/users",
                "Links": [
                    {
                        "SpanId": "3e4f5a6b7c8d9e0f",
                        "TraceId": "1a2b3c4d5e6f7g8h",
                        "Attributes": [
                            {
                                "Key": "link.type",
                                "Value": "child"
                            }
                        ],
                        "TraceState": "vendor1=value1,vendor2=value2"
                    }
                ],
                "Events": [
                    {
                        "Name": "cache.hit",
                        "Timestamp": 1622548800000000,
                        "Attributes": [
                            {
                                "Key": "cache.key",
                                "Value": "user_123"
                            }
                        ]
                    }
                ],
                "SpanId": "3e4f5a6b7c8d****",
                "Status": {
                    "Code": "OK",
                    "Message": "Operation successful"
                },
                "EndTime": 1622548800000000,
                "TraceId": "ef97a7****",
                "Resource": {
                    "Attributes": [
                        {
                            "Key": "service.name",
                            "Value": "user-service"
                        },
                        {
                            "Key": "service.version",                            "Value": "1.0.0"
                        },
                        {
                            "Key": "deployment.environment",
                            "Value": "production"
                        }
                    ]
                },
                "StartTime": 1622548800000000,
                "Attributes": [
                    {
                        "Key": "http.method",                        "Value": "GET"
                    },
                    {
                        "Key": "http.status_code",
                        "Value": "200"
                    }
                ],
                "TraceState": "vendor1=value1,vendor2=value2",
                "ParentSpanId": "1a2b3c4d5e6f****",
                "InstrumentationLibrary": {
                    "Name": "opentelemetry-java",
                    "Version": "1.0.0"
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Public Error Code](https://docs.byteplus.com/en/docs/tls/common-error-codes) to get more information about error codes.
