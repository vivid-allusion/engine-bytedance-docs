---
title: "Connecting to an instance by using the default endpoint"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/connecting-by-default"
---

This topic describes how to connect to a Kafka instance by using the default endpoint over a virtual private cloud (VPC). After connecting to the instance, you can produce and consume messages.

<span id="背景信息"></span>
## Background information

Message Queue for Kafka supports ordinary access over the PLAINTEXT protocol. Each Kafka instance comes with a default endpoint. When you connect to an instance by using the default endpoint over the VPC, the instance can be directly accessed without a username and password.

<span id="前提条件"></span>
## Before you begin


* Get the information on the default endpoint, including the connection address and the port number. For more information, refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).

* Create a topic. For more information, refer to [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic).

* Buy an Elastic Compute Service (ECS) instance, install a Java Development Kit (JDK), and configure environment variables. In addition, download an open source Kafka client, such as [Kafka client version 2.2.2](https://archive.apache.org/dist/kafka/2.2.2/kafka_2.11-2.2.2.tgz).


<span id="生产消息"></span>
## Producing messages


1. Uncompress the file of the Kafka client.

2. In the `./bin` directory, open the terminal window.

3. Run the following command to start the producer and begin producing messages.

   ```Bash
   bash kafka-console-producer.sh --broker-list ${DEFAULT_ENDPOINT} --topic ${TOPIC_NAME}
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |Default access point |The domain name and port number of the default endpoint that is displayed on the instance details page in the Message Queue for Kafka console. The default endpoint is used only for access over a VPC. |
   |Topic name |The topic name of your Kafka instance. |
   

4. Type the content of the message to be produced, and press Enter to send the message to your Kafka instance.

   All content that you type after the cursor is encapsulated into a message and sent to your Kafka instance. If you want to stop the message production process, press Ctrl+C to quit.

   ```Plain
   [root@kafkaecs bin]# bash kafka-console-producer.sh --broker-list kafka-ap-1dyb***.kafka.ibytepluses.com:9092 --topic mytopic
      
   >Hello world!
   >This is a Kafka message!
   >^C[root@kafkaecs bin]# 
   ```
   


<span id="e7c53575"></span>
## Consuming messages


1. Open another terminal window and run the following command to consume messages.

   If you want to stop the message consumption process, press Ctrl+C to quit.

   ```Bash
   bash kafka-console-consumer.sh --bootstrap-server ${DEFAULT_ENDPOINT}  --topic ${TOPIC_NAME} --group ${CONSUMER_GROUP_NAME} --from-beginning
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |Default access point |The domain name and port number of the default endpoint that is displayed on the instance details page in the Message Queue for Kafka console. |
   |Topic name |The topic name of your Kafka instance. |
   |Group ID |The custom name of a consumer group.<br><br>If you have specified a consumer group name in the configuration file, make sure that the same name is used in the command. Otherwise, a message consumption failure may occur. |
   

2. After the command is run successfully, the consumers can receive the messages that are sent by the producer.

   ```Plain
   [root@kafka bin]# bash kafka-console-consumer.sh --bootstrap-server kafka-ap-1dyb***.kafka.ibytepluses.com:9092 --topic mytopic --group grouptest --from-beginning
      
   Hello world!
   This is a Kafka message!
   ^CProcessed a total of 2 messages
   [root@kafka bin]#
   ```
