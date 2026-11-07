---
title: "Using SASL_SSL endpoint for stress testing"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/using-SASL-SSL-endpoint-for-stress-test"
---

This topic describes how to perform stress testing for Kafka production and consumption using the SASL_SSL endpoint.

<span id="d825e5ea"></span>
## Testing recommendations


* To increase throughput, create topics with at least 3 partitions. Since Kafka instances have a minimum of 3 nodes, having only 1 partition will lead to performance issues as it will be handled by a single broker.

* Since Kafka handles messages in a FIFO queue among multiple partitions, excessive partitions can also affect production performance. It is recommended to limit the number of partitions to no more than 6.

* To ensure effective stress testing, simulate concurrency with multiple clients. It is advisable to use several machines as testing clients (producers), launching multiple testing programs on each machine. Start one producer every second to avoid high load from simultaneous starts.


<span id="6c38da0d"></span>
## Prerequisites


* A Kafka instance has been created, and endpoint information obtained. For more information, please see [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance).

* A topic has been created. For more information, please see Creating a topic.

* An ECS instance has been purchased, with JDK installed and environment variables configured. For more information, please see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

* To access instances with SASL security mechanisms, SASL users of PLAIN or SCRAM type have been created in advance. For more information, please see [Creating a SASL user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Notice    </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When connecting to Kafka instances using SASL_SSL endpoint, messages are authorized and encrypted by SSL certificate. Regardless of whether you access the instance via public network or private network, the client metadata is connected using an IP address. Since certificates generally do not include this IP, a <code>certificate verify failed</code> error may occur.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To avoid the above issue, it is recommended to uniformly configure the parameter on the client side (taking Java SDK for example, the parameter is: <code>ssl.endpoint.identification.algorithm= </code>). Clients in other programming languages can refer to the official open\-source configuration to skip certificate domain name verification.   </div>
   


<span id="4da77cf9"></span>
## Procedure


1. Connect to the ECS instance. For connection methods, please see [Log in to ECS Instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Download the Kafka 2.2.2 toolkit on the ECS instance.

   ```HTTP
   wget https://archive.apache.org/dist/kafka/2.2.2/kafka_2.11-2.2.2.tgz
   ```
   

3. Extract the Kafka 2.2.2 toolkit.

   ```Bash
   tar -zxvf kafka_2.11-2.2.2.tgz 
   ```
   

4. Configure authentication.

   1. Navigate to the `./config` directory of the extracted files.

   2. Modify the configuration files `consumer.properties` and `producer.properties` according to the following commands to set the SASL user type, username, and password.

      1. for **PLAIN** users

         ```XML
         sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="{PLAIN username}" password="{password}";        
         sasl.mechanism=PLAIN
         security.protocol=SASL_SSL
         ```
         

      2. for **SCRAM** users

         ```XML
         sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required username="{SCRAM username}" password="{password}";        
         sasl.mechanism=SCRAM-SHA-256
         security.protocol=SASL_SSL
         ```
         

5. **Stress test for message production**:

   1. Navigate to the `./bin` directory of the extracted files.

   2. Run the following command to perform the stress test for message production.

      ```Bash
      ./kafka-producer-perf-test.sh --topic {Topic name} --num-records 100000 --record-size 1000 --throughput 20000 --producer-props bootstrap.servers={SASL_SSL access point domain name:port} --producer.config ../config/producer.properties
      ```
      

      
      |**Parameter** |**Description** |
      |---|---|
      |\-\-topic |Name of the target topic, which must be created in Kafka console beforehand. |
      |\-\-num\-records |Number of messages to send. |
      |\-\-record\-size |Size of the message in bytes. |
      |\-\-throughput |Throughput per second, i.e., how many messages to send per second.<br><br>Set to \-1 for no limit. |
      |\-\-producer\-props |The configuration properties of Kafka producer.<br><br><br>* bootstrap.servers: access points for the Kafka instance, namely the<br><br><br>**SASL_SSL access point** in the **Service access** pane of **Instance details** page in the console. |
      |\-\-producer.config |Specify the producer configuration file, e.g., `../config/producer.properties`. |
      

   3. Check the test results.

      ```JSON
      [root@iv-xxx5uo bin]# ./kafka-producer-perf-test.sh --topic topic-1 --num-records 100000 --record-size 1000 --throughput 20000 --producer-props bootstrap.servers=kafka-xxxdgw.kafka.ap-southeast-1.ibytepluses.com:9095 --producer.config ../config/producer.properties
      62737 records sent, 12544.9 records/sec (11.96 MB/sec), 1501.5 ms avg latency, 2430.0 ms max latency.
      100000 records sent, 11490.290704 records/sec (10.96 MB/sec), 1940.06 ms avg latency, 3803.00 ms max latency, 1934 ms 50th, 3651 ms 95th, 3798 ms 99th, 3799 ms 99.9th.
      ```
      

      **Analysis**: in this example, 100,000 messages were written, with a total of 10.96 MB of data sent to Kafka per second, averaging 11,490.290704 messages/second, with an average latency of 1,940.06 ms and a maximum latency of 3,803.00 ms.

6. **Stress test for message consumption**:

   1. Navigate to the `./bin` directory of the extracted files.

   2. Run the following command to start the consumption stress test.

      ```Bash
      ./kafka-consumer-perf-test.sh --topic {Topic name} --fetch-size 1048576 --messages 100000 --group {Group name} --broker-list {SASL_SSL access point domain name:port} --consumer.config ../config/consumer.properties
      ```
      

      
      |**Parameter** |**Description** |
      |---|---|
      |\-\-topic |Name of the target topic to subscribe to. |
      |\-\-fetch\-size |Amount of data to fetch per request, default 1048576 bytes. |
      |\-\-messages |Number of messages to consume. |
      |\-\-group |Custom name for the group. There is no need to create it in Kafka console in advance. |
      |\-\-broker\-list |Access points for the Kafka instance, namely the **SASL_SSL access point** in the **Service access** pane of **Instance details** page in the console. |
      |\-\-consumer.config |Specify the consumer configuration file, e.g., `../config/consumer.properties`. |
      

   3. Check the test results.

      ```JSON
      [root@iv-xxx5uo bin]# ./kafka-consumer-perf-test.sh --topic topic-1 --fetch-size 1048576 --messages 100000 --group group-1 --broker-list kafka-xxxdgw.kafka.ap-southeast-1.ibytepluses.com:9095 --consumer.config ../config/consumer.properties
      start.time, end.time, data.consumed.in.MB, MB.sec, data.consumed.in.nMsg, nMsg.sec, rebalance.time.ms, fetch.time.ms, fetch.MB.sec, fetch.nMsg.sec
      2024-08-05 17:44:26:414, 2024-08-05 17:44:40:749, 95.3674, 6.6528, 100000, 6975.9330, 3099, 11236, 8.4877, 8899.9644
      ```
      

      After executing the command, you may receive results similar to the following:

      * Start time (start.time): 2024\-08\-05 17:44:26:414

      * End time (end.time): 2024\-08\-05 17:44:40:749

      * Maximum throughput (data.consumed.in.MB): 95.3674 MB/s

      * Average consumption per second (MB.sec): 6.6528 MB/s

      * Maximum number of messages consumed per second (data.consumed.in.nMsg): 100,000

      * Average number of messages consumed per second (nMsg.sec): 6975.9330
