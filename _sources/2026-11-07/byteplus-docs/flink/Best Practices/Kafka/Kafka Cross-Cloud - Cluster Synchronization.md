---
title: "Kafka Cross-Cloud/Cluster Synchronization"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Kafka_Cross_Cloud_Cluster_Synchronization"
---

<span id="48c96862"></span>
# Scenario Introduction

Kafka cross\-cluster data synchronization refers to the process of syncing data between two or more different Kafka clusters, widely used in disaster recovery and cross\-cloud synchronization scenarios. Its main purpose is to achieve data synchronization and redundancy across multiple data centers, geographic locations, or clusters, enhancing data availability and disaster recovery capabilities.

<span id="843edc18"></span>
# Advantages of BytePlus Flink Cross\-Cluster Data Synchronization

Currently, for cross\-cluster data synchronization, the open\-source Kafka's MirrorMaker tool is generally used. However, MirrorMaker has issues such as complex deployment, monitoring, alerting, high operational costs, and poor scalability.

To resolve the above issues, we have supported Kafka cross\-cluster data synchronization on BytePlus Flink, allowing for cross\-cluster synchronization of multiple topics through simple SQL configuration. Additionally, BytePlus Flink is a fully\-managed one\-stop real\-time computing platform, providing managed Flink services, simple operation, and maintenance\-free, resulting in low usage and operational costs.

We compared MirrorMaker and BytePlus Flink in the scenario of cross\-cluster data synchronization:


|**Feature Points** |**MirrorMaker** |BytePlus **Flink** |
|---|---|---|
|Deployment Cost |Deployment cost is high; building a custom MirrorMaker on the cloud requires ECS\-based setup. |Deployment cost is extremely low; BytePlus Flink provides a fully managed Flink service that is ready to use out of the box. |
|Monitoring |Monitoring is challenging; if you need to monitor MirrorMaker metrics, you’ll have to set up Prometheus + Grafana. This is costly and difficult to maintain. |Based on BytePlus Cloud Monitoring, a fully managed monitoring service is provided, where users can monitor the operational status of Flink jobs through data curves. |
|Alerts |Lacking alerting capabilities, MirrorMaker does not support sending alerts, which leads to delayed notifications to operations personnel when data is delayed, or when MirrorMaker malfunctions or exits. |Based on BytePlus Cloud Monitoring, fully managed alert services are provided. Users can configure alerts for various aspects of jobs, including Kafka business delays, running status, and Checkpoints. |
|Operations maintenance |Operational costs are high. If MirrorMaker fails, it might require a manual restart, incurring certain operational expenses. |Operational costs are low. BytePlus Flink has its own failover mechanism. In the event of abnormal data synchronization, it automatically recovers through the failover mechanism without the need for manual maintenance. |
|Scalability |Scalability is poor. When a single machine's resources cannot meet the needs of cross\-cluster real\-time synchronization, it is necessary to build a multi\-node MirrorMaker cluster based on ECS. The setup process is complicated. Moreover, if there is a need for future expansion, manual addition of new nodes and integration into the existing cluster is required, making it impossible to achieve elastic scalability of resources. |High scalability. BytePlus Flink allows for custom\-defined concurrency levels to quickly enhance data synchronization capacity as data volumes increase, with resource pool scaling and job concurrency modification taking minutes. |
|Usability |Usability is poor, requiring deployment and maintenance based on shell scripts. |High usability. BytePlus Flink provides a visual development interface, making development and maintenance more convenient. |
|Customer Support |As an open\-source product, maintenance must be self\-managed. If issues arise during usage, feedback needs to be provided to the open\-source community, and the repair cycle is lengthy. |BytePlus Flink iterates faster, has quicker bug fixes, and is more stable. |


<span id="cf80ce01"></span>
# Steps for cross\-cluster synchronization with BytePlus Flink

<span id="f99243a7"></span>
## Prerequisites

To ensure network access security, the Kafka resources used in this document must be network\-connected via the internet or dedicated lines.

Before creating cloud resources, you can first create a private network. For related documentation, please refer to [creating a private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). To use Flink tasks to access external networks/cross VPC, please refer to [Flink Accessing the Public Internet](https://docs.byteplus.com/docs/flink/Flink_Accessing_the_Public_Internet).

<span id="a9785167"></span>
## Step One: Develop a Flink SQL Task

Create a new Flink Stream SQL task, select the Flink 1.16\-byted version, and write SQL in the task editing area, as shown in the template below.

The main logic of this SQL is to first define a single Kafka Source that reads all the required topics from the upstream Kafka cluster in raw format, separately reading the original message's key and value, and then define a single Kafka Sink to write the original message's key and value into the corresponding topic of the downstream Kafka cluster. Topic routing is achieved through the metadata fields 'topic' of the Kafka Source and Sink. The Source retrieves the topic metadata, and the Sink, when writing, routes to the specified topic based on this metadata.

**To ensure a one\-to\-one correspondence between upstream and downstream partitions during synchronization, and to maintain the order and correctness of messages, the concurrency must be set to an integer multiple of the maximum number of partitions across all topics. For example, if topic\-1 has 12 partitions and topic\-2 has 24 partitions, set the job concurrency to 24 or a multiple of 24.** 

```SQL
CREATE TABLE kafka_source (
  `topic` STRING METADATA,
  -- Define topic metadata, which is used to provide downstream with corresponding topic writing according to topic name
  `msg_key` VARBINARY,
  -- Define message key, this time use raw format to read raw data, the field type needs to be VARBINARY
  `msg_value` VARBINARY -- Define message value, this time use raw format to read raw data, the field type needs to be VARBINARY
) WITH (
  'connector' = 'kafka',
  'topic' = 'topic1;topic2',
  -- Specify the upstream topic list to be synchronized
  'properties.bootstrap.servers' = 'kafka-xxx-cluster-1.kafka.byteplus.com:9092',
  'properties.group.id' = 'test',
  'key.format' = 'raw',
  -- Use raw format to read the key and value of the original message respectively
  'key.fields' = 'msg_key',
  'value.format' = 'raw',
  'value.fields-include' = 'EXCEPT_KEY',
  'scan.startup.mode' = 'latest-offset'
);


CREATE TABLE kafka_sink (
  `topic` STRING METADATA,
  -- Define topic metadata so that the corresponding topic can be written according to the topic name
  `msg_key` VARBINARY,
  -- Define the message key. This time, the raw format is used to write the original data. The field type needs to be VARBINARY
  `msg_value` VARBINARY -- Define the message value. This time, the raw format is used to write the original data. The field type needs to be VARBINARY
) WITH (
  'connector' = 'kafka',
  'topic' = 'topic1;topic2',
  -- Specify the data to be written Topic list
  'properties.bootstrap.servers' = 'kafka-xxx-cluster-2.kafka.byteplus.com:9092',
  'key.format' = 'raw',
  -- Use raw format to write the key and value of the original message
  'key.fields' = 'msg_key',
  'value.format' = 'raw',
  'value.fields-include' = 'EXCEPT_KEY',
  'properties.enable.idempotence' = 'false',
  -- Turn off transaction writing
  'properties.linger.ms' = '500',
  -- Batch time 500ms, reduce writing pressure
  'properties.batch.size' = '5242880',
  -- Batch size 5MB
  'properties.retries' = '10',
  -- Set the number of retries to 10. Improve stability
  'properties.send.buffer.bytes' = '5242880',
  'properties.max.in.flight.requests.per.connection' = '150',
  'properties.request.timeout.ms' = '120000',
  'properties.buffer.memory' = '67108864',
  'properties.delivery.timeout.ms' = '3000000',
  'sink.partitioner' = 'fixed' -- Use a fixed partitioning strategy to ensure that each Flink concurrently writes to the corresponding Kafka topic partition
);


-- The upstream topic is synchronized to the downstream topic with the same name as before
INSERT INTO
  kafka_sink
SELECT
  topic,
  msg_key,
  msg_value
FROM
  kafka_source;
```


It is important to note that in addition to defining multiple topic lists, Source and Sink also support topicPattern, which uses regular expressions to match the required topics. The parameters are as follows:


|**Parameter** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|topic |Optional |(None) |String |When used as a source, it refers to the topic name for reading data, or the topic name for writing data when used as a sink. It also supports a list of topics separated by semicolons, such as `'topic-1;topic-2'` as the topic list for the source. Note that "topic\-pattern" and "topic" can only specify one of them. For sinks, the topic name is the topic where data is written. It also supports a list of topics for the sink. The provided topic list is considered as a permitted list of valid values for the `topic` metadata column. If a list is provided, for sink tables, the 'topic' metadata column is writable and must be specified. |
|topic\-pattern |Optional |(None) |String |Regular expression for the topic name pattern used for reading or writing. All topic names matching the specified regular expression will be subscribed to by consumers when the job starts running. For sinks, the `topic` metadata column is writable and must be provided, matching the `topic-pattern` regular expression. Note, only one of "topic\-pattern" and "topic" can be specified. |


<span id="7932967b"></span>
## Step Two: Set the mapping relationship of upstream and downstream Topics (as needed)

If it is necessary to adjust the name of the Kafka Topic during cross\-cluster synchronization, one can refer to the following SQL example to adjust the INSERT statements:

```SQL
-- There are mapping rules for upstream and downstream topics, such as mapping upstream topic-1 to downstream prefix-topic-1
-- The places that need to be modified are:
-- 1. Change the Kafka sink topic list to 'topic' = 'prefix-test-1;test-2-suffix;test-3'
-- 2. Use CASE WHEN to define the mapping rules for upstream and downstream topics
INSERT INTO
  Kafka_sink
SELECT
  CASE
  WHEN topic = 'topic-1' THEN 'prefix-topic-1' -- Add a prefix to topic-1, and the topic name written to the downstream cluster is prefix-topic-1
  WHEN topic = 'topic-2' THEN concat('topic-2', '-suffix') -- Add a suffix to topic-2, and the topic name written to the downstream cluster is topic-2-suffix
  ELSE topic END AS topic,
  -- The rest of the topics The name is synchronized to the downstream topic with the same name as before
  msg_key,
  msg_value
FROM
  Kafka_source;
```


<span id="42cf2002"></span>
## Step Three: Launch the Flink SQL job


1. In the task editing area, click the launch button above.

2. In the task launch settings dialog, select the Flink resource pool, set task priority and scheduling strategy, then click confirm.


The system will indicate that the task has been successfully launched, and you can go to the task management page to check.


3. On the task management page, click to start the task.


<span id="01630933"></span>
# Cautions

<span id="5159e5c4"></span>
## Upstream Scale\-out Processing Method

In the scenario of scaling partitions in the upstream topic, you need to first stop the Flink synchronization job, scale the partitions for the corresponding downstream topic, and then, after completion, expand the concurrency of the Flink job to the current maximum partition number of the topic and restart the Flink job from the latest state. After the restart, the Flink job can map the upstream and downstream partitions one\-to\-one.

<span id="e611f625"></span>
## Choose Another Partitioning Strategy

If the current downstream write operation uses a fixed partition strategy and there is no synchronicity requirement in the business such that partitions must correspond one\-to\-one, then the downstream write operation can choose to use the default partitioning strategy. The default partitioning strategy uses [Sticky Partition Strategy (Sticky Partition Strategy)](https://www.confluent.io/blog/apache-kafka-producer-improvements-sticky-partitioner/) for messages without a key and uses the Murmur2 hash algorithm to calculate partitions for messages that contain a key.

If one\-to\-one correlation of the upstream topic partitions is not required and there is skew in the topic partitions, it is recommended to use the default partitioning strategy to ensure uniform distribution of data across downstream topic partitions. The method to set the default partitioning strategy is to remove the 'sink.partitioner' configuration in the Kafka Sink DDL, which will then by default use this strategy.

<span id="a67064a4"></span>
# MirrorMaker Migration to Flink Plan

If you are currently using MirrorMaker for Kafka data traffic synchronization and wish to migrate stably to BytePlus Flink, you can follow these steps:

<span id="3b6b72d0"></span>
## Migration Steps


1. Obtain MirrorMaker configurations, mainly including the connection information for the source and target Kafka clusters, permissible regular expressions for syncing topics, and whether to refresh the topic list, among others.

2. Fill in configurations based on the Flink SQL template: Using the Flink SQL template provided above, enter the MirrorMaker configurations into the corresponding parameters.

> Suggestion: It's recommended to use the same consumer group for MirrorMaker and Flink SQL. And set the Kafka startup mode in Flink SQL to `'scan.startup.mode' = 'group-offset'`. This ensures that Flink SQL continues consuming from the Offset consumed by MirrorMaker.


3. Start the Flink job and monitor the job's performance and the cluster's operational monitoring.


<span id="db47c07e"></span>
## Dual\-Running Solution

When migrating MirrorMaker to BytePlus Flink, a common gray release strategy can be employed. Gray release allows us to divide the migration process into several phases, gradually directing traffic to the new system or new Kafka clusters, minimizing risks and potential impacts.

Initially, switch a small amount of topics to BytePlus Flink for synchronization. Observe for a period, and after confirming stability and performance meet requirements, gradually increase the range of topics in the pilot. Recommended pilot proportions are 5% \-\> 20% \-\> 50% \-\> 100%, gradually increasing the migration ratio.

BytePlus Flink supports adding new topics to the source topic list. When recovering from the latest state, the existing topics in the job recover from historical states, and the added topics start from the SQL configured parameters, such as if 'group\-offset' mode is configured in SQL, then it starts from that mode.

Monitoring Indicators:


* Stability indicators for Flink jobs (failover scenarios, load conditions), performance indicators (QPS, latency).

* Upstream and downstream Kafka cluster indicators (cluster load, QPS, throughput).


<span id="fd847d23"></span>
## Rollback Plan

If issues are discovered during migration, it is crucial to quickly rollback to MirrorMaker. Specific rollback steps:


1. Stop the Flink job.

2. Add the topics needing rollback to the MirrorMaker whitelist, restart MirrorMaker, and begin consuming from the upstream cluster's consumer group's consumption offset.


<span id="cca4f324"></span>
## Cutover Plan

Gradually switch all topic traffic to BytePlus Flink through phased release.

<span id="46e39b39"></span>
# Performance Description

Based on actual performance tests, with a message size of 1KB per message, BytePlus Flink can handle up to 20k QPS and a data rate of 20MB/s per CU. During testing, the job ran stably, with both upstream and downstream Kafka clusters operating smoothly.
