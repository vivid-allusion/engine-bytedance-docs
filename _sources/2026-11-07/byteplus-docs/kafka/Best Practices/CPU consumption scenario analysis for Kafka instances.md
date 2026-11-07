---
title: "CPU consumption scenario analysis for Kafka instances"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CPU-consumption-scenario-analysis"
---

This topic describes the scenarios in which a large number of CPU resources are consumed during the use of Kafka and offers optimization recommendations related to client usage for each scenario.

<span id="5c4bbe59"></span>
## Background information

Kafka is not a computing\-intensive product based on its orientation and design. The business traffic of a Kafka instance is reflected in the network bandwidth usage and disk throughput. No concern on the CPU usage is required in daily use. However, because scenarios vary in actual production environments, CPU may be a bottleneck for Kafka instances in some business models.

Currently, the scenarios with high CPU consumption on Kafka instances include the excessively high request rate and the message format version of the client being earlier than the Kafka instance version.

<span id="c28df276"></span>
## Excessively high request rate

The issue of the excessively high request rate has been considered during the design and implementation of Kafka clients.


* A Kafka client itself is not designed to send messages synchronously. When an API action is called for sending messages, messages are not directly sent to the Kafka instance but are cached in the client memory. All sent messages are aggregated in the memory cache. Later, an asynchronous sending thread maintained in the client back\-end constantly reads data from the memory cache and sends the data to the Kafka instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you focus on the callback function for message sending results as the asynchronous message sending mode is used for Kafka.</div>



* For message consumption, the Kafka client uses a pull mode and actively initiates requests to read messages. Messages are read in batches each time, and the read results are cached in the local memory. Later, data is read from the memory cache by calling API actions.


Although batch aggregation is adopted for message sending and consumption, the request rate is excessively high in some scenarios. This is because the default configurations of Kafka prioritize speed so that the producer client can send messages and the consumer client can consume messages as soon as possible. Therefore, the default configurations cannot meet the business requests in scenarios with relatively large user business volume.

Generally, excessive requests are caused by the following factors:


|Main Factor |Description |
|---|---|
|Too small message size per request by the producer |To send 1 MB of data, if 1 KB of data is sent per request, a total of 1,024 requests are required. However, if 10 KB of data is sent per request, only 102 requests must be sent.<br><br>You can optimize the producer client by using the following parameters:<br><br><br>* batch.size: controls the size of messages that are aggregated on the producer client in each partition. The default value is 16 KB. If the production traffic is high, you can increase the value of this parameter, for example, to 512 KB.<br><br>* linger.ms: controls the aggregation period of messages in each partition. The default value is 0 ms. If the writing frequency of the producer is not high, adjusting `batch.size` alone may not have a significant effect. You must also adjust the value of this parameter for optimization, for example, to 50 ms.<br><br>* send.buffer.bytes: controls the size of a TCP send buffer. The default value is 128 KB. After adjusting `batch.size`, you can also adjust this parameter, for example, to 1 MB, to ensure prompt message sending from the TCP buffer. |
|Too small message size per pull by the consumer |Similar to message production, if more messages are pulled per time, fewer pull requests are required to read the same amount of data.<br><br>You can control the message size per pull by setting the following parameters for the consumer client.<br><br><br>* fetch.min.bytes: controls the minimum message size per pull. The default value is 0 KB. If the size of the read messages is greater than specified minimum message size, the request is returned by the Kafka instance until the minimum message size is met or after a short period, which defaults to 500 ms. Therefore, when the consumption data volume is high, you can adjust this parameter appropriately, for example, to 1 MB, to lower the consumption request rate.<br><br>* receive.buffer.bytes: controls the size of a TCP receive buffer. The default value is 64 KB. If the business volume is high, you can adjust this parameter appropriately, for example, to 1 MB. |
|Frequent consumer offset commit |The message consumption progress is usually persisted in the Kafka instance through consumer offset commit requests. As a result, frequent consumer offset commits also lead to increased CPU usage of the Kafka instance. We recommend that the consumer offset be committed based on a specific time interval, rather than based on the number of consumed messages. This ensures that the consumer offset commit does not increase due to the growth in business volume. |
|Too many clients |In addition to too many requests from a single client, the total requests can also be excessively high when an instance is accessed by many clients, even if a few requests are sent from a single client. In this case, we recommend you use an instance with larger CPU specifications or optimize your own business. |


<span id="fd3a4ee9"></span>
## Outdated message format version of the client

Up to now, Kafka has undergone two iterations of message format versions. The first one is version 0.10, and the second one is version 0.11. Currently, BytePlus Message Queue for Kafka supports the latest message format version. If the message format versions on the client and the Kafka instance are inconsistent, messages are converted into a local message format of the Kafka instance before being stored on the Kafka instance. Similarly, this message format is further converted into the format supported by the consumer for message consumption. This process consumes more CPU resources.

In this case, we recommend that you update the client version to ensure no message conversion due to inconsistent message format during message production and consumption. Currently, BytePlus Message Queue for Kafka supports the message format of v2. Therefore, a client of version 2.2 or later is recommended.
