---
title: " SDK for Go overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/go_sdk_overview"
---

Torch Log Service (TLS) SDK for Go encapsulates commonly used API actions of TLS. You can use TLS SDK for Go to call server\-side API actions to implement features such as collecting and querying logs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to basic features, TLS SDK for Go offers flexible and easy\-to\-use Golang class libraries: <a href="https://github.com/volcengine/volc-sdk-golang/tree/main/service/tls/producer">Go Producer</a> and <a href="https://github.com/volcengine/volc-sdk-golang/tree/main/service/tls/consumer">Go Consumer</a>.</div>



* <div data-tips="true" data-tips-type="tip">Go Producer sends log data quickly in massive data scenarios. For information on how to use Go Producer and set relevant parameters, visit <a href="https://github.com/volcengine/volc-sdk-golang/blob/main/service/tls/producer/producer.md">GitHub</a>.</div>


* <div data-tips="true" data-tips-type="tip">Go Consumer can consume log data in multiple topics of a project asynchronously. For information on how to use Go Consumer and set relevant parameters, visit <a href="https://github.com/volcengine/volc-sdk-golang/blob/main/service/tls/consumer/consumer.md">GitHub</a>.</div>



<span id="版本说明"></span>
## Release notes

For information on the update logs and release notes of TLS SDK for Go, visit [GitHub](https://github.com/volcengine/volc-sdk-golang/tags). We recommend that you use the latest version of the SDK to use the latest product capabilities and more stable services.

For information on the latest source code of TLS SDK for Go, refer to [TLS SDK for Go source code](https://github.com/volcengine/volc-sdk-golang/tree/main/service/tls).

<span id="示例项目"></span>
## Sample projects

TLS SDK for Go offers sample projects for your reference, including log collection and resource management. For more information, refer to the sample projects on GitHub.


|Sample Project on GitHub |Description |
|---|---|
|[Project management](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_project.go) |Includes sample code of project management, demonstrating how to create, modify, view, and delete projects. |
|[Topic management](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_topic.go) |Includes sample code of topic management, demonstrating how to create, modify, view, and delete topics. |
|[Log management](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_log.go) |Includes sample code of log collection and queries, demonstrating how to create resources, collect log data, configure indexes, query logs, and analyze logs. |
|[Sending logs using Go Producer](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_producer.go) |Includes sample code that demonstrates how Go Producer sends logs. Go Producer features asynchronous sending, high performance, retry on failure, and graceful shutdown. We recommend that you use Go Producer to send logs. |
|[Consuming logs using Go Consumer](https://github.com/volcengine/volc-sdk-golang/blob/main/example/tls/demo_consumer.go) |Includes sample code that demonstrates how Go Consumer consumes logs. Go Consumer consumes the data of all shards in a topic in a balanced way. Go Consumer features asynchronous consumption, high performance, retry on failure, and graceful shutdown. We recommend that you use Go Consumer to consume logs. |
