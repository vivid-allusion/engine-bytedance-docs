---
title: "Use Spark Streaming to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_spark_streaming_to_consume_logs"
---

Torch Log Service (TLS) allows you to consume data using the Kafka protocol. You can use the spark\-streaming\-kafka component of Spark Streaming to connect to TLS. This allows you to use Spark Streaming to write log data collected in TLS to downstream big data components or data warehouses for consumption.

## Scenario overview

Spark Streaming is a real\-time computing framework built on top of Spark, offering scalable, high\-throughput, and fault\-tolerant stream processing capabilities. It allows you to integrate data from various data sources. For example, you can use spark\-streaming\-kafka to integrate data from Kafka and consume Kafka messages. In TLS, you can enable the feature of consumption using the Kafka protocol for a specified topic. After enabled, Spark Streaming considers the topic as a Kafka topic for consumption. For example, the log data in the topic is written to downstream big data components or data warehouses for consumption, making it suitable for stream computing or big data storage scenarios.

## Before you begin

* Create a project and a topic. For more information, refer to [Create resources](https://docs.byteplus.com/docs/tls/getting_started_creating_resources)

* Enable the feature of consumption using the Kafka protocol for the specified topic, and get **Kafka protocol consumer topic ID**. For more information, refer to [Use the Kafka protocol to consume logs](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs).

* We recommend that you use an IAM user for authentication. Before using an IAM user, make sure the IAM user is created by the BytePlus account and granted the required consumption permissions. For more information, refer to [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions).

* Get the AccessKey pair of the current login account. For more information, refer to [Creating an AccessKey pair](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).

## Procedure

### Step 1: Add the Maven dependency

To use Spark Streaming to consume log data from BytePlus TLS, use spark\-streaming\-kafka\-0\-10 offered by Spark Streaming.

Add the following Maven dependency to your project:

> **tip**

> To use Kafka to consume data in TLS, the Kafka protocol version must be 0.11.0 or later. You must manually specify the Kafka client version of Spark as 0.11.0 or later.

```xml
<dependency>
    <groupId>org.apache.spark</groupId>
    <artifactId>spark-streaming-kafka-0-10_2.11</artifactId>
    <version>${spark.version}</version>
    <exclusions>
        <exclusion>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-clients</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <!--The version must be 0.11.0 or later. -->
    <version>1.0.0</version>
</dependency>
```

### Step 2: Configure a Spark input stream

Refer to the following sample code to configure a Spark input stream. For more information on the configurations, refer to [Spark official documentation](https://spark.apache.org/docs/latest/streaming-programming-guide.html). The table below explains the parameters.

The following example demonstrates how to create a Spark input stream to consume log data from the topic `0fdaa6b6-3c9f-424c-8664-fc0d222c****`.

```java
// Create a Spark Streaming context.
SparkConf conf = new SparkConf().setAppName("TlsDemo").setMaster("local").set("spark.serializer", "org.apache.spark.serializer.KryoSerializer");
conf.registerKryoClasses((Class<?>[]) Arrays.asList(ConsumerRecord.class).toArray());

// Spark Streaming jobs collect data received from the data source every 5 seconds.
JavaStreamingContext jssc = new JavaStreamingContext(conf, Durations.seconds(5));

// Create a Kafka parameter map.
// The map is used to store the address of the Kafka cluster, that is, the broker address.
Map<String, Object> kafkaParams = new HashMap<>();
//Specify the initial cluster connection URL, in the format of Endpoint:Port number, such as tls-ap-southeast-1.ibytepluses.com:9093, where:
//The endpoint is the endpoint of TLS in the current Region. Select the correct endpoint based on the Region and network type. For more information, refer to Endpoints.
//The port number is fixed to 9093.
kafkaParams.put("bootstrap.servers", tlsEndConsumePoint);
//Specify the data type and encoding format for Kafka output keys. By default, the string type and UTF-8 encoding are used.
kafkaParams.put("key.deserializer", StringDeserializer.class);
//Specify the data type and encoding format for Kafka output values. By default, the string type and UTF-8 encoding are used.
kafkaParams.put("value.deserializer", StringDeserializer.class);
//Specify a consumer group ID arbitrarily.
kafkaParams.put("group.id", consumeGroupID);
kafkaParams.put("auto.offset.reset", "latest");
kafkaParams.put("enable.auto.commit", false);
//Specify the security mode. Only SASL_SSL is supported in TLS.
kafkaParams.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_SSL");
//Specify the authentication mode. Only PLAIN is supported in TLS.
kafkaParams.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
//Set the username and password:
//Username: Set it to the TLS project ID.
//Password: Set it to the AccessKey pair of your BytePlus account,
// in the format of ${access-key-id}#${access-key-secret}, where:
//${access-key-id}: Replace it with your AccessKey ID.
//${access-key-secret}: Replace it with your AccessKey secret.
kafkaParams.put(SaslConfigs.SASL_JAAS_CONFIG,
        "org.apache.kafka.common.security.plain.PlainLoginModule " +
                "required username=\"" + bd4d5b20-479a-4f33-9099-a44db3be**** + "\" password=\"" + AK****NWE2MTI#WldWa1p****dZd05JKJKHHUI== + "\";");

// Create a topic set.
Collection<String> topics = new HashSet<>();
//Specify the topic from which log data is to be consumed, in the format of out-xxxxxxxxx.
topics.add(out-0fdaa6b6-3c9f-424c-8664-fc0d222c****);

try {
    // Get data from Kafka.
    final JavaInputDStream<ConsumerRecord<String, String>> stream = KafkaUtils.createDirectStream(jssc, LocationStrategies.PreferConsistent(),
            ConsumerStrategies.Subscribe(topics, kafkaParams));
            
    // Write data to downstream big data components for consumption.
    stream.print();
    jssc.start();
    jssc.awaitTermination();
    jssc.close();

} catch (Exception e) {
    e.printStackTrace();
}
```

The required parameters are as follows:

|Parameter |Description |
|---|---|
|bootstrap.servers |Specify the initial cluster connection URL, in the format of `Endpoint:Port number`, such as `tls-ap-southeast-1.ibytepluses.com:9093`.<br><br><br>* The endpoint is the endpoint of TLS in the current Region. Select the correct endpoint based on the Region and network type. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br>* The port number is fixed to 9093. |
|consumeTopic |Specify the Kafka topic to subscribe to. Specify the TLS topic ID for consumption using the Kafka protocol, in the format of **`out-${log topic ID}`** , such as `out-0fdaa6b6-3c9f-424c-8664-fc0d222c****`. On the topic details page in the TLS console, you can view and copy **Kafka protocol consumer topic ID**. |
|SECURITY_PROTOCOL_CONFIG |Set the security mode to SASL_SSL. |
|SASL_MECHANISM |Set the authentication mechanism to PLAIN. |
|SASL_JAAS_CONFIG |Specify the authentication information of the current login user, where:<br><br><br>* username: Specify the Kafka Simple Authentication and Security Layer (SASL) username. Set it to the TLS project ID.<br><br>* password: Specify the Kafka SASL user password. Set it to the AccessKey pair of your BytePlus account, in the format of `${access-key-id}#${access-key-secret}`, where:<br><br>   * `${access-key-id}`: Replace it with your AccessKey ID.<br><br>   * `${access-key-secret}`: Replace it with your AccessKey secret. |
