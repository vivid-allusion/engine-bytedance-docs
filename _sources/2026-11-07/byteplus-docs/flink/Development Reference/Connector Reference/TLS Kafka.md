---
title: "TLS Kafka"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/TLS_Kafka"
---

TLS Log Service offers Kafka protocol consumption capabilities that allow a log topic to be consumed as a Kafka Topic, with each log corresponding to a Kafka message. You can use the Flink Kafka connector to link to the Log Service, consuming the collected log data via Flink tasks to downstream big data components or a Data Warehouse.

<span id="8e9fca8c"></span>
## Prerequisites


1. BytePlus Flink and TLS Log Services are already activated through the console.

2. Using Kafka protocol to consume logs requires that the TLS console has [activated Kafka protocol consumption](https://docs.byteplus.com/en/docs/tls/use_the_kafka_protocol_to_consume_logs) feature. It is also necessary to ensure that TLS and Flink belong to the same Region and are connected via a private network.

3. The current version of Flink is recommended to use Flink\-1.16\-byted or higher.


<span id="9c891f14"></span>
## DDL Definition

<span id="7293c57a"></span>
### Used as a data source (Source)

```sql
CREATE TABLE kafka_source (
   user_id BIGINT,
   item_id BIGINT,
   behavior STRING
) WITH (
     'connector' = 'kafka',
     -- The consumption topic needs to be prefixed with out-
     'topic' = 'out-${TLS_TOPIC_ID}',
     -- Refer to the TLS documentation site to access via private domain name, port 9093
     'properties.bootstrap.servers' = 'tls-cn-beijing.byteplus.com:9093',
     -- Configure the security protocol to SASL_SSL and the authentication mechanism to PLAIN
     'properties.security.protocol' = 'SASL_SSL',
     'properties.sasl.mechanism' = 'PLAIN',
     -- Configure JAAS. Fill in the TLS project ID and AK and SK contents for the username and password respectively.
     'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.plain.PlainLoginModule required username="${TLS_PROJECT_ID}" password="${ACCESS_KEY}#${SECRET_KEY}";',
     -- Specify the consumer group, consumption mode and parsing format.
     'properties.group.id' = 'test_topic_01',
     'scan.startup.mode' = 'latest-offset',
     'format' = 'json'
 );
```


<span id="1b2cb7f1"></span>
### Used as a data sink (Sink)

```SQL
CREATE TABLE kafka_sink (
   user_id BIGINT,
   item_id BIGINT,
   behavior STRING
 ) WITH (
   'connector' = 'kafka',
   -- Select the corresponding private network domain name 9094 port according to the specific region.
   'properties.bootstrap.servers' = 'tls-cn-beijing.byteplus.com:9094',
   -- Turn off idempotency.
   'properties.enable.idempotence' = 'false',   
   -- Configure the security protocol to SASL_SSL and the mechanism to PLAIN.
   'properties.security.protocol' = 'SASL_SSL',
   'properties.sasl.mechanism' = 'PLAIN',
   -- Configure JAAS. Enter the project id AK and SK for username and password respectively.
   'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.plain.PlainLoginModule required username="${TLS_PROJECT_ID}" password="${ACCESS_KEY}#${SECRET_KEY}";',
   -- Note that the topic is the TLS Topic ID when writing.
   'topic' = '${TLS_TOPIC_ID}',
   'format' = 'json'
 );
```


<span id="a21cd36e"></span>
## WITH parameters

<span id="ef0b5e47"></span>
### General and consumer parameters


|**Parameter** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specify the connector to use, TLS currently supports Kafka Connector for uploading and consuming data.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The Kafka clients used by the Kafka\-0.10 and Kafka\-0.11 version connectors have defects, which may fail to automatically commit Kafka offset information in some cases.</div><br> |
|topic |Is |(none) |String |Specify the TLS log Topic ID. Note:<br><br><br>1. When consuming, you need to use the format `'topic' = 'out-${TLS_TOPIC_ID}'`, and add the prefix `out-` before the Topic ID.<br><br>2. When writing, use the format `'topic' = '${TLS_TOPIC_ID}'` and do not add the `out-` prefix |
|properties.bootstrap.servers |is |(none) |String |Specify the TLS access address, refer to [TLS service address](https://docs.byteplus.com/en/docs/tls/endpoint). Note:<br><br><br>1. Producer: Usually the 9094 port service<br><br>2. Consumer: Requires the console to enable Kafka protocol consumption, usually the 9093 port service |
|properties.group.id |Yes |(none) |String |Specify the ID of the TLS Consumer Group. |
|format |Yes |(none) |String |The format used to deserialize the TLS return message body (value). Common log formats are as follows:<br><br><br>* JSON<br><br>* CSV<br><br>* RAW |
|scan.startup.mode |No |group\-offsets |String |Startup mode when reading data. Values are as follows:<br><br><br>* **Latest\-offset**: Read from the earliest partition of Kafka.<br><br>* **Latest\-offset**: Starts reading from the latest Kafka offset.<br><br>* **Group\-offsets**: The default setting, reads according to the Group.<br><br>* **Timestamp**: Reads from a specified timestamp in Kafka. The **scan.startup.timestamp\-millis** parameter must be specified in the WITH parameters.<br><br>* **Specific\-offsets**: Reads from a specified partition offset in Kafka. The **scan.startup.specific\-offsets** parameter must be specified in the WITH parameters. |
|scan.startup.specific\-offsets |No |(none) |String |In **specific\-offsets** startup mode, specify the starting offset for each partition. Such as `partition:0,offset:42;partition:1,offset:300`. |
|scan.startup.timestamp\-millis |No |(none) |Long |In **timestamp** startup mode, specify the start timestamp in milliseconds. |
|scan.parallelism |No |(none) |Integer |Set the Source concurrency separately. If not set, the parallelism is the job's default concurrency.<br><br>This parameter is often used in scenarios where the Source and downstream operators need to break the operator chain, allowing operators that recompute downstream to use a larger default concurrency, enhancing computational capacity while maintaining the concurrency of the Source equal to the number of Kafka partitions. In this case, due to different concurrency from Source to downstream, data shuffle is uniform, thus improving the overall computation rate. |


&nbsp;

<span id="9b4f757e"></span>
### Producer parameters

In addition, as producer parameters, TLS Kafka supports the following parameter types:


|**Parameter** |**Required** |**Default value** |**Data type** |**Description** |
|---|---|---|---|---|
|properties.enable.idempotence |No |true |Boolean |If it is writing to a TLS service, idempotence must be disabled. Set to false.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you write to the TLS log service via the Kafka connector, then you must set the <code>properties.enable.idempotence</code> parameter to <strong>false</strong> to disable idempotence, otherwise the task will fail.</div><br> |
|properties.compression.type |No |(none) |string |Used to specify the compression algorithm before messages are sent to Kafka. It is recommended to use the lz4 algorithm. |
|properties.batch.size |No |16 |string |The maximum number of bytes that can be written to a single Partition's Batch, with the default value being 16 KB.<br><br><br>* batch.size=Single Producer's message QPS \* message size \* linger.ms/ number of Partitions<br><br>* Increasing the value of batch.size allows a batch to write more data, which can enhance the throughput. However, the batch.size should not be set too high to avoid the scenario where a Batch is not filled in time, leading to high message sending delays.<br><br>* Typically used in conjunction with **properties.linger.ms** and **properties.buffer.memory**, messages are sent immediately when any of the conditions are met.<br><br><br>**Recommended value**<br><br><br>* When compression is set: 262144<br><br>* When compression is not set: 2621440 |
|properties.linger.ms |No |0 |string |The residence time of messages in the batch, i.e., the waiting time before sending messages. Default is 0 milliseconds, which means "send messages immediately."<br><br><br>* You can appropriately increase the linger.ms value, introducing a slight delay to enhance throughput and compression ratio. Recommended value: 100 ms.<br><br>* This parameter is generally used in conjunction with **properties.batch.size** and **properties.buffer.memory**, sending messages immediately if any condition is met. |
|properties.max.request.size |No |(none) |Integer |Used to specify the maximum size of a single request (which may contain multiple partitions). Unit: Bytes.<br><br>**Recommended value**:<br><br><br>* Compression set: 1046576<br><br>* Compression not set: 10465760 |
|properties.buffer.memory |No |32M |string |Total available memory space for caching messages; if memory runs out, messages in the cache are sent immediately.<br><br><br>* When setting, it is recommended to use the formula: buffer.memory \>= batch.size \* number of partitions \* 2.<br><br>* This parameter is typically used in conjunction with **properties.batch.size** and **properties.linger.ms** parameters, and messages will be sent immediately if any of the conditions are met.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If buffer.memory is small, it might cause Batch failure, leading to problems such as an increase in QPS being throttled by downstream.</div><br> |
|sink.partitioner |No |fixed |String |Mapping relationship between Flink partitions and TLS partitions. The values are as follows:<br><br><br>* fixed (default): Each Flink partition corresponds to one TLS partition.<br><br>* round\-robin: Data in Flink partitions will be distributed in turns to Kafka partitions.<br><br>* Custom mapping mode: Supports creating a subclass of FlinkKafkaPartitioner to customize the partition mapping pattern. For example, `org.mycompany.MyPartitioner`. |
|sink.parallelism |No |(none) |Integer |Set the parallelism of the TLS Sink operator separately. By default, the parallelism is set by the framework to be the same as the operator connected upstream. |


<span id="90b88739"></span>
## SQL example code

<span id="a9bc4a98"></span>
### Source representation example

Here is how to consume TLS as a source table:

```sql
CREATE TABLE tls_source (
   user_id BIGINT,
   item_id BIGINT,
   behavior STRING
) WITH (
   'connector' = 'kafka',
   'topic' = 'out-${TLS_TOPIC_ID}',
   'properties.bootstrap.servers' = 'tls-cn-beijing.byteplus.com:9093',
   'properties.security.protocol' = 'SASL_SSL',
   'properties.sasl.mechanism' = 'PLAIN',
   'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.plain.PlainLoginModule required username="${TLS_PROJECT_ID}" password="${ACCESS_KEY}#${SECRET_KEY}";',
   'properties.group.id' = 'test_topic_01',
   'scan.startup.mode' = 'latest-offset',
   'format' = 'json'
 );

CREATE TABLE print_sink (
   user_id BIGINT,
   item_id BIGINT,
   behavior STRING
) WITH (
   'connector' = 'print'           
);
insert into print_sink
select * from tls_source;
```


<span id="204fd6ef"></span>
### Producer example

Here is an example of TLS acting as a producer:

```SQL
CREATE TABLE datagen_source (
   user_id BIGINT,
   item_id BIGINT,
   behavior STRING
) WITH (
   'connector' = 'datagen',
   'rows-per-second' = '5'          
);

CREATE TABLE tls_sink (
   user_id BIGINT,
   item_id BIGINT,
   behavior STRING
 ) WITH (
   'connector' = 'kafka',
   'properties.bootstrap.servers' = 'tls-cn-beijing.byteplus.com:9094',
   'properties.enable.idempotence' = 'false',   
   'properties.security.protocol' = 'SASL_SSL',
   'properties.sasl.mechanism' = 'PLAIN',
   'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.plain.PlainLoginModule required username="${TLS_PROJECT_ID}" password="${ACCESS_KEY}#${SECRET_KEY}";',
   'topic' = '${TLS_TOPIC_ID}',
   'format' = 'json'
 );

insert into tls_sink
select * from datagen_source;
```


<span id="867eaf5e"></span>
## JAVA example code

POM file dependencies, which support Flink versions 1.11, 1.16, and 1.17, among others.

```XML
<dependency>
    <groupId>org.apache.flink</groupId>
    <artifactId>flink-connector-kafka</artifactId>
    <version>${flink.version}</version>
</dependency>
```


<span id="97b08c35"></span>
### Consumer example

TLS consumer code example:

```Java
package com.example;

import org.apache.flink.api.common.eventtime.WatermarkStrategy;
import org.apache.flink.api.common.serialization.SimpleStringSchema;
import org.apache.flink.connector.kafka.source.KafkaSource;
import org.apache.flink.connector.kafka.source.enumerator.initializer.OffsetsInitializer;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;


public class KafkaConsumerJob {
    public static void main(String[] args) throws Exception {
        // Creating an execution environment
        StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();


        String jaas = "org.apache.kafka.common.security.plain.PlainLoginModule" +
                " required username=\"${TLS_PROJECT_ID}\"" +
                " password=\"${ACCESS_KEY}#${SECRET_KEY}\";";

        // Configuring the Kafka source
        KafkaSource<String> source = KafkaSource.<String>builder()
                // Set consumption
                .setBootstrapServers("tls-cn-beijing.byteplus.com:9093")
                .setTopics("out-${TLS_TOPIC_ID}")
                .setGroupId("flink-consumer-group")
                .setStartingOffsets(OffsetsInitializer.latest())
                .setValueOnlyDeserializer(new SimpleStringSchema())
                .setProperty("security.protocol", "SASL_SSL")
                .setProperty("sasl.mechanism", "PLAIN")
                .setProperty("sasl.jaas.config", jaas)
                .build();

        // Add source and process data
        DataStream<String> stream = env.fromSource(source, WatermarkStrategy.noWatermarks(), "Kafka Source");
        // Add data processing logic
        stream.map(value -> {
            System.out.println("Received message: " + value);
            return value;
        });
        // Execute the task
        env.execute("Kafka Consumer Job");
    }
}
```


<span id="47960875"></span>
### Producer example

TLS write code example:

```Java
package com.example;

import org.apache.flink.api.common.serialization.SimpleStringSchema;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.streaming.api.functions.source.SourceFunction;
import org.apache.flink.connector.kafka.sink.KafkaRecordSerializationSchema;
import org.apache.flink.connector.kafka.sink.KafkaSink;

import java.time.LocalDateTime;
import java.util.Properties;

public class KafkaProducerJob {
    public static void main(String[] args) throws Exception {
        // Creating an execution environment
        StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();

        // Create a data source
        DataStream<String> sourceStream = env.addSource(new CustomDataSource());
        // Please fill in project-id, AK, and SK in the authentication information.
        String jaas = "org.apache.kafka.common.security.plain.PlainLoginModule" +
                " required username=\"${project-id}\"" +
                " password=\"${ACCESS_KEY}#${SECRET_KEY}\";";

        // Configuring the Kafka sink
        KafkaSink<String> sink = KafkaSink.<String>builder()
                // Modify the private network access address based on the specific region
                .setBootstrapServers("tls-cn-beijing.byteplus.com:9094")
                // Note the configuration of topic-id
                .setRecordSerializer(KafkaRecordSerializationSchema.builder()
                        .setTopic("${topic-d}")
                        .setValueSerializationSchema(new SimpleStringSchema())
                        .build()
                )
                // Configure authentication, disable idempotence, and other configurations
                .setProperty("security.protocol", "SASL_SSL")
                .setProperty("enable.idempotence", "false")
                .setProperty("sasl.mechanism", "PLAIN")
                .setProperty("sasl.jaas.config", jaas)
                .build();
        // Writing data to Kafka
        sourceStream.sinkTo(sink);
        // Execute the task
        env.execute("Kafka Producer Job");
    }

    // Custom Data Sources
    public static class CustomDataSource implements SourceFunction<String> {
        private volatile boolean isRunning = true;

        @Override
        public void run(SourceContext<String> ctx) throws Exception {
            while (isRunning) {
                // Simulate json data writing
                String message = "{\"a\": 1, \"b\": 2}";
                ctx.collect(message);
                Thread.sleep(500); // Generate one piece of data per second
            }
        }

        @Override
        public void cancel() {
            isRunning = false;
        }
    }
}
```


<span id="080a3e90"></span>
## FAQ

<span id="59043569"></span>
### State loss restart

If the job's topology is modified and new operators are added, it cannot recover from historical states. In this case, discard the state and start using the timestamp or group\-offsets mode:


* Recover from timestamp


Suitable for previous tasks that did not initiate a checkpoint. You need to find the current consumption delay from the data curve \- business delay monitoring, and deduce the current consumption time point from it. You can then recover from this time point.

For example, if the business delay is 1 hour, and the current time is 12 o'clock, then the deduced consumption time point is 11 o'clock. To avoid data loss, you can consume a bit more in advance depending on the situation, such as advancing 30 minutes, thus setting the recovery time to 10:30.

Parameters are as follows:

> 'properties.scan.startup.mode' = 'timestamp',

> 'properties.scan.startup.timestamp\-millis' = 'xxxx' \-\- millisecond timestamp, can be obtained from https://tool.chinaz.com/tools/unixtime.aspx


* Recover from group offsets


Applicable if the previous job started a checkpoint and completed it. Since during the checkpoint, the kafka source submits the offset to the kafka instance, the offset will be saved to the kafka instance.

At this time, you need to change the startup mode in the Kafka source to group\-offsets, with the following parameters:

> 'properties.scan.startup.mode' = 'group\-offsets'


Note, if this consumer group has no offset information previously, it will throw an error unable to fetch the partition’s offset info when starting for the first time; at this moment, you need to set the following Kafka parameters:

> 'properties.auto.offset.reset' = 'earliest'


This parameter means if there is no group\-offset, consume from the oldest position.

<span id="f437ccf6"></span>
### Automatic Offset Commit Mechanism

Currently, the following two methods are generally used for automatic submission of Kafka Offsets.


* **Method 1**: Rely on Flink job Checkpoints.

   When a Flink job starts Checkpoints, Kafka Source submits the current consumption point upon completing a Checkpoint, ensuring consistency between Flink's Checkpoint status and the submitted point on the Kafka Broker.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When relying on Flink task Checkpoints to manage Kafka Offsets, if the upstream data volume is large, it may trigger an upstream LAG alert.   </div>
   

* **Method 2**: Rely on the timing submission logic of Kafka Consumer's points.

   When Flink tasks do not have Checkpoint enabled, Kafka Source relies on the Kafka Consumer's offset commit logic based on timing. You can control the offset timing auto\-commit by setting `enable.auto.commit` and `auto.commit.interval.ms`.

   ```SQL
     -- Whether to automatically submit offsets. A value of true indicates automatic submission of offsets; a value of false indicates manual synchronous or asynchronous submission.
     'enable.auto.commit' = 'true',
     -- The interval for automatically submitting Offsets, in ms.
     'auto.commit.interval.ms' = '500',
   ```
   


&nbsp;
