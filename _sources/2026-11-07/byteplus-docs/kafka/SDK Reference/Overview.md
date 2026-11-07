---
title: "Overview"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/SDK-overview"
---

Byteplus Engine message queue Kafka version is fully compatible with the open source Kafka protocol and supports multi\-language SDK. The client side can access the message queue Kafka version through VPC network and public network access, and send and receive messages. The message queue Kafka version provides sample projects for message production and consumption, and provides reference documents. Based on the example project, it introduces the main process of using the client side to access the Byteplus Engine message queue Kafka version to receive and send messages.

<span id="a29c2594"></span>
## SDK type

Message queue Kafka Edition instances are fully compatible with the open source Kafka protocol and can be connected directly using the Kafka open source client side.


|**SDK type** |**Purpose and description** |
|---|---|
|Apache Kafka client side SDK |Message queue for Kafka is fully compatible with open source Apache Kafka and supports the production and consumption of messages through the open source Kafka SDK. The open source Kafka SDK is usually integrated into client side programs to manage resources and data in Kafka instances, such as production messages, consumption messages.<br><br>Message queue Kafka version provides Go, Java and other multi\-language example projects for your reference, including sample code for message production and message consumption under various mechanisms. For details, please refer to:<br><br><br>* [Kafka Java client side SDK](https://docs.byteplus.com/en/docs/kafka/Apache-Java-SDK-overview)<br><br>* [Kafka Go client side SDK](https://docs.byteplus.com/en/docs/kafka/Apache-Go-overview) |


<span id="6060a05c"></span>
## Restrictions


|**Category** |**Restriction statement** |
|---|---|
|Produce message |* For scenarios where the delay of the message is sensitive, it is recommended to pass `linger.ms=0` Set up send optimization.<br><br>* When the message fails to be sent, a retry mechanism is required. You can configure the number of retries through the parameter retries. It is recommended to retry 3 times.<br><br>* The production callback function cannot block, otherwise it will cause problems such as blocking the sending of client side messages.<br><br>* It is recommended to reserve enough JVM memory on the production side to avoid problems such as sending blocking due to insufficient memory. |
|Consume message |* In special scenarios, Kafka may have repeated consumption, and the business side needs to ensure the idempotence of message processing.<br><br>* It is recommended to set the local cache size of messages pulled by consumers reasonably to avoid out\-of\-memory (OOM).<br><br>* When the consumer thread exits, the close method of the consumer should be called to avoid other consumers in the same group blocking sesstion.timeout.ms time.<br><br>* If the owner thread of the consumer exits abnormally, it may cause the client side to fail to initiate a consumption request, causing problems such as blocking consumption, so it is necessary to ensure the stability of the owner thread.<br><br>* When consuming messages using the long connection poll mode, closing the consumer channel immediately after consumption will result in frequent rebalancing, blocking consumption progress.<br><br>* It is recommended that consumers set the interval of periodic polling to 200 milliseconds to maintain the heartbeat state of the server to avoid frequent joining and exiting of consumers due to heartbeat timeout, blocking the consumption progress.<br><br>* Depending on the business situation, a reasonable value should be set for the consumer's session, such as 30 seconds with the following parameter: session.timeout.ms = 30000.<br><br>* It is recommended that the number of consumers does not exceed the number of partitions of the topic, otherwise some consumers will not be able to pull the message.<br><br>* It is recommended to do the message commit after processing the message, otherwise when the business message processing fails, the failed message cannot be re\-pulled. |
