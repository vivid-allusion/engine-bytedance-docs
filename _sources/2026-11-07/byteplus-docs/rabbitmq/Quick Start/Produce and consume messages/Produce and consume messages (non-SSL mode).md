---
title: "Produce and consume messages (non-SSL mode)"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Produce_and_consume_messages_non_SSL_mode"
---

BytePlus message queue for RabbitMQ is compatible with the open\-source RabbitMQ protocol. After creating a RabbitMQ instance, you can connect to it to produce and consume messages.

For RabbitMQ usage tutorials, refer to the connection and usage guides in different languages provided by the official RabbitMQ website. For details, see [RabbitMQ official website](https://www.rabbitmq.com/getstarted.html).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the RabbitMQ instance has SSL authentication enabled, refer to <a href="https://docs.byteplus.com/en/docs/rabbitmq/Produce_and_consume_messages_SSL_mode">Produce and consume messages (SSL mode)</a> to connect to the instance and perform messaging.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Prepare the development environment. For specifications, please refer to [Prepare the environment](https://docs.byteplus.com/en/docs/rabbitmq/Prepare_the_environment).

* Purchase the RabbitMQ instance and make sure the instance status is **Running**. For operation steps, please refer to [Create Instance](https://docs.byteplus.com/en/docs/rabbitmq/Create_instance).

* Obtain the **AMQP endpoint** of the RabbitMQ instance details. Operation steps: Please refer to [View instance information](https://docs.byteplus.com/en/docs/rabbitmq/View_instance_information).

* Before producing and consuming, create a new non\-Admin user on the RabbitMQ cluster management Web UI and bind the user to a Virtual Host. Operation steps: Please refer to [Bind user and Vhost](https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost).


<span id=".5pON5L2c5q2l6aqk"></span>
## Operation steps


1. Install Java dependency.

   1. If the project uses Maven, add the following dependency to the `pom.xml` file.

   ```java
   <dependency>
       <groupId>com.rabbitmq</groupId>
       <artifactId>amqp-client</artifactId>
       <version>5.12.0</version>
   </dependency>
   ```
   

   2. If the project uses Gradle, add the following dependency:

   ```java
   compile 'com.rabbitmq:amqp-client:5.12.0'
   ```
   

2. Connect to the instance and produce messages.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To improve stability and availability, we recommend that you follow the sample code and enable <strong>Client auto\-reconnect</strong>, <strong>Publish Confirm</strong>, and other mechanisms.   </div>
   

   ```java
   package org.example.amqp.producer;
   
   import com.rabbitmq.client.*;
   import java.nio.charset.StandardCharsets;
   import java.util.HashMap;
   import java.util.UUID;
   
   public class SimpleProducer {
     private static final String host= "your-end-point"; // AMQP protocol private network access address.
     private static final int port= 5672;
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
   // Set the access point. View it on the instance details page in the RabbitMQ version console
           factory.setHost(host);
   // Set the port, AMQP protocol SSL encrypted port 5671
           factory.setPort(port);
   // Username, configured and managed in the WebUI console
           factory.setUsername(userName);
   // Password configured and managed in the WebUI console
           factory.setPassword(password);
   // Set the Vhost name, ensure it is created in the RabbitMQ version console
           factory.setVirtualHost(vhost);
   
   // Enable automatic recovery, default is true
           factory.setAutomaticRecoveryEnabled(true);
   // Set automatic recovery interval
           factory.setNetworkRecoveryInterval(5000);
   // Set negotiation timeout for connection establishment
           factory.setConnectionTimeout(20000);
   
   // Establish Connection
           Connection connection = factory.newConnection();
   
   // Create channel
           Channel channel = connection.createChannel();
   
   // Enable publish confirm (optional, recommended)
           channel.confirmSelect();
   
   // Create exchange (optional)
           channel.exchangeDeclare(exchangeName, "direct", true, false, false,null);
   // Create classic queue (optional)
           channel.queueDeclare(queueName, true, false, false, new HashMap<String, Object>());
   // Bind Exchange and queue (optional)
           channel.queueBind(queueName, exchangeName, bindingKey);
   
   // Register publish confirm callback
           channel.addConfirmListener(new ConfirmListener() {
               public void handleNack(long deliveryTag, boolean multiple) {
   // handle nack callback
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
   
                   //  Wait for confirm of the previous batch of sent messages
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
   
   public class SimpleConsumer {
       private static final String host= "your-end-point"; // AMQP protocol private network access address.
       private static final int port= 5672;
       private static final String userName= "your-user-name";
       private static final String password= "your-password";
     private static final String vhost= "/";
     private static final String queueName= "your-queue";
   
       public static void main(String[] args) throws IOException, TimeoutException, KeyManagementException, NoSuchAlgorithmException {
           ConnectionFactory factory = new ConnectionFactory();
   // Set the access point. View it on the RabbitMQ version console instance detail page
           factory.setHost(host);
   // Set the port. Default AMQP protocol port is 5672
           factory.setPort(port);
   // Username, configured and managed in the WebUI console
           factory.setUsername(userName);
   // Password, configured and managed in the WebUI console
           factory.setPassword(password);
   // Set the Vhost name. Please ensure it is created in the RabbitMQ version console.
           factory.setVirtualHost(vhost);
   
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
   // Process incoming messages
                   System.out.printf("Received Message: %s, consumerTag: %s, deliveryTag: %s, messageId: %s\n", new String(body, StandardCharsets.UTF_8),
                           consumerTag, envelope.getDeliveryTag(), properties.getMessageId());
               }
           });
       }
   }
   ```
