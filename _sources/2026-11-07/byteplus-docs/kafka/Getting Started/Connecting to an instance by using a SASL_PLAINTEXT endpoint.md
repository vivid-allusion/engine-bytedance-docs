---
title: "Connecting to an instance by using a SASL_PLAINTEXT endpoint"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_PLAINTEXT"
---

This topic describes how to connect to a Kafka instance by using a SASL_PLAINTEXT endpoint. After connecting to the instance, you can produce and consume messages.

<span id="背景信息"></span>
## Background information

Message Queue for Kafka supports secure access over the SASL/PLAIN protocol. Each Kafka instance comes with a SASL_PLAINTEXT endpoint. When you connect to an instance by using a SASL_PLAINTEXT endpoint, the Simple Authentication and Security Layer (SASL) username and password authentication is required before the instance can be accessed. PLAIN and SCRAM mechanisms are available for the access and connection to a Kafka instance. When you create an instance, a SASL user is created synchronously. You can also create a SASL user after the instance is created. When you access the instance, use different mechanisms to produce and consume messages as needed.

By default, a Kafka instance can be accessed from the virtual private cloud (VPC). When the internet\-facing access feature is enabled, you can also access the instance over the internet. The instance can be connected by using a SASL_PLAINTEXT endpoint in both network types. The SASL_SSL endpoint is recommended if SSL authentication is required for accessing an instance over the internet. For more information, refer to [Connecting to an instance by using a SASL_SSL endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL).

<span id="前提条件"></span>
## Before you begin


* Get the information on the SASL_PLAINTEXT endpoint, including the connection address and the port number. For more information, refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).

* Create a topic. For more information, refer to [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic).

* If you want to access an instance over the internet, associate an elastic IP address (EIP) with the instance. We recommend that the upper limit of the EIP bandwidth is greater than the estimated maximum internet traffic. For more information, refer to [Enabling internet-facing access](https://docs.byteplus.com/en/docs/kafka/enabling-internet-facing).

* Install a Java Development Kit (JDK) in your development environment and configure environment variables. In addition, download an open source Kafka client, such as [Kafka client version 2.2.2](https://archive.apache.org/dist/kafka/2.2.2/kafka_2.11-2.2.2.tgz).


<span id="配置鉴权"></span>
## Configuring authentication

In the `./config` directory of the package of the Kafka client, modify the `consumer.properties` and `producer.properties` files.

Add the following content according to the specific SASL mechanism type. For more information on the configuration file, refer to [Configuration file](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Configuration-file).


* If the PLAIN mechanism is used:

   Add the following content to the `consumer.properties` and `producer.properties` files. Note that the username and password of a PLAIN SASL user must be filled in the `username` and `password` fields.


```YAML
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="{$plainusername}" password="{$plainpwxxx}";        
sasl.mechanism=PLAIN
security.protocol=SASL_PLAINTEXT
```



* If the SCRAM\-SHA\-256 mechanism is used:

   Add the following content to the `consumer.properties` and `producer.properties` files. Note that the username and password of a SCRAM SASL user must be filled in the `username` and `password` fields.


```YAML
sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required username="{$scramusername}" password="{$scrampw}";          
sasl.mechanism=SCRAM-SHA-256
security.protocol=SASL_PLAINTEXT
```


<span id="生产消息"></span>
## Producing messages


1. Uncompress the file of the Kafka client.

2. In the `./bin` directory, open the terminal window.

3. Run the following command to start the producer and begin producing messages.

   ```Bash
   bash kafka-console-producer.sh --broker-list ${SASL_ENDPOINT} --topic ${TOPIC_NAME}  --producer.config ../config/producer.properties
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |SASL_PLAINTEXT Access Point |The domain name and port number of the SASL_PLAINTEXT endpoint that is displayed on the instance details page in the Message Queue for Kafka console. |
   |Topic name |The topic name of your Kafka instance. |
   

4. Type the content of the message to be produced, and press Enter to send the message to your Kafka instance.

   All content that you type after the cursor is encapsulated into a message and sent to your Kafka instance. If you want to stop the message production process, press Ctrl+C to quit.

   ```Plain
   [root@kafkaecs bin]# bash kafka-console-producer.sh --broker-list kafka-ap-1dyb8**.kafka.ibytepluses.com:9093 --topic mytopic --producer.config ../config/producer.properties
   >Hello world!
   >This is a Kafka message!
   >^C[root@kafkaecs bin]# 
   ```
   


<span id="32ccab6f"></span>
## Consuming messages


1. Open another terminal window and run the following command to consume messages.

   If you want to stop the message consumption process, press Ctrl+C to quit.

   ```Bash
   bash kafka-console-consumer.sh --bootstrap-server ${SASL_ENDPOINT}  --topic ${TOPIC_NAME} --group ${CONSUMER_GROUP_NAME} --from-beginning --consumer.config ../config/consumer.properties   
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |SASL_PLAINTEXT Access Point |The domain name and port number of the SASL_PLAINTEXT endpoint that is displayed on the instance details page in the Message Queue for Kafka console. |
   |Topic name |The topic name of your Kafka instance. |
   |Group name |The custom name of a consumer group.<br><br>If you have specified a consumer group name in the configuration file, make sure that the same name is used in the command. Otherwise, a message consumption failure may occur. |
   

2. After the command is run successfully, the consumers can receive the messages that are sent by the producer.

   ```Plain
   [root@kafka bin]# bash kafka-console-consumer.sh --bootstrap-server kafka-ap-1dyb***.kafka.ibytepluses.com:9093 --topic mytopic --group grouptest --from-beginning --consumer.config ../config/consumer.properties
   Hello world!
   This is a Kafka message!
   ^CProcessed a total of 2 messages
   [root@kafka bin]# 
   ```
