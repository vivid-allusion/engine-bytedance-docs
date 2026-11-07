---
title: "SDK for Java overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_java_overview"
---

Torch Log Service (TLS) SDK for Java encapsulates commonly used API actions of TLS. You can use TLS SDK for Java to call server\-side API actions to implement features such as collecting and querying logs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to basic features, TLS SDK for Java offers a flexible and easy\-to\-use class library: <a href="https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/ProducerDemo.java">Java Producer</a>, which sends log data quickly in massive data scenarios. For more information, visit <a href="https://github.com/volcengine/volc-sdk-java/blob/main/volc-sdk-java/src/main/java/com/volcengine/model/tls/producer/Producer.md">GitHub</a>.</div>


<span id="版本说明"></span>
## Release notes

For information on the update logs and release notes of TLS SDK for Java, visit [GitHub](https://github.com/volcengine/volc-sdk-java/tags). We recommend that you use the latest version of the SDK to use the latest product capabilities and more stable services.

<span id="示例项目"></span>
## Sample projects

TLS SDK for Java offers sample projects for your reference, including log collection and resource management. For more information, refer to the source code on GitHub.


|Source Code on GitHub |Description |
|---|---|
|[ProjectDemo.java](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/ProjectDemo.java) |Includes sample code of project management, demonstrating how to create, modify, view, and delete projects. |
|[TopicDemo.java](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/TopicDemo.java) |Includes sample code of topic management, demonstrating how to create, modify, view, and delete topics. |
|[IndexDemo.java](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/IndexDemo.java) |Includes sample code of log collection and queries, demonstrating how to create resources, collect log data, configure indexes, query and analyze logs. |
|[ProducerDemo.java](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/ProducerDemo.java) |Includes sample code that demonstrates how Java Producer sends logs. Java Producer features asynchronous sending, high performance, retry on failure, and graceful shutdown. We recommend that you use Java Producer to send logs. |
|[ConsumerDemo.java](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/tls/demo/ConsumerDemo.java) |Includes sample code that demonstrates how Java Consumer consumes logs. Java Consumer consumes the data of all shards in a topic in a balanced way. Go Consumer features asynchronous consumption, high performance, retry on failure, and graceful shutdown. We recommend that you use Java Consumer to consume logs. |
