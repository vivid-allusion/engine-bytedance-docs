---
title: "Kafka/BMQ"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Kafka_BMQ"
---

Kafka connector provides the ability to consume and write data from Kafka Topics or BMQ Topics, supporting their use as source tables and result tables. You can create a source stream to retrieve data from Kafka Topics as job input data; you can also write job output data to Kafka Topics through Kafka result tables.

<span id="60216699"></span>
## Precautions


* Users of Flink SQL should note that connectors for versions **kafka\-0.10** and **kafka\-0.11** are no longer supported. Please use the **kafka** connector to access Kafka 0.10 and 0.11 clusters directly.

   The Kafka clients used in the connectors for Kafka\-0.10 and Kafka\-0.11 have flaws, which may result in the inability to automatically commit Kafka offset information under certain conditions.

* Users developing with the datastream API should note, when reading Kafka messages, do not use **FlinkKafkaConsumer010** and **FlinkKafkaConsumer011** consumers; instead, use **FlinkKafkaConsumer** for development. Likewise, when writing messages to Kafka, do not use **FlinkKafkaProducer010** and **FlinkKafkaProducer011** producers; instead, use **FlinkKafkaProducer** for development.


<span id="fbbf884b"></span>
## DDL Definition

<span id="9b322888"></span>
### Used as a Data Source (Source)

```sql
CREATE TABLE kafka_source (
    name String,
    score INT
 ) WITH (
     'connector' = 'kafka',
     'topic' = 'test_topic_01',
     'properties.bootstrap.servers' = 'localhost:9092',
     'properties.group.id' = 'test_topic_01',
     'format' = 'csv',
     'scan.startup.mode' = 'earliest-offset'
 );
```


<span id="d1485470"></span>
### Used as a data sink

```SQL
CREATE TABLE kafka_sink (
    name String,
    score INT
 ) WITH (
     'connector' = 'kafka',
     'topic' = 'test_topic_01',
     'properties.bootstrap.servers' = 'localhost:9092',
     'format' = 'csv'
 );
```


<span id="38b6f1af"></span>
## WITH parameters


|**Parameter** |**Is it mandatory?**  |**Default value** |**Data type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Designate the connector to use, only the Kafka connector is supported here.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The connectors for Kafka\-0.10 and Kafka\-0.11 use a Kafka client with defects, which may fail to automatically commit Kafka offset information under certain circumstances.</div><br> |
|topic |Yes |(none) |String |Name the specified Kafka topic. |
|properties.bootstrap.servers |Yes |(none) |String |Specify the address of the Kafka Broker in the format `host:port`. |
|properties.group.id |Yes |(none) |String |Specify the ID of the Kafka consumer group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When consuming BMQ messages using the Kafka connector in Flink, a Consumer Group must be created on the BMQ platform in advance.</div><br><br><br><div data-tips="true" data-tips-type="warning">If a Group is not created in advance, the task can run normally, but cannot submit Offset properly.</div><br> |
|properties.batch.size |No |16 |string |The maximum byte size supported for writing in a Batch corresponding to a single Partition, with a default value of 16 KB.<br><br><br>* batch.size = single Producer's message QPS \* message size \* liner.ms/ number of Partitions<br><br>* By increasing the value of batch.size, a Batch can write more data, thus enhancing throughput. However, the batch.size should not be set too high to avoid the situation where a Batch is not filled in time, leading to high message sending delays.<br><br>* Generally used in conjunction with **properties.linger.ms** and **properties.buffer.memory**, messages will be sent immediately if any of these conditions are met.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you experience insufficient throughput when writing data to Kafka, it is recommended that you increase the batch.size value, typically set to 128KB.</div><br> |
|properties.linger.ms |No |0 |string |The time a message stays in the batch, i.e., the waiting time before sending the message. Default is 0 milliseconds, meaning "send messages immediately."<br><br><br>* By appropriately increasing the linger.ms value, a small delay can be introduced at the cost of improving throughput and compression ratio.<br><br>* This parameter is usually used in conjunction with **properties.batch.size** and **properties.buffer.memory**, and messages are sent immediately if any of these conditions are met.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you experience insufficient throughput when writing data to Kafka, it is recommended to increase the linger.ms value, generally set to 100ms.</div><br> |
|properties.buffer.memory |No |32M |string |The total available memory space for caching messages; if the memory is depleted, the messages in the cache will be sent immediately.<br><br><br>* When setting this, it is advisable to use the calculation formula: buffer.memory\>=batch.size \* number of partitions \* 2.<br><br>* This parameter is generally used in conjunction with **properties.batch.size** and **properties.linger.ms**, and messages will be sent immediately if any of the conditions are met.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the buffer.memory is too small, it may cause batch failure, leading to increased QPS and downstream rate limiting issues.</div><br> |
|properties.enable.idempotence |No |true |Boolean |Whether to enable idempotence for the Kafka connector. Default is true, indicating that idempotence is enabled.<br><br>Once idempotence is enabled, the system's response to message duplicates caused by client retries is the same as handling a single request, ensuring the order and integrity of messages.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you connect BMQ resources through the Kafka connector and use the Flink 1.16\-byted engine, you must set the <code>properties.enable.idempotence</code> parameter to <strong>false</strong> to disable idempotence; otherwise, the task will fail.</div><br> |
|scan.topic\-partition\-discovery.interval |No |none |Duration |In scenarios involving dynamic scaling in Kafka/BMQ, the recommended interval for periodically scanning and discovering new Topics and Partitions is set at 120s.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The default value is none, which means it is not enabled. <strong>It is recommended</strong> that you add this parameter configuration to your task to set the interval for dynamic detection.</div><br><br><br><div data-tips="true" data-tips-type="warning">If this parameter is not configured in the task, dynamic discovery of partitions will not occur. At this time, if a new partition is added, it will not be able to read data from the new partition.</div><br> |
|format |Yes |(none) |String |The format used to deserialize the Kafka message body (value). The supported formats include:<br><br><br>* CSV<br><br>* JSON<br><br>* Debezium\-JSON<br><br>* Canal\-JSON<br><br>* Maxwell\-JSON<br><br>* Ogg\-JSON<br><br>* Avro<br><br>* Confluent Avro<br><br>* RAW |
|scan.startup.mode |No |group\-offsets |String |Startup mode when loading data. The values are as follows:<br><br><br>* **Earliest\-offset**: Start reading from the earliest partition in Kafka.<br><br>* **Latest\-offset**: Starts reading from the latest position in Kafka.<br><br>* **Group offsets**: default value, read according to Group<br><br>* **timestamp**: Read from Kafka from a specified point in time. You need to specify the **scan.startup.timestamp\-millis** parameter in the WITH clause.<br><br>* **Specific\-offsets**: Read from the specified partition target offsets in Kafka. You need to specify the **scan.startup.specific\-offsets** parameter in the WITH clause. |
|scan.startup.specific\-offsets |No |(none) |String |In **specific\-offsets** startup mode, specify the startup offset for each partition. For example, `partition:0,offset:42;partition:1,offset:300`. |
|scan.startup.timestamp\-millis |No |(none) |Long |In **timestamp** startup mode, specify the start point timestamp in milliseconds. |
|scan.parallelism |No |(none) |Integer |Separately set the concurrency of Source. If not set, the degree of parallelism will be the default concurrency of the job.<br><br>This parameter is often used in scenarios where Source and downstream operators need to break operator chains, allowing downstream recomputation operators to use higher default concurrency to enhance computing power. At the same time, it keeps the Source concurrency equal to the number of Kafka partitions, ensuring data shuffling is uniform from Source to downstream due to different concurrencies, thus increasing the overall computation rate. |
|sink.partitioner |No |fixed |String |Mapping relationship from Flink partitions to Kafka partitions. The values are as follows:<br><br><br>* Fixed (default): Each Flink partition corresponds to one Kafka partition.<br><br>* Round\-robin: Data in Flink partitions will be distributed to various Kafka partitions in turns.<br><br>* Custom mapping mode: Supports creating a subclass of FlinkKafkaPartitioner to customize the partition mapping pattern. For example, `org.mycompany.MyPartitioner`. |
|sink.parallelism |No |(none) |Integer |Set the parallelism of the Kafka Sink operator independently. By default, parallelism is set to be the same as the operator connected upstream in the framework. |


<span id="4b5f6953"></span>
## Offsets auto\-commit disabled

There are generally two methods used for auto\-committing Kafka offsets.


* **Method 1**: Relies on Flink task checkpoints.

   When Flink task checkpoints are enabled, the Kafka Source submits the current consumption position at the completion of the checkpoint, ensuring the consistency of Flink's checkpoint state with the committed positions on the Kafka broker.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When relying on Flink task Checkpoints to manage Kafka Offsets, a substantial amount of upstream data can likely trigger upstream LAG alerts.   </div>
   

* **Method 2**: Relies on the periodic commit logic of the Kafka consumer.

   When Flink tasks do not have checkpoints enabled, the Kafka Source will rely on the Kafka Consumer's periodic commit logic. You can control the periodic automatic submission of positions by setting the `enable.auto.commit` and `auto.commit.interval.ms` parameters.

   ```SQL
     -- Whether to automatically submit offsets. A value of true indicates automatic submission of offsets; a value of false indicates manual synchronous or asynchronous submission.
     'enable.auto.commit' = 'true',
     -- The interval for automatically submitting Offsets, in ms。
     'auto.commit.interval.ms' = '500',
   ```
   


<span id="54d30b72"></span>
## Security and authentication

If the Kafka cluster requires secure connections or authentication, you need to add security\-related configurations in the WITH parameters through the `properties.` prefix.

**Example 1**: Use SASL_PLAINTEXT security protocol with the SASL mechanism as PLAIN.

```SQL
CREATE TABLE KafkaTable (
  user_id BIGINT,
  item_id BIGINT,
  behavior STRING
) WITH (
  'connector' = 'kafka',
  ...
  -- Configure the security protocol to SASL_PLAINTEXT.
  'properties.security.protocol' = 'SASL_PLAINTEXT',
  -- Configure the SASL mechanism to PLAIN.
  'properties.sasl.mechanism' = 'PLAIN',
  -- Configure JAAS.
  'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.plain.PlainLoginModule required username="yourname" password="yourpassword";'
)
```


**Example 2**: Use SASL_SSL security protocol with the SASL mechanism as SASL_SSL, and configure certificate and key information.

```SQL
CREATE TABLE KafkaTable (
  user_id BIGINT,
  item_id BIGINT,
  behavior STRING
) WITH (
  'connector' = 'kafka',
  ...
  -- Configure the security protocol to SASL_SSL.
  'properties.security.protocol' = 'SASL_SSL',
  -- Configure the path and password of the truststore (CA certificate) provided by the server.
  'properties.ssl.truststore.location' = '/path/to/kafka.client.truststore.jks',
  'properties.ssl.truststore.password' = 'test1234',
  -- If client authentication is required, you need to configure the keystore (private key) path and password.
  'properties.ssl.keystore.location' = '/path/to/kafka.client.keystore.jks',
  'properties.ssl.keystore.password' = 'test1234',
  -- Configure the SASL mechanism to SCRAM-SHA-256. 
  'properties.sasl.mechanism' = 'SCRAM-SHA-256',
  -- Configure JAAS.
  'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.scram.ScramLoginModule required username="yourname" password="yourpassword";',
  -- If the access point is a private domain name, you need to skip the private domain name verification.
  'properties.ssl.endpoint.identification.algorithm' = ''
)
```


<span id="0cfa857f"></span>
## Sample Code


* Source Example

   ```sql
   CREATE TABLE kafka_source (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_status varchar,
        order_update_time timestamp
        )
   WITH (
     'connector' = 'kafka',
     'topic' = 'source',
     'properties.bootstrap.servers' = 'localhost:9092',
     'properties.group.id' = 'group_01',  -- When consuming BMQ messages, you need to create a Group on the BMQ platform in advance, otherwise the Offset cannot be submitted normally.
     'scan.startup.mode' = 'earliest-offset',
     'format' = 'json'
   );
   CREATE TABLE print_sink (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_status varchar,
        order_update_time timestamp
       )
   WITH (
        'connector' = 'print'           
   );
   insert into print_sink
   select * from kafka_source;
   ```
   

* Result Example

   ```SQL
   CREATE TABLE datagen_source (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_status varchar,
        order_update_time as localtimestamp
       )
   WITH (
        'connector' = 'datagen',
        'rows-per-second' = '5'          
   );
   
   CREATE TABLE kafka_sink (
        order_id bigint,
        order_product_id bigint,
        order_customer_id bigint,
        order_status varchar,
        order_update_time timestamp
        )
   WITH (
     'connector' = 'kafka',
     'topic' = 'sink',
     'properties.bootstrap.servers' = 'localhost:9092',
     'properties.group.id' = 'group_01',
     'format' = 'json'
   );
   
   insert into kafka_sink
   select * from datagen_source;
   ```
   


<span id="cab43f94"></span>
## FAQ

<span id="7ed7d7f7"></span>
### State Loss Restart

If the job's topology has been modified, adding some operators, it cannot be restored from historical state. In this case, you can discard the state and start from the timestamp or group\-offsets mode:


* Recover from timestamp


Suitable for previous jobs that have not initiated a checkpoint. You need to find the current consumption delay in the data curve\-business delay monitoring, reverse\-infer the current consumption time point, and recover from this time point.

For instance, if the business delay is 1h and the current time is 12 o'clock, the inferred consumption time point is 11 o'clock. To avoid data loss, you can consume a bit earlier depending on the situation, such as 30 minutes earlier, setting the recovery time at 10:30.

Parameters are as follows:

> 'properties.scan.startup.mode' = 'timestamp',

> 'properties.scan.startup.timestamp\-millis' = 'xxxx' \-\- Millisecond timestamp, which can be obtained from https://tool.chinaz.com/tools/unixtime.aspx


* Recover from group offsets


Suitable for previous jobs that have initiated and completed a checkpoint. During a checkpoint, the kafka source submits an offset to the kafka instance, therefore the offset is saved in the kafka instance.

At this time, you need to change the startup mode in the kafka source to 'group\-offsets', with the following parameters:

> 'properties.scan.startup.mode' = 'group\-offsets'


Be aware, if this consumer group has no prior offset information, it will error out when starting up for the first time as it cannot fetch partition offset information. In this case, set the following Kafka parameter:

> 'properties.auto.offset.reset' = 'earliest'


This parameter means that if there are no group\-offsets, consumption will start from the oldest position.
