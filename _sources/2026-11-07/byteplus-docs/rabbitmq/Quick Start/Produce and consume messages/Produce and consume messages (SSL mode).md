---
title: "Produce and consume messages (SSL mode)"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Produce_and_consume_messages_SSL_mode"
---

BytePlus message queue for RabbitMQ is compatible with the open\-source RabbitMQ protocol. After creating a RabbitMQ instance, you can connect to the instance via SSL authentication to generate and consume messages.

For RabbitMQ tutorials, refer to the connection and usage guides in different languages provided on the RabbitMQ official website. For details, see the [RabbitMQ official website](https://www.rabbitmq.com/getstarted.html).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Prepare the development environment. For steps, see [Prepare the environment](https://docs.byteplus.com/en/docs/rabbitmq/Prepare_the_environment).

* Purchase a RabbitMQ instance and ensure its status is **Running**. For steps, see [Create Instance](https://docs.byteplus.com/en/docs/rabbitmq/Create_instance).

* Public network access and SSL authentication are enabled for the instance. When enabling public network access, it is recommended that the bound EIP bandwidth limit exceeds the estimated peak public network traffic. Operation steps see [Setting public network access](https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access). 

* Obtained the **AMQP endpoint** from RabbitMQ instance details. Operation steps: see [View instance information](https://docs.byteplus.com/en/docs/rabbitmq/View_instance_information).

* Before generating and consuming, create a new non\-Admin user on the RabbitMQ cluster management Web UI and bind the user to a Virtual Host. Operation steps see [Bind user and Vhost](https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost).


<span id=".5pON5L2c5q2l6aqk"></span>
## Operation steps


1. Install Java dependencies.

   1. If you use Maven, add the following dependency to the `pom.xml` file.

   ```java
   <dependency>
       <groupId>com.rabbitmq</groupId>
       <artifactId>amqp-client</artifactId>
       <version>5.12.0</version>
   </dependency>
   ```
   

   2. If you use Gradle, add the following dependency:

   ```java
   compile 'com.rabbitmq:amqp-client:5.12.0'
   ```
   

2. Connect to the instance and generate messages.

   To improve stability and availability, it is recommended to refer to the sample code and enable mechanisms such as **Client auto\-reconnect** and **Publish Confirm**.

   ```java
   package org.example.amqp.producer;
   
   import com.rabbitmq.client.*;
   import java.nio.charset.StandardCharsets;
   import java.util.HashMap;
   import java.util.UUID;
   
   public class SimpleProducerSSL {
       private static final String host= "your-end-point";  //AMQP protocol public access address.
       private static final int port= 5671;
       private static final String userName= "your-user-name";
       private static final String password= "your-password";
       private static final String vhost= "/";
       private static final String exchangeName= "your-exchange";
       private static final String queueName= "your-queue";
       private static final String bindingKey= "your-key";
       private static final int deliveryMode= 2;
       private static final int batchSize= 50;
       private static final int publishConfirmTimeout= 10000; // publish confirm timeout 10 seconds
   
       public static void main(String[] args) throws Exception{
           ConnectionFactory factory = new ConnectionFactory();
   // Set the access point. View it on the RabbitMQ version console instance details page
           factory.setHost(host);
   // Set port, AMQP protocol SSL encrypted port 5671
           factory.setPort(port);
   // Username, configured and managed in the WebUI console
           factory.setUsername(userName);
   // Password, configured and managed in the WebUI console
           factory.setPassword(password);
   // Set Vhost name. Ensure it is created in the RabbitMQ version console
           factory.setVirtualHost(vhost);
   // Enable SSL (optional)
           factory.useSslProtocol();
   
   // Enable automatic reconnection, default is true
           factory.setAutomaticRecoveryEnabled(true);
   // Set automatic reconnection interval
           factory.setNetworkRecoveryInterval(5000);
   // Set negotiation timeout for connection establishment
           factory.setConnectionTimeout(20000);
   
   // Establish Connection
           Connection connection = factory.newConnection();
   
   // Create channel
           Channel channel = connection.createChannel();
   
   // Enable publish confirm (optional, recommended)
           channel.confirmSelect();
   
   // Create Exchange (optional)
           channel.exchangeDeclare(exchangeName, "direct", true, false, false,null);
   // Create a Classic type queue (optional)
           channel.queueDeclare(queueName, true, false, false, new HashMap<String, Object>());
   // Bind exchange and queue (optional)
           channel.queueBind(queueName, exchangeName, bindingKey);
   
   // Register publish confirm callback
           channel.addConfirmListener(new ConfirmListener() {
               public void handleNack(long deliveryTag, boolean multiple) {
   // Handle nack callback
                   System.out.println("nack received: " + deliveryTag);
               }
   
               public void handleAck(long deliveryTag, boolean multiple) {
   // handle ack callback
                   System.out.println("ack received: " + deliveryTag);
               }
           });
   
           int msgsToSend = 10000;
   
   // continue sending messages
           while (msgsToSend >0) {
   // Set message properties
               AMQP.BasicProperties props = new AMQP.BasicProperties.Builder().messageId(UUID.randomUUID().toString()).deliveryMode(deliveryMode).build();
               String msgBody = "hello rabbitmq";
   
               try {
                   channel.basicPublish(exchangeName, bindingKey, true, props, msgBody.getBytes(StandardCharsets.UTF_8));
   
                   msgsToSend--;
   
   // Wait for confirm of the previous batch of sent messages
                   if (msgsToSend%batchSize  ==0) {
                       channel.waitForConfirms(publishConfirmTimeout);
                   }
               } catch (Exception e) {
                   e.printStackTrace();
               }
           }
   
   // Close Channel and Connection
           channel.close();
           connection.close();
       }
   }
   ```
   

3. Connect to the instance and consume messages.

   ```java
   package org.example.amqp.consumer;
   
   import com.rabbitmq.client.*;
   
   import java.io.IOException;
   import java.nio.charset.StandardCharsets;
   import java.security.KeyManagementException;
   import java.security.NoSuchAlgorithmException;
   import java.util.HashMap;
   import java.util.concurrent.TimeoutException;
   
   public class SimpleConsumerSSL {
       private static final String host= "your-end-point"; // AMQP protocol public network access address.
       private static final int port= 5671;
       private static final String userName= "your-user-name";
       private static final String password= "your-password";
       private static final String vhost= "/";
       private static final String queueName= "your-queue";
   
       public static void main(String[] args) throws IOException, TimeoutException, KeyManagementException, NoSuchAlgorithmException {
           ConnectionFactory factory = new ConnectionFactory();
   // Set the access point. View it on the RabbitMQ version console instance details page
           factory.setHost(host);
   // Set port. Default port for AMQP protocol is 5672
           factory.setPort(port);
   // Username, configured and managed in the WebUI console
           factory.setUsername(userName);
   // password, configured and managed in the WebUI console
           factory.setPassword(password);
   // Set Vhost name, make sure it is created in the RabbitMQ version console
           factory.setVirtualHost(vhost);
   // Enable SSL
           factory.useSslProtocol();
   
   // Establish Connection
           Connection connection = factory.newConnection();
   // Create Channel
           Channel channel = connection.createChannel();
   
           // Create Classic type queue (optional, skip if already created in WebUI console)
           channel.queueDeclare(queueName, true, false, false, new HashMap<String, Object>());
   
   // Start consuming
           consume(connection);
   
   // Close Channel and Connection
           channel.close();
           connection.close();
       }
   
       private static void consume(Connection connection) throws IOException {
           final Channel channel = connection.createChannel();
   
           channel.basicConsume(queueName, true, "test_consumer", new DefaultConsumer(channel) {
               @Override
               public void handleDelivery(String consumerTag, Envelope envelope,
                                          AMQP.BasicProperties properties, byte[] body)
                       throws IOException {
   // Process received message
                   System.out.printf("Received Message: %s, consumerTag: %s, deliveryTag: %s, messageId: %s\n", new String(body, StandardCharsets.UTF_8),
                           consumerTag, envelope.getDeliveryTag(), properties.getMessageId());
               }
           });
       }
   }
   ```
