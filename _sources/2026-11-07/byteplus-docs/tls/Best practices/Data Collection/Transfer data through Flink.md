---
title: "Transfer data through Flink"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Transfer-data-through-flink"
---

Torch Log Service is fully integrated with the Flink ecosystem. It not only supports receiving logs written by the Flink connector, but also supports consuming logs into downstream big data components through the flink\-connector\-kafka.

<span id="b226ce9f"></span>
## Background information

Apache Flink is a distributed processing engine and framework for stateful computation on both bounded and unbounded data streams. It has a rich ecosystem of connectors, such as the Flink connector and the [Apache Kafka ](https://kafka.apache.org/)connector (the flink\-connector\-kafka plugin).

TLS is fully integrated with the Flink ecosystem. It supports easily accessing all kinds of logs from different sources via the Flink connector, enabling operations such as real\-time collection, in\-depth analysis and structured processing of logs. It also supports seamlessly connecting with big data processing and analysis platforms through the flink\-connector\-kafka plugin and consuming the processed logs into downstream big data components or data warehouses.

<span id="6567e050"></span>
## prerequisite


* The log project and log topic have been created. For detailed operation steps, please refer to [Create resources](https://docs.byteplus.com/docs/tls/getting_started_creating_resources).

* The Kafka protocol consumption function has been enabled for the specified log topic, and the Kafka protocol consumption topic ID has been obtained. For detailed instructions, please refer to [Use the Kafka protocol to consume logs](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs).

* It is recommended to use IAM users for access authentication. Before using IAM users, it is necessary to confirm that the BytePlus account has created IAM users and has granted them consumption\-related permissions. For detailed instructions, please refer to [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions).

* Get the AccessKey pair of the current login account. For more information, refer to [Creating an AccessKey pair](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).


<span id="d0e6694c"></span>
## Step 1: Write the logs through the Flink connector

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only Flink at least once semantics is supported. When a task fails, the data written into TLS may be duplicated, but it will not be lost.</div>


<span id="aee9f75e"></span>
### Operation steps


1. Initialize FlinkLogSInk.

   1. Set the production parameters.

      In general, you can use the default values. If necessary, you can customize the configuration. For configuration examples, please refer to [Transfer data through Flink](https://docs.byteplus.com/docs/tls/36893).

      
      |Configuration item |Required |Default value |Description |
      |---|---|---|---|
      |endpint |Yes |/ |The endpoint of TLS. For example: tls\-cn\-beijing.bytepluses.com. Please choose the correct service entry according to the region and network type. For detailed information, please refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">There is no need to specify the service address at <code>https://</code>.</div><br> |
      |region |Yes |/ |The region where the project is located, for example: cn\-beijing. |
      |accessKey |Yes |/ |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted.<br><br>It is recommended to use IAM users for authentication and configure their Access Key ID in the environment variables. |
      |AccessSecret |Yes |/ |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted.<br><br>It is recommended to use IAM users for authentication and configure their Access Key secret in the environment variables. |
      |totalSizeInBytes |No |104857600 |The maximum available cache memory size for sending logs in TLS. |
      |maxThreadCount |No |50 |The maximum available number of threads for TLS to send logs. |
      |maxBatchSizeBytes |No |524288 |The size of logs sent in a single request, with a maximum not exceeding 10MB. |
      |maxBatchCount |No |4096 |The number of logs sent in a single request, with a maximum not exceeding 40,960. |
      |lingerMs |No |2000 |The maximum waiting time for a single request, unit: milliseconds. |
      |maxBlockMs |No |60000L |The maximum waiting time for applying available memory, unit: milliseconds. |
      |retryCount |No |2 |The number of retries allowed in case of sending failure, with a maximum not exceeding 4 times. |
      |maxReservedAttempts |No |3 |The number of request records that can be retained, with a maximum not exceeding 5. |
      |multiAccountEnable |No |false |Whether to enable writing data across accounts.<br><br>After enabling writing data across accounts, authentication can be completed through the authorized roles. |
      |roleName |No |/ |The name of the role authorized by the target account. It is required when `multiAccountEnable=true`. |
      |failStrategy |No |log_pass |Failure strategy. Optional values:<br><br><br>* fall_through: The task fails directly.<br><br>* log_pass: Print the logs.<br><br>* write_to_topic: Send the logs to the topic. At this time, it is necessary to ensure that the provided Access Key ID and Secret Access Key have the log writing permission for this topic. If it fails again, an error log will be printed. When `multiAccountEnable=true`, `failStrategy` can be set to `write_to_topic`. |
      

   2. Overload the LogSerializationFunction function to serialize data into a FlinkLogGroup.

      ```Java
      /** SimpleStringFunction. */
      public static class SimpleStringFunction implements LogSerializationFunction<String> {
      
          private final String topic;
      
          public SimpleStringFunction(String topic) {
              this.topic = topic;
          }
      
          @Override
          public FlinkLogGroup serialize(String element) {
              FlinkLogGroup group = new FlinkLogGroup();
              group.setTopic(topic);
              LogItem log = new LogItem();
              log.setTime(System.currentTimeMillis());
              log.addContent("content", element);
              group.getLogs().add(log);
              return group;
          }
      }
      ```
      

2. Simulate data writing to TLS.

   ```Java
   /** Simulate producing messages. */
   public static class RandomStringSource implements ParallelSourceFunction<String> {
       private volatile boolean running = true;
   
       @Override
       public void run(SourceContext<String> ctx) throws Exception {
           long seq = 0;
           while (running) {
               Thread.sleep(10);
               ctx.collect((seq++) + "-" getLongString(30));
           }
       }
   
       @Override
       public void cancel() {
           running = false;
       }
   
       public static String getLongString(int length) {
           String str = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
           Random random = new Random();
           StringBuffer sb = new StringBuffer();
           for (int i = 0; i < length; i++) {
               int number = random.nextInt(62);
               sb.append(str.charAt(number));
           }
           return sb.toString();
       }
   }
   ```
   


<span id="fdeaf708"></span>
### Configuration examples

You can refer to the following example to complete log writing.

```SQL
package org.apache.flink.connectors.tls;

import org.apache.flink.api.java.utils.ParameterTool;
import org.apache.flink.connectors.tls.config.LogConstants;
import org.apache.flink.connectors.tls.entry.FlinkLogGroup;
import org.apache.flink.connectors.tls.entry.LogSerializationFunction;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.streaming.api.functions.source.ParallelSourceFunction;

import com.volcengine.model.tls.LogItem;

import java.util.Random;

/** TLS sink sample. */
public class FlinkLogSinkSample {

    private static final String DEFAULT_TLS_ENDPOINT = "http://tls-cn-guilin-boe.bytepluses.com";
    private static final String DEFAULT_REGION = "cn-guilin-boe";
    private static final String ACCESS_KEY_ID = "";
    private static final String ACCESS_KEY_SECRET = "";

    public static void main(String[] args) throws Exception {
        final ParameterTool params = ParameterTool.fromArgs(args);
        final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
        env.getConfig().setGlobalJobParameters(params);
        env.setParallelism(3);
        env.enableCheckpointing(5000);
        DataStream<String> stream = env.addSource(new RandomStringSource());

        // When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks.
        // If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty.
        // The FlinkLogSink has default values configured during initialization, which can be adjusted according to the actual situation.
        FlinkLogSink<String> flinkLogSink =
                new FlinkLogSink.Builder<String>(
                                params.get(LogConstants.LOG_ENDPOINT, DEFAULT_TLS_ENDPOINT),
                                params.get(LogConstants.LOG_REGION, DEFAULT_REGION),
                                params.get(LogConstants.LOG_ACCESS_KEY, ACCESS_KEY_ID),
                                params.get(LogConstants.LOG_ACCESS_SECRET, ACCESS_KEY_SECRET))
                        .setSerializationFunction(new SimpleStringFunction(params.get("TOPIC")))
                        .build();
        stream.addSink(flinkLogSink);
        env.execute("flink log producer");
    }

    /** Simulate generating messages. */
    public static class RandomStringSource implements ParallelSourceFunction<String> {
        private volatile boolean running = true;

        @Override
        public void run(SourceContext<String> ctx) throws Exception {
            long seq = 0;
            while (running) {
                Thread.sleep(10);
                ctx.collect((seq++) + "-" getLongString(30));
            }
        }

        @Override
        public void cancel() {
            running = false;
        }

        public static String getLongString(int length) {
            String str = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
            Random random = new Random();
            StringBuffer sb = new StringBuffer();
            for (int i = 0; i < length; i++) {
                int number = random.nextInt(62);
                sb.append(str.charAt(number));
            }
            return sb.toString();
        }
    }

    /** SimpleStringFunction. */
    public static class SimpleStringFunction implements LogSerializationFunction<String> {

        private final String topic;

        public SimpleStringFunction(String topic) {
            this.topic = topic;
        }

        @Override
        public FlinkLogGroup serialize(String element) {
            FlinkLogGroup group = new FlinkLogGroup();
            group.setTopic(topic);
            LogItem log = new LogItem();
            log.setTime(System.currentTimeMillis());
            log.addContent("content", element);
            group.getLogs().add(log);
            return group;
        }
    }
}
```


<span id="d5edfa5f"></span>
## Step 2: Consume logs through flink\-connector\-kafka

When consuming the log data of TLS through Flink, it is necessary to use flink\-connector\-kafka provided by Flink as the Connector.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Apache Flink has multiple Kafka clients built\-in, and the version of the client used may change among different Flink distributions. Currently, TLS only supports connections from Kafka clients with versions 0.11.x and above. The corresponding Flink version should be 1.7.x and above. If Flink with a version below 1.7.x is used, it is necessary to manually specify the version of the Kafka client to be 0.11.x and above.</div>


<span id="382fe899"></span>
### 1 Add Maven dependencies

Add the Maven dependencies related to flink\-connector\-kafka in the project. The detailed information of the dependencies is as follows:

```xml
<dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-connector-kafka</artifactId>
        <version>1.16.0</version>
</dependency>
```


<span id="8cb90dd9"></span>
### 2 Configure the Kafka source for Flink

The Kafka Source provides builder classes to create instances of KafkaSource. For its usage methods and implementation details, please refer to [Flink](https://nightlies.apache.org/flink/flink-docs-release-1.16/docs/connectors/datastream/kafka/#usage).

When building KafkaSource, you must specify the underlying properties through the following methods.


|Method |Description |
|---|---|
|setBootstrapServers() |Set the Bootstrap server to the initial cluster connection URL, in the format of `Endpoint:Port number`, such as `tls-ap-southeast-1.ibytepluses.com:9093`.<br><br><br>* The endpoint is the endpoint of TLS in the current region. Select the correct endpoint based on the region and network type. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br>* The port number is fixed to 9093. |
|setTopics() |Specify the Kafka topic to subscribe to. Specify the TLS topic ID for consumption using the Kafka protocol, in the format of `out-${log topic ID}`, such as `out-0fdaa6b6-3c9f-424c-8664-fc0d222c****`. On the topic details page in the TLS console, you can view and copy **Kafka protocol consumer topic ID**. |
|setGroupId() |Specify the consumer group ID. |
|setValueOnlyDeserializer() |Set a deserializer for parsing Kafka messages. |
|setProperty() |Configure security and authentication settings as follows:<br><br><br>* Set `CommonClientConfigs.SECURITY_PROTOCOL_CONFIG` to `SASL_SSL`.<br><br>* Set `SaslConfigs.SASL_MECHANISM` to `PLAIN`.<br><br>* In `SaslConfigs.SASL_JAAS_CONFIG`, configure the authentication information of the current login user.<br><br>   * username: Specify the Kafka Simple Authentication and Security Layer (SASL) username. Set it to the TLS project ID.<br><br>   * password: Specify the Kafka SASL user password. Set it to the AccessKey pair of your BytePlus account, in the format of `${access-key-id}#${access-key-secret}`, where:<br><br>      * `${access-key-id}`: Replace it with your AccessKey ID.<br><br>      * `${access-key-secret}`: Replace it with your AccessKey secret.<br><br>         For more information on the configurations, refer to the sample code below. |


The following code snippet shows how to build KafkaSource to consume log data in a log topic `0fdaa6b6-3c9f-424c-8664-fc0d222c****`.

```java
final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();

// Consuming data from TLS kafka
KafkaSource<String> tlsKafkaSource = KafkaSource.<String>builder()
        //Specify the initial cluster connection URL, in the format of Endpoint:Port number, such as tls-ap-southeast-1.ibytepluses.com:9093, where:
        //The endpoint is the endpoint of TLS in the current Region. Select the correct endpoint based on the Region and network type. For more information, refer to Endpoints.
        //The port number is fixed to 9093.
        .setBootstrapServers(tls-cn-beijing.ibytepluses.com:9093)
        //Specify the topic from which log data is to be consumed, in the format of out-xxxxxxxxx.
        .setTopics(out-0fdaa6b6-3c9f-424c-8664-fc0d222c****)
        //Configure the consumer group.
        .setGroupId(consumeGroupID)
        .setStartingOffsets(OffsetsInitializer.earliest())
        .setValueOnlyDeserializer(new SimpleStringSchema())
        ///Specify the security mode. Only SASL_SSL is supported in TLS.
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
