---
title: "Upload logs based on Flume"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Upload-logs-based-on-flume"
---

Flume is a distributed, highly reliable, and highly available massive log collection, aggregation, and transport system that enables the collection and aggregation of data from individual applications into a single data storage system. This topic describes how to upload data to TLS through Flume's Kafka Sink.

<span id="1169bbb5"></span>
## Background information

When Flume is used as a data collection tool, Flume's Kafka Sink supports sending data from the Flume channel to Kafka, while TLS supports receiving data through the Kafka protocol, so Flume can upload data to the topic of TLS through Kafka Sink.

<span id="0bb6fb80"></span>
## **Prerequisites**


* A project and a topic have been created.

* It is recommended to use IAM user for access authentication. Before using an IAM user, you need to confirm that you have created an IAM user and have the permission to upload logs through the Kafka protocol, that is, you have the `PutLogs`permission. For more information, see [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions).


<span id="0c1cc0cb"></span>
# Flume Configuration

When uploading data to TLS through Flume, you need to configure the Kafka Sink provided by Flume. Only the parameters required to upload data to TLS and the parameters that affect the data upload performance are listed here. For other parameter descriptions, please refer to [Kafka Sink ](https://flume.apache.org/releases/content/1.9.0/FlumeUserGuide.html#kafka-sink).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic takes Flume 1.9.0 version as an example. The configuration parameters of different Flume versions may be different. For details, please refer to the <a href="https://flume.apache.org/">Flume official website documentation </a>.</div>



|Parameter name |Required |Example Value |Description |
|---|---|---|---|
|Type |Yes |`Org.apache.flume.sink.kafka. KafkaSink` |It is must be configured as<br><br>`Org.apache.flume.sink.kafka. KafkaSink`. |
|Kafka.bootstrap.servers |Yes |`tls-cn-beijing.bytepluses.com:9094` |The cluster address of the initial connection, in the format of `service address: port`, where:<br><br><br>* service address is the service entry of TLS. Please select the correct service portal by region and network type, see [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br>* The port number is fixed to 9094.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The service address does not need to be specified <code>https://</code>.</div><br> |
|kafka.producer.security protocol |Yes |SASL_SSL |In order to ensure the security of data transmission, the connection protocol must be set to `SASL_SSL`. |
|Kafka.producer.sasl.mechanism |Yes |PLAIN |Set the authentication method for uploading data to TLS, which needs to be set to `PLAIN`. |
|Kafka.producer.sasl.jaas.config |Yes |None |The specific authentication configuration for uploading data to TLS, including username and password.<br><br><br>* Set `username`to the project ID of TLS.<br><br>* Set the `password`to the Byteplus account AccessKey. On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID and AccessKey secret as prompted. The configuration format here is `${access-key-id} #${access-key-secret}`.<br><br><br>```Properties```<br>```org.apache.kafka.common.security.plain.PlainLoginModule required username="Project ID" password="Byteplus account AccessKey";```<br> |
|Kafka. topic |No |F93fc61xxxxefec8a5 |The Kafka topic, where you need to configure the topic ID of TLS. When Flume uploads data, it is uploaded to this topic of TLS. |
|flumeBatchSize |No |100 |The number of data pieces uploaded each time. Larger values will increase throughput but also increase latency. The default value is 100. it is not recommended to modify this. |
|Kafka.producer.acks |No |1 |The message sending confirmation mechanism of Kafka producer. The default value is 1, indicating that the Leader broker was written successfully. It is not recommended to modify this. |
|Kafka.producer .batch.size |No |1048576 |The size of the batch data sent by Kafka producers, in bytes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The recommended setting is 1048576, which is 1MB.</div><br> |
|kafka.producer.linger.ms |No |100 |The waiting time for Kafka producer before sending messages in batches, in milliseconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to set it to 100.</div><br> |
|Kafka.producer .compression.type |No |LZ4 |It is recommended to set the compression method of messages sent by Kafka producers to lz4. |


<span id="b904b9c8"></span>
## Configuration example

The following configuration indicates that Flume uploads data from `/var/log/test1/example.log`log file to TLS.

```Properties
a1.sources = r1
a1.sinks = k1
a1.channels = c1

a1.sources.r1.type = TAILDIR
a1.sources.r1.channels = c1
a1.sources.r1.filegroups = f1
a1.sources.r1.filegroups.f1 = /var/log/test1/example.log #Replace it with the actual log file.
a1.sinks.k1.type = org.apache.flume.sink.kafka.KafkaSink
a1.sinks.k1.kafka.bootstrap.servers = tls-cn-beijing.ibytepluses.com:9094
a1.sinks.k1.channel = c1
a1.sinks.k1.kafka.topic = 5f93fcxxxxfec8a5
a1.sinks.k1.kafka.producer.acks = 1
a1.sinks.k1.kafka.producer.batch.size = 1048576
a1.sinks.k1.kafka.producer.linger.ms = 100
a1.sinks.k1.kafka.producer.compression.type = lz4
a1.sinks.k1.kafka.producer.security.protocol = SASL_SSL
a1.sinks.k1.kafka.producer.sasl.mechanism = PLAIN
a1.sinks.k1.kafka.producer.sasl.jaas.config = org.apache.kafka.common.security.plain.PlainLoginModule required username="20fxxxx8ad7af" password="AKxxxx#T0RNME5EUTFZVxxxx";

a1.channels.c1.type = memory
```
