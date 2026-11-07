---
title: "SDK for Python overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_python_overview"
---

Torch Log Service (TLS) SDK for Python encapsulates commonly used API actions of TLS. You can use TLS SDK for Python to call server\-side API actions to implement features such as collecting and querying logs.

<span id="版本说明"></span>
## Release notes

For information on the update logs and release notes of TLS SDK for Python, visit [GitHub](https://github.com/volcengine/volc-sdk-python). We recommend that you use the latest version of the SDK to use the latest product capabilities and more stable services.

<span id="示例项目"></span>
## Sample projects

TLS SDK for Python offers sample projects for your reference, including log collection and resource management. For more information, refer to the source code on GitHub.


|Source Code on GitHub |Description |
|---|---|
|[example_project.py](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/tls/example_project.py) |Includes sample code of project management, demonstrating how to create, modify, view, and delete projects. |
|[example_topic.py](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/tls/example_topic.py) |Includes sample code of topic management, demonstrating how to create, modify, view, and delete topics. |
|[example_index.py](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/tls/example_index.py) |Includes sample code of log index management, demonstrating how to create, modify, query, and delete indexes. |
|[example_log.py](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/tls/example_log.py) |Includes sample code of log management, demonstrating how to upload logs, query cursors, consume logs, and query logs. |
|[example_host_group.py](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/tls/example_host_group.py) |Includes sample code of host group management, demonstrating how to create, modify, query, and delete host groups, how to query and delete hosts, and how to query collection rules of host groups. |
|[example_rule.py](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/tls/example_rule.py) |Includes sample code of collection rule management, demonstrating how to create, modify, query, and delete collection rules, apply collection rules to host groups, and delete collection rules from host groups. |
|[example_alarm.py](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/tls/example_alarm.py) |Includes sample code of alarm management, demonstrating how to create, modify, query, and delete alarm notification groups, and how to create, modify, query, and delete alarm policies. |
|[example_consumer.py](https://github.com/volcengine/volc-sdk-python/blob/main/volcengine/example/tls/example_consumer.py) |Includes sample code that demonstrates how to use consumer groups to consume logs. Python Consumer can consume the data of all shards in a topic in a balanced way. Python Consumer features asynchronous consumption, high performance, retry on failure, and graceful shutdown. We recommend that you use Python Consumer to consume logs. |
