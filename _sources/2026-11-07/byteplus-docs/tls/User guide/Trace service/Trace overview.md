---
title: "Trace overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/trace_overview"
---

Trace is a distributed tracing feature offered by Torch Log Service (TLS). Trace is built based on the native OpenTelemetry protocol and standards. It allows you to integrate, store, query, analyze, view, and perform other operations on trace data, achieving end\-to\-end trace data observability. This topic describes the trace feature, its limits, and integration methods.

<span id=".5Yqf6IO9566A5LuL"></span>
## Feature description

In cloud\-native, microservice, and distributed architectures or systems, multiple services interact with each other, and one request is often processed by multiple microservices. In addition, a performance issue may involve multiple services and components. As distributed systems grow in size and complexity, it is more challenging to understand how requests go through paths and components in systems. Distributed tracing allows you to get the complete call chain and view of a request in the system, trace the path of abnormal signals, and monitor the execution process of an entire transaction. This helps you understand the performance metrics of each microservice to locate and solve issues in time.

Trace offers distributed tracing capabilities based on the [OpenTelemetry](https://opentelemetry.io/docs/what-is-opentelemetry/) (OTel) protocol. It is suitable for scenarios such as performance enhancement, troubleshooting, microservice architecture monitoring, service call chain analysis, distributed transaction tracing, and security audit. OpenTelemetry offers a cross\-language specification that unifies all observability data, and also offers language\-specific SDKs implemented based on the OpenTelemetry API. The SDKs allow you to customize the collection of observability data. After trace data is integrated into TLS, TLS records each end\-to\-end request and the context in time, and saves the data to the server in a unified format for queries, analysis, and data visualization.

Currently, the trace feature allows you to:


* Integrate and store various types of trace data.

* Query and analyze trace data online and in real time.


<span id=".55u45YWz6LWE5rqQ"></span>
## Related resources


|Resource |Description |
|---|---|
|Topic |When you create a trace instance, TLS automatically creates two topics. The two topics are:<br><br><br>* `tls_${TRACE_ INSTANCE_NAME}-trace`: Used for storing the collected original Trace data.<br><br>* `tls_${TRACE_ INSTANCE_NAME}-dependency`: Used for storing the topological relationship data that has been extracted from the original Trace data and then aggregated.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Manually deleting log topics is not supported, but the configuration of tls_${trace instance name}\-trace can be modified.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, trace data is retained in a topic for 30 days. Modify the time\-to\-live (TTL) as needed.</div><br> |
|Index |By default, TLS configures indexes for trace topics. Add index fields based on the default ones as needed. Do not modify or delete predefined index fields. Otherwise, trace instances become abnormal or query errors occur. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The trace feature is free of charge. However, resources such as topics, shards, data storage, and index storage involved when you use this feature incur fees based on the standard billing mode.

* To secure data, we recommend that you use the trace feature as a BytePlus IAM user. Make sure the IAM user is granted the permissions to operate trace instances and write data. For more information, refer to [Policy for granting permissions on the API actions for collecting trace data](https://docs.byteplus.com/en/docs/tls/Permissions_policy_template).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The number of trace instances that can be created in each BytePlus account depends on the number of topics that can be created in the project to which the trace instance belong.

* The trace function relies on the scheduling concurrency limitations of scheduled SQL tasks. For detailed descriptions, please refer to [Limits](https://docs.byteplus.com/docs/tls/scheduled_sql_overview#%E4%BD%BF%E7%94%A8%E9%99%90%E5%88%B6).

* The upload throughput and QPS for trace are aligned with the associated topic. If thresholds are exceeded, errors will occur. 

* When you query trace, the query QPS and data volume are aligned with the associated topic. If thresholds are exceeded, errors will occur. 

* The log topic name and index configuration of the dependency associated with the Trace instance cannot be modified. 

* When uploading spans, each span can not exceed 9 KiB. The maximum size per request is 4 MiB.


<span id=".5o6l5YWl5pa55qGI"></span>
## Integration methods

TLS allows you to integrate trace data into TLS using the native OpenTelemetry protocol. We recommend that you use one of the following methods to integrate trace data.


|Method |Description |Reference |
|---|---|---|
|OpenTelemetry SDK |OpenTelemetry offers language\-specific SDKs implemented based on the OpenTelemetry API. The SDKs can be used to collect trace data. The OpenTelemetry SDK allows you to write trace data to TLS over HTTPS or gRPC. |[Use the OpenTelemetry SDK to write data](https://docs.byteplus.com/docs/tls/use_the_opentelemetry_sdk_to_write_data) |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">We recommend that you use the open\-source OpenTelemetry protocol, OpenTracing standard, and OpenTelemetry standard to connect to TLS and other open\-source systems seamlessly.</div>


* <div data-tips="true" data-tips-type="tip">We recommend that you use the same method to integrate with the trace feature for each component and service in the system. This helps you collect and upload trace data in one stop.</div>
