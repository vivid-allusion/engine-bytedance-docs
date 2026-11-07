---
title: "Using default endpoint for stress testing"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/using-default-endpoint-for-stress-test"
---

This topic describes how to perform stress testing for Kafka production and consumption using the default endpoint.

<span id="7327b4e3"></span>
## Testing recommendations


* To increase throughput, create topics with at least 3 partitions. Since Kafka instances have a minimum of 3 nodes, having only 1 partition will lead to performance issues as it will be handled by a single broker.

* Since Kafka handles messages in a FIFO queue among multiple partitions, excessive partitions can also affect production performance. It is recommended to limit the number of partitions to no more than 6.

* To ensure effective stress testing, simulate concurrency with multiple clients. It is advisable to use several machines as testing clients (producers), launching multiple testing programs on each machine. Start one producer every second to avoid high load from simultaneous starts.


<span id="d3086070"></span>
## Prerequisites


* A Kafka instance has been created, and endpoint information obtained. For more information, please see [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance).

* A topic has been created. For more information, please see [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic.).

* An ECS instance has been purchased, with JDK installed and environment variables configured. For more information, please see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).


<span id="df91baac"></span>
## Procedure


1. Connect to the ECS instance. For connection methods, please see [Logging on to ECS Instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Download the Kafka 2.2.2 toolkit on the ECS instance.

   ```HTTP
   wget https://archive.apache.org/dist/kafka/2.2.2/kafka_2.11-2.2.2.tgz
   ```
   

3. Extract the Kafka 2.2.2 toolkit.

   ```Bash
   tar -zxvf kafka_2.11-2.2.2.tgz 
   ```
   

4. Navigate to the `./bin` directory of the extracted files.

5. **Stress test for message production**:

   1. Run the following command to perform the stress test for message production.

      ```Bash
      ./kafka-producer-perf-test.sh --topic {Topic name} --num-records 100000 --throughput 20000 --record-size 1000 --producer-props bootstrap.servers={default access piont domain name:port}
      ```
      

      
      |**Parameter** |**Description** |
      |---|---|
      |\-\-topic |Name of the target topic, which must be created in Kafka console beforehand. |
      |\-\-num\-records |Number of messages to send. |
      |\-\-throughput |Throughput per second, i.e., how many messages to send per second.<br><br>Set to \-1 for no limit. |
      |\-\-record\-size |Size of the message in bytes. |
      |\-\-producer\-props |The configuration properties of Kafka producer.<br><br><br>* bootstrap.servers: access points for the Kafka instance, namely the **Default access point** in the **Service access** pane of **Instance details** page in the console. |
      

   2. Check the test results.

      ```JSON
      [root@iv-xxx5uo bin]# ./kafka-producer-perf-test.sh --topic topic-1 --num-records 100000 --throughput 20000 --record-size 1000 --producer-props bootstrap.servers=kafka-xxxc5y.kafka.ap-southeast-1.ibytepluses.com:9092
      99949 records sent, 19981.8 records/sec (19.06 MB/sec), 8.8 ms avg latency, 159.0 ms max latency.
      100000 records sent, 19932.230417 records/sec (19.01 MB/sec), 8.78 ms avg latency, 159.00 ms max latency, 1 ms 50th, 84 ms 95th, 139 ms 99th, 155 ms 99.9th.
      ```
      

      **Analysis**: in this example, 100,000 messages were written, with a total of 19.01MB of data sent to Kafka per second, averaging 19,932.23 messages/second, with an average latency of 13.84 ms and a maximum latency of 159 ms.

6. **Stress test for message consumption**:

   1. Run the following command to start the consumption stress test.

      ```Bash
      ./kafka-consumer-perf-test.sh --topic {Topic name} --fetch-size 1048576 --messages 100000 --group {Group name} --broker-list {default endpoint:port} 
      ```
      

      
      |**Parameter** |**Description** |
      |---|---|
      |\-\-topic |Name of the target topic to subscribe to. |
      |\-\-fetch\-size |Amount of data to fetch per request, default 1048576 bytes. |
      |\-\-messages |Number of messages to consume. |
      |\-\-group |Custom name for the group. There is no need to create it in Kafka console in advance. |
      |\-\-broker\-list |Access points for the Kafka instance, found in the **Service access** pane of instance details page in the console. |
      

   2. Check the test results.

      ```JSON
      [root@iv-xxx5uo bin]# ./kafka-consumer-perf-test.sh --topic topic-1 --fetch-size 1048576 --messages 100000 --group group-1 --broker-list kafka-xxxc5y.kafka.ap-southeast-1.ibytepluses.com:9092
      start.time, end.time, data.consumed.in.MB, MB.sec, data.consumed.in.nMsg, nMsg.sec, rebalance.time.ms, fetch.time.ms, fetch.MB.sec, fetch.nMsg.sec
      2024-08-05 11:29:47:003, 2024-08-05 11:30:00:905, 95.3674, 6.8600, 100000, 7193.2096, 3038, 10864, 8.7783, 9204.7128
      ```
      

      After executing the command, you may receive results similar to the following:

      * Start time (start.time): 2024\-08\-05 11:29:47:003

      * End time (end.time): 2024\-08\-05 11:30:00:905

      * Maximum throughput (data.consumed.in.MB): 95.3674 MB/s

      * Average consumption per second (MB.sec): 6.8600 MB/s

      * Maximum number of messages consumed per second (data.consumed.in.nMsg): 100,000

      * Average number of messages consumed per second (nMsg.sec): 7193.2096
