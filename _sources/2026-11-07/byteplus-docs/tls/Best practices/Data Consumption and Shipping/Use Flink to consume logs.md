---
title: "Use Flink to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_flink_to_consume_logs"
---

Torch Log Service (TLS) allows you to consume data using the Kafka protocol. You can use the flink\-connector\-kafka plug\-in of Flink to connect to TLS. This allows you to use Flink to write log data collected in TLS to downstream big data components or data warehouses for consumption.

<span id=".5Zy65pmv5qaC6L-w"></span>
## Scenario overview

Apache Flink is a distributed data processing engine and framework for stateful computations over bounded and unbounded data streams. With flink\-connector\-kafka, an [Apache Kafka](https://kafka.apache.org/) connector, Flink can read data from and write data to Kafka topics. In TLS, you can enable the feature of consumption using the Kafka protocol for a specified topic. After enabled, Flink considers the topic as a Kafka topic for consumption. For example, the log data in the topic is written to downstream big data components or data warehouses for consumption, making it suitable for stream computing or big data storage scenarios.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Create a project and a topic. For more information, refer to [Create resources](https://docs.byteplus.com/docs/tls/getting_started_creating_resources).

* Enable the feature of consumption using the Kafka protocol for the specified topic, and get **Kafka protocol consumer topic ID**. For more information, refer to [Use the Kafka protocol to consume logs](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs).

* We recommend that you use an IAM user for authentication. Before using an IAM user, make sure the IAM user is created by the BytePlus account and granted the required consumption permissions. For more information, refer to [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions).

* Get the AccessKey pair of the current login account. For more information, refer to [Creating an AccessKey pair](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Apache Flink has multiple built\-in Kafka clients, and different releases of Flink may use different client versions. TLS currently supports only Kafka clients of version 0.11.x and later, corresponding to Flink version 1.7.x and later. If a Flink version earlier than 1.7.x is used, you must manually set the Kafka client version to 0.11.x or later.

<span id=".6YWN572u5q2l6aqk"></span>
## Procedure

<span id=".XzEt5re75YqgLW1hdmVuLeS-nei1lg=="></span>
### Step 1: Add the Maven dependency

To use Flink to consume log data from BytePlus TLS, use flink\-connector\-kafka offered by Flink as the connector.

Add the following Maven dependency to your project:

```xml
<dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-connector-kafka</artifactId>
        <version>1.16.0</version>
</dependency>
```


<span id=".XzIt5Li6LWZsaW5rLemFjee9ri1rYWZrYS1zb3VyY2U="></span>
### Step 2: Configure a Kafka source for Flink

The Kafka Source provides builder classes to create instances of KafkaSource. For its usage methods and implementation details, please refer to [Flink](https://nightlies.apache.org/flink/flink-docs-release-1.16/docs/connectors/datastream/kafka/#usage).

When building KafkaSource, you must specify the underlying properties through the following methods.


|Method |Description |
|---|---|
|setBootstrapServers() |Set the Bootstrap server to the initial cluster connection URL, in the format of `Endpoint:Port number`, such as `tls-ap-southeast-1.ibytepluses.com:9093`.<br><br><br>* The endpoint is the endpoint of TLS in the current Region. Select the correct endpoint based on the region and network type. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br>* The port number is fixed to 9093. |
|setTopics() |Specify the Kafka topic to subscribe to. Specify the TLS topic ID for consumption using the Kafka protocol, in the format of `out-${log topic ID}`, such as `out-0fdaa6b6-3c9f-424c-8664-fc0d222c****`. On the topic details page in the TLS console, you can view and copy **Kafka protocol consumer topic ID**. |
|setGroupId() |Specify the consumer group ID. |
|setValueOnlyDeserializer() |Set a deserializer for parsing Kafka messages. |
|setProperty() |Configure security and authentication settings as follows:<br><br><br>* Set `CommonClientConfigs.SECURITY_PROTOCOL_CONFIG` to `SASL_SSL`.<br><br>* Set `SaslConfigs.SASL_MECHANISM` to `PLAIN`.<br><br>* In `SaslConfigs.SASL_JAAS_CONFIG`, configure the authentication information of the current login user.<br><br>   * username: Specify the Kafka Simple Authentication and Security Layer (SASL) username. Set it to the TLS project ID.<br><br>   * password: Specify the Kafka SASL user password. Set it to the AccessKey pair of your BytePlus account, in the format of `${access-key-id}#${access-key-secret}`, where:<br><br>      * `${access-key-id}`: Replace it with your AccessKey ID.<br><br>      * `${access-key-secret}`: Replace it with your AccessKey secret.<br><br>         For more information on the configurations, refer to the sample code below. |


The following code snippet demonstrates how to build a KafkaSource to consume log data from the topic `0fdaa6b6-3c9f-424c-8664-fc0d222c****`.

```java
final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();

// Consuming data from TLS kafka
KafkaSource<String> tlsKafkaSource = KafkaSource.<String>builder()
        //Specify the initial cluster connection URL, in the format of Endpoint:Port number, such as tls-ap-southeast-1.ibytepluses.com:9093, where:
        //The endpoint is the endpoint of TLS in the current Region. Select the correct endpoint based on the Region and network type. For more information, refer to Endpoints.
        //The port number is fixed to 9093.
        .setBootstrapServers(tls-ap-southeast-1.ibytepluses.com:9093)
        //Specify the topic from which log data is to be consumed, in the format of out-xxxxxxxxx.
        .setTopics(out-0fdaa6b6-3c9f-424c-8664-fc0d222c****)
        //Configure the consumer group.
        .setGroupId(consumeGroupID)
        .setStartingOffsets(OffsetsInitializer.earliest())
        .setValueOnlyDeserializer(new SimpleStringSchema())
        //Specify the security mode. Only SASL_SSL is supported in TLS.
        .setProperty(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_SSL")
        //Specify the authentication mode. Only PLAIN is supported in TLS.
        .setProperty(SaslConfigs.SASL_MECHANISM, "PLAIN")
        //Set the username and password:
        //username: Set it to the TLS project ID.
        //password: Set it to the AccessKey pair of your BytePlus account, in the format of ${access-key-id}#${access-key-secret}, where:
        //${access-key-id}: Replace it with your AccessKey ID.
        //${access-key-secret}: Replace it with your AccessKey secret.
        .setProperty(SaslConfigs.SASL_JAAS_CONFIG,
                "org.apache.kafka.common.security.plain.PlainLoginModule " +
                        "required username=\"" + bd4d5b20-479a-4f33-9099-a44db3be**** + "\" password=\"" + AK****NWE2MTI#WldWa1p****dZd05JKJKHHUI== + "\";")
        .build();
DataStreamSource<String> data = env.fromSource(tlsKafkaSource, WatermarkStrategy.noWatermarks(), "Kafka Source");

// Customize the sink as needed. You have to implement your own sink.
Sink<String> customizedSink = CreateSink();
data.sinkTo(customizedSink);

env.execute("Flink Tls Kafka Job");
```
