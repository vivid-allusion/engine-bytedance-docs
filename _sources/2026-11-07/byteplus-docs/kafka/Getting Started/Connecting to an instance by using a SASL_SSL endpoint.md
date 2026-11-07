---
title: "Connecting to an instance by using a SASL_SSL endpoint"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL"
---

This topic describes how to connect to a Kafka instance by using a SASL_SSL endpoint. After connecting to the instance, you can produce and consume messages.

<span id="背景信息"></span>
## Background information

Message Queue for Kafka supports multiple secure access methods by using a SASL_SSL endpoint. The data must pass the SASL_PLAIN protocol authentication and SSL certificate authentication if this endpoint is used to connect to an instance.


* SASL_PLAIN protocol authentication means that a Kafka client must pass the Simple Authentication and Security Layer (SASL) username and password authentication before it can access a Kafka instance. PLAIN and SCRAM mechanisms are available for the access and connection to a Kafka instance. When you create an instance, a SASL user is created synchronously. You can also create a SASL user and grant data read and write permissions to it after the instance is created. When you access the instance, the corresponding SASL username and password can be used for permission authentication.

* Message Queue for Kafka supports message authentication and encryption by using SSL certificates. This ensures data security and prevents data interception and eavesdropping when data is being transferred over the network. This access method is more secure than ordinary access over the network. Currently, one\-way authentication is supported, that is, only the client verifies the certificate of the Kafka instance.


<span id="前提条件"></span>
## Before you begin


* Get the information on the SASL_SSL endpoint, including the connection address and the port number. For more information, refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).

* Create a topic. For more information, refer to [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic).

* If you want to access an instance over the internet, associate an elastic IP address (EIP) with the instance. We recommend that the upper limit of the EIP bandwidth is greater than the estimated maximum internet traffic. For more information, refer to [Enabling internet-facing access](https://docs.byteplus.com/en/docs/kafka/enabling-internet-facing).

* Install a Java Development Kit (JDK) in your development environment and configure environment variables. In addition, download an open source Kafka client, such as [Kafka client version 2.2.2](https://archive.apache.org/dist/kafka/2.2.2/kafka_2.11-2.2.2.tgz).


<span id="配置鉴权"></span>
## Configuring authentication

In the `./config` directory of the package of the Kafka client, modify the `consumer.properties` and `producer.properties` files. Add the following content according to the specific SASL mechanism type. For more information on the configuration file, refer to [Configuration file](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Configuration-file).


* If the PLAIN mechanism is used:

   Add the following content to the `consumer.properties` and `producer.properties` files. Note that the username and password of a PLAIN SASL user must be filled in the `username` and `password` fields.

   ```YAML
   sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="{$plainusername}" password="{$plainpwxxx}";        
   sasl.mechanism=PLAIN
   
   security.protocol=SASL_SSL
   ```
   

* If the SCRAM\-SHA\-256 mechanism is used:

   Add the following content to the `consumer.properties` and `producer.properties` files. Note that the username and password of a SCRAM SASL user must be filled in the `username` and `password` fields.

   ```YAML
   sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required username="{$scramusername}" password="{$scrampw}";        
   sasl.mechanism=SCRAM-SHA-256
   
   security.protocol=SASL_SSL
   ```
   

   The following table describes the fields.

   
   |**Field** |**Description** |
   |---|---|
   |username |The username of the SASL user.<br><br>If the PLAIN mechanism is used, type the username of the PLAIN SASL user that was specified when you created the instance.<br><br>If the SCRAM mechanism is used, type the username of the SCRAM SASL user. |
   |password |The password of the SASL user.<br><br>If the PLAIN mechanism is used, type the password of the PLAIN SASL user that was specified when you created the instance.<br><br>If the SCRAM mechanism is used, type the password of the SCRAM SASL user. |
   |security.protocol |The name of the protocol. Set this field to SASL_SSL. |
   


<span id="生产消息"></span>
## Producing messages


1. Uncompress the file of the Kafka client.

2. In the `./bin` directory, open the terminal window.

3. Run the following command to start the producer and begin producing messages.

   ```Bash
   bash kafka-console-producer.sh --broker-list ${SASL_SSL_ENDPOINT} --topic ${TOPIC_NAME}  --producer.config ../config/producer.properties
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |SASL_SSL Access Point |The domain name and port number of the SASL_SSL endpoint that is displayed on the instance details page in the Message Queue for Kafka console. |
   |Topic name |The topic name of your Kafka instance. |
   

4. Type the content of the message to be produced, and press Enter to send the message to your Kafka instance. All content that you type after the cursor is encapsulated into a message and sent to your Kafka instance. If you want to stop the message production process, press Ctrl+C to quit.

   ```Plain
   [root@kafkaecs bin]# bash kafka-console-producer.sh --broker-list kafka-ap-1dyb***.kafka.ibytepluses.com:9095 --topic mytopic --producer.config ../config/producer.properties
   >Hello world!
   >This is a Kafka message!
   >^C[root@kafkaecs bin]#
   ```
   


<span id="消费消息"></span>
## Consuming messages


1. Open another terminal window and run the following command to consume messages.

   If you want to stop the message consumption process, press Ctrl+C to quit.

   ```Bash
   bash kafka-console-consumer.sh --bootstrap-server ${SASL_SSL_ENDPOINT}  --topic ${TOPIC_NAME} --group ${CONSUMER_GROUP_NAME} --from-beginning --consumer.config ../config/consumer.properties
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |SASL_SSL Access Point |The domain name and port number of the SASL_SSL endpoint that is displayed on the instance details page in the Message Queue for Kafka console. |
   |Topic name |The topic name of your Kafka instance. |
   |Group name |The custom name of a consumer group.<br><br>If you have specified a consumer group name in the configuration file, make sure that the same name is used in the command. Otherwise, a message consumption failure may occur. |
   

2. After the command is run successfully, the consumers can receive the messages that are sent by the producer.

   ```Plain
   [root@kafka bin]# bash kafka-console-consumer.sh --bootstrap-server kafka-ap-1dyb***.kafka.ibytepluses.com:9095 --topic mytopic --group grouptest --from-beginning --consumer.config ../config/consumer.properties
   Hello world!
   This is a Kafka message!
   ^CProcessed a total of 2 messages
   [root@kafka bin]#
   ```
