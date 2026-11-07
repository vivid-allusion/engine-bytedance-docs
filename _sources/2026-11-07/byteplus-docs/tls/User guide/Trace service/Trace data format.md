---
title: "Trace data format"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/trace_data_format"
---

Torch Log Service (TLS) supports the data format defined in the OpenTelemetry protocol. This topic describes the fields defined when trace data is collected.

After trace data is collected and written to TLS, the data is stored in a specific topic in the format of key\-value pairs and key\-value indexing is enabled. The following table describes the trace data fields defined by TLS:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The trace data format is compatible with the standard data format in the <a href="https://opentelemetry.io/docs/concepts/signals/traces/">OpenTelemetry</a> protocol. Trace data written to TLS using the OpenTelemetry protocol can be automatically mapped to the trace data format of OpenTelemetry.</div>



|**Field** |**Data Type** |**Example** |**Description** |
|---|---|---|---|
|Name |String |Poll |The span name. |
|TraceID |String |e29a0a64fd256081ad57e983d260xxxx |The trace ID to which the span belongs in hexadecimal format. |
|SpanID |String |198b93e4fc50xxxx |The span ID in hexadecimal format. |
|TraceState |String |lasterror=f39cd56cc44274fd5abd07ef1164246d10cexxxx |The custom key\-value pair, which is optional. |
|ParentSpanID |String |198b93e4fc50xxxx |The upper\-level span ID of the current span. The ParentSpanID of the first span is empty. |
|Kind |String |SERVER |The span type, such as SERVER and CLIENT. |
|Start |Integer |1683032165241  |The span start time. The value is a Unix timestamp. Unit: milliseconds. |
|End |Integer |1683032220248  |The span end time. The value is a Unix timestamp. Unit: milliseconds. |
|Duration |Integer |55007  |The span duration. The value is the difference between the start time and end time. Unit: milliseconds. |
|Attributes |JSON |{"component": "net/http", "http.method": "GET", "http.status_code": 200, "http.url": "0.0.0.0:8083", "net/http.reused": true, “net/http.was_idle”: true} |The attribute information about the span. For more information, refer to [Attribute Naming](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/common/attribute-naming.md). |
|Events |JSON |[ { "Attributes": { "event": "GetConn" }, "Name": "", "Time": 1684420552720997000 }, { "Attributes": { "event": "ClosedBody" }, "Name": "", "Time": 1684420552786987000 } ] |The event information about the span. The value is a JSON string. |
|Links |JSON |[{"TraceID" : "e29a0a64fd256081ad57e983d260\*\*\*\*", "SpanId" : "198b93e4fc50\*\*\*\*", "TraceState" : "Client", "Attributes" : {} }] |The associated span. The value is a JSON string. |
|StatusCode |String |OK |The status code, which can be OK, ERROR, or UNSET. |
|StatusDescription |String |Success |The status description. |
|Resource |JSON |{"environment":"demo","service.name":"fib","service.version":"v0.1.0","telemetry.sdk.language":"go","telemetry.sdk.name":"opentelemetry","telemetry.sdk.version":"1.11.0"} |The resource fields. For more information, refer to [Resource Semantic Conventions](https://github.com/open-telemetry/opentelemetry-specification/tree/main/specification/resource/semantic_conventions). |
|ServiceName |String |TLS_OTEL_SERVICE |The source service name of the span, that is, the value of **service.name** in **resource**. |
|Host |String |localhost |The source host name of the span, that is, the value of **host.name** in **resource**. |
|OTLPName |String |opentelemetry |The trace SDK name. |
|OTLPVersion |String |1.11.0 |The trace SDK version. |
