---
title: "Overview"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Overview_2"
---

This topic provides information about using the RabbitMQ Java client SDK to access Message Queue for RabbitMQ for sending and receiving messages.

<span id=".5o6l5YWl5Y2P6K6u"></span>
## Access protocol

Cloud\-hosted RabbitMQ service is fully compatible with open\-source RabbitMQ, supporting clients in configuring routing, sending and receiving messages, and more via the AMQP protocol. Meanwhile, Message Queue for RabbitMQ also supports extension management. After enabling the `rabbitmq_mqtt` extension, access via the MQTT protocol is supported.

<span id=".54mI5pys5pSv5oyB"></span>
## Supported versions

Message Queue for RabbitMQ uses open\-source `3.8.18` and `3.12` versions, and supports important features such as [Quorum Queues](https://www.rabbitmq.com/quorum-queues.html) and [Feature Flags](https://www.rabbitmq.com/feature-flags.html).

<span id=".6K6_6Zeu5pa55byP"></span>
## Access methods

RabbitMQ currently supports public network access and cloud VPC access.


* VPC is an isolated, configurable, and manageable virtual network environment for cloud resources, ensuring the security of messages during network transmission.

* When building connection between client and instance, SSL authentication is required. Enabling public network access automatically enables SSL. After enabling SSL, data is transmitted encrypted and higher security is provided. You can also enable public network access and SSL authentication after creating an instance. For a detailed description, please refer to [Enable public network access](https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access).

   * SSL encrypted transmission is supported only in public network environments.

   * For security reasons, after you enable Public network access, SSL is enabled by default and SSL encryption is used for transmission, and during Public network access, disabling SSL authentication is not supported.


<span id=".5byA5rqQIFJhYmJpdE1RIFNESyDliJfooag="></span>
## List of open\-source RabbitMQ SDKs

RabbitMQ supports the [AMQP 0-9-1](https://www.amqp.org/specification/0-9-1/amqp-org-download) protocol and the MQTT protocol. Users can use any SDK that implements both the AMQP 0\-9\-1 protocol and the MQTT protocol to send and receive messages. For documentation on common programming languages and their corresponding SDK usage, please refer to the table below. For more information about the open\-source RabbitMQ SDK, please refer to [Clients Libraries and Developer Tools](https://www.rabbitmq.com/devtools.html).


|**Language or framework** |**SDK** |
|---|---|
|Java |[RabbitMQ Java Client Library](https://www.rabbitmq.com/java-client.html) |
|Spring Framework |[Spring AMQP project for Java](https://spring.io/projects/spring-amqp) |
|.NET |[.NET SDK](https://www.rabbitmq.com/devtools.html#dotnet-dev) |
|Python |[Python SDK](https://www.rabbitmq.com/devtools.html#python-dev) |
|PHP |[PHP SDK](https://www.rabbitmq.com/devtools.html#php-dev) |
|Rust |[Rust SDK](https://www.rabbitmq.com/devtools.html#rust-dev) |
|C and C++ |[C and C++ SDK](https://www.rabbitmq.com/devtools.html#c-dev) |
|Go |[Go SDK](https://www.rabbitmq.com/devtools.html#go-dev) |
|JavaScript and Node |[JavaScript and Node SDK](https://www.rabbitmq.com/devtools.html#node-dev) |
|Objective\-C and Swift |[Objective-C and Swift SDK](https://www.rabbitmq.com/devtools.html#objc-swift-dev) |


<span id=".U0RL57G75Z6L"></span>
## SDK type

Message Queue for RabbitMQ instances are fully compatible with the open\-source RabbitMQ protocol and can be connected directly using the open\-source RabbitMQ client.


|**SDK type** |**Usage and description** |
|---|---|
|Open source RabbitMQ SDK |Message Queue for RabbitMQ is fully compatible with open\-source Apache RabbitMQ and supports producing and consuming messages through the open\-source RabbitMQ SDK. The open\-source RabbitMQ SDK is typically integrated into client applications to manage resources and data in RabbitMQ instances, such as producing and consuming messages. Message Queue for RabbitMQ provides sample projects in Java for your reference, including example code for message production and consumption using various mechanisms. For more information, refer to the Java SDK. |
|OpenAPI SDK |Provides multilingual SDKs for the data plane, allowing you to call the OpenAPI of various services. By calling API endpoints, you can manage cloud resources without the need for signature and authentication processes, enabling rapid integration with cloud services. Message Queue for RabbitMQ has been integrated with the OpenAPI SDK. You can refer to the following documentation to install and use the SDK.<br><br><br>* [An overview of the Java SDK](https://api.volcengine.com/api-sdk/view?serviceCode=RabbitMQ&version=2022-01-01&language=Java)<br><br>* [Go SDK overview](https://api.volcengine.com/api-sdk/view?serviceCode=RabbitMQ&version=2022-01-01&language=Golang)<br><br>* [Python SDK overview](https://api.volcengine.com/api-sdk/view?serviceCode=RabbitMQ&version=2022-01-01&language=Python) |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

For sample code on sending and receiving messages with RabbitMQ, refer to the official RabbitMQ documentation [RabbitMQ SDK usage examples](https://rabbitmq.com/getstarted.html) and the sample code project for common scenarios on [GitHub](https://github.com/rabbitmq) called [rabbitmq-tutorials](https://github.com/rabbitmq/rabbitmq-tutorials). In addition, Message Queue for RabbitMQ provides the following example projects for your reference:


* [AMQP protocol Java SDK demo](https://rabbitmq-demo.tos-cn-beijing.volces.com/AMQP-DEMO.zip)

* [Java SDK demo for the MQTT protocol](https://rabbitmq-demo.tos-cn-beijing.volces.com/MQTT-DEMO.zip)
