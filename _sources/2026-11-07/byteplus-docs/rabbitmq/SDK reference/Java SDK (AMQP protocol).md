---
title: "Java SDK (AMQP protocol)"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Java_SDK_AMQP_protocol"
---

This topic uses call Client SDK for Java as an example to describe the process of sending and receiving messages using the AMQP protocol with an open\-source SDK, and provides corresponding sample code. The process of sending and receiving SDK messages is similar in other languages or frameworks.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note


* This document demonstrates sample code for message production and consumption under the AMQP protocol. Based on the protocol type of your business, copy the AMQP access point in the console and configure the relevant parameters.

* During message transmission, use persistent connections and avoid creating a new connection for each message. Otherwise, this will result in significant unnecessary resource consumption and may even trigger SYN Flood protection on the server.

* Directly using the administrator account for production and consumption may pose a risk of information leakage. Before producing and consuming messages, you need to create a new user with a non\-Admin role in the RabbitMQ Cluster management Web UI, and bind a Virtual Host to the new user. See [Bind users and Vhost](https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost) for the steps.


<span id="c3accef1"></span>
## Sample projects

For sample code on sending and receiving messages with RabbitMQ, refer to the official RabbitMQ documentation [RabbitMQ SDK usage examples](https://rabbitmq.com/getstarted.html) and the sample code project for common scenarios, [rabbitmq-tutorials](https://github.com/rabbitmq/rabbitmq-tutorials), on [GitHub](https://github.com/rabbitmq). In addition, Message Queue for RabbitMQ provides a sample project, [Java SDK Demo for the AMQP protocol](https://rabbitmq-demo.tos-cn-beijing.volces.com/AMQP-DEMO.zip), for your reference.

<span id=".546v5aKD5YeG5aSH"></span>
## Environment setup


1. Install JDK 8 or a later version in the client environment.

2. Add dependencies

   * If the project uses Maven, add the following dependency to the `pom.xml` file.

      ```XML
      <dependency>
          <groupId>com.rabbitmq</groupId>
          <artifactId>amqp-client</artifactId>
          <version>5.12.0</version>
      </dependency>
      ```
      

   * If the project uses Gradle, add the following dependency:

      ```xml
      compile 'com.rabbitmq:amqp-client:5.12.0'
      ```
      


<span id=".5o6l5YWl6YWN572u"></span>
## Access configuration

When using a client to connect to a RabbitMQ instance for message production and consumption, you must configure the following parameters in your code. Please ensure that these parameters are correctly configured in the client code.


|**Parameter Name** |**Parameter description** |
|---|---|
|host |Access point domain name Go to the RabbitMQ console instance details page and obtain the domain portion displayed under the **AMQP access point**. |
|port |Access point port Go to the instance details page in the RabbitMQ console and obtain the port displayed in the **AMQP access point** section. |
|username |To view the username, go to the RabbitMQ console instance details page. Use the **Web UI access point** to enter the RabbitMQ Cluster web console page, and check the **Users** tab. Please ensure that the User you are using has already been bound to the vhost to be accessed. For detailed instructions, see [Binding User and Vhost](https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost). |
|password |To access the user password, go to the RabbitMQ console instance details page, use the **Web UI access point** to enter the RabbitMQ Cluster Web console page, and view it in the **Users** tab. |


<span id=".5raI5oGv55Sf5Lqn"></span>
## Message production

The following is an example code for message production.

```Java
import com.rabbitmq.client.*;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.security.KeyManagementException;
import java.security.NoSuchAlgorithmException;
import java.util.concurrent.TimeoutException;
import java.util.HashMap;
import java.util.UUID;

public class Producer {
    public static void main(String[] args) throws IOException, TimeoutException, NoSuchAlgorithmException, KeyManagementException {
        // If SSL authentication is disabled, the private network access point domain name is used. If SSL authentication is enabled, the public network access point domain name is used.
        final String host = "rbtmq-xxxxx.rabbitmq.xxx.com";
        // The private network access point port is 5672, and the public network access point port is 5671.
        final int port = 5671;
        // It is recommended to use a user with a non-Admin role.
        final String username = "demo-user";
        final String password = "demo-user-password";

        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost(host);
        factory.setPort(port);
        factory.setUsername(username);
        factory.setPassword(password);
        // If you use SSL to send and receive messages, please uncomment the following.
        // factory.useSslProtocol();

        // Configure connection-related parameters according to business characteristics and network conditions.
        factory.setAutomaticRecoveryEnabled(true);
        factory.setNetworkRecoveryInterval(5000);
        factory.setConnectionTimeout(30 * 1000);
        factory.setHandshakeTimeout(30 * 1000);
        factory.setShutdownTimeout(0);

        // The following is the AMQP-0-9-1 protocol object configuration for message publishing
        final String vhost = "/";
        final String exchange = "demo-exchange";
        final String exchangeType = "direct";
        final String queue = "demo-queue";
        final String bindingKey = "foo";

        // Set the Vhost name. Make sure it has been created in the RabbitMQ cluster web console.
        factory.setVirtualHost(vhost);

        // Creating a Connection and a Channel
        Connection connection = factory.newConnection();
        Channel channel = connection.createChannel();

        // Create a direct exchange. If you have already created it manually in the RabbitMQ cluster web console, you can skip this step.
        channel.exchangeDeclare(exchange, exchangeType, true, false, false, null);
        HashMap<String, Object> arg = new HashMap<>();
        channel.queueDeclare(queue, true, false, false, arg);
        channel.queueBind(queue, exchange, bindingKey);

        // Start message production
        for (int i = 0; i < 100; i++  ) {
            // Fill in the corresponding BindingKey according to business needs.
            AMQP.BasicProperties props = new AMQP.BasicProperties.Builder().messageId(UUID.randomUUID().toString()).build();
            channel.basicPublish(exchange, bindingKey, true, props,
                    ("demo message "  + i).getBytes(StandardCharsets.UTF_8));
        }

        channel.close();
        connection.close();
    }
}
```


<span id=".5raI5oGv5raI6LS5"></span>
## Message consumption

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using the AMQP 0\-9\-1 protocol, it is not recommended to fetch messages one by one using the <code>basic.get</code> method, as this approach is less efficient compared to persistent consumers. For a detailed description, please refer to the <a href="https://www.rabbitmq.com/consumers.html#fetching">RabbitMQ official documentation</a>. The sample code for message consumption is as follows.</div>


```Java
import com.rabbitmq.client.*;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.security.KeyManagementException;
import java.security.NoSuchAlgorithmException;
import java.util.HashMap;
import java.util.concurrent.CountDownLatch;
import java.util.concurrent.TimeoutException;

public class Consumer {
    public static void main(String[] args) throws IOException, TimeoutException, InterruptedException, NoSuchAlgorithmException, KeyManagementException {
        // If SSL authentication is disabled, the private network access point domain name is used. If SSL authentication is enabled, the public network access point domain name is used.
        final String host = "rbtmq-xxxxx.rabbitmq.xxx.com";
        // The private network access point port is 5672, and the public network access point port is 5671.
        final int port = 5671;
        // It is recommended to use a user with a non-Admin role.
        final String username = "demo-user";
        final String password = "demo-user-password";

        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost(host);
        factory.setPort(port);
        factory.setUsername(username);
        factory.setPassword(password);
        // If you use SSL to send and receive messages, please uncomment the following.
        // factory.useSslProtocol();

        // Configure connection-related parameters according to business characteristics and network conditions.
        factory.setAutomaticRecoveryEnabled(true);
        factory.setNetworkRecoveryInterval(5000);
        factory.setConnectionTimeout(30 * 1000);
        factory.setHandshakeTimeout(30 * 1000);
        factory.setShutdownTimeout(0);

        // The following is the AMQP-0-9-1 protocol object configuration for message publishing
        final String vhost = "/";
        final String exchange = "demo-exchange";
        final String exchangeType = "direct";
        final String queue = "demo-queue";
        final String bindingKey = "foo";

        // Set the Vhost name. Make sure it has been created in the RabbitMQ cluster web console.
        factory.setVirtualHost(vhost);

        // Creating a Connection and a Channel
        Connection connection = factory.newConnection();
        Channel channel = connection.createChannel();

        // Create a direct exchange. If you have already created it manually in the RabbitMQ cluster web console, you can skip this step.
        channel.exchangeDeclare(exchange, exchangeType, true, false, false, null);
        HashMap<String, Object> arg = new HashMap<>();
        channel.queueDeclare(queue, true, false, false, arg);
        channel.queueBind(queue, exchange, bindingKey);

        // Start consuming messages.
        channel.basicConsume(queue, false, "consumertag", new DefaultConsumer(channel) {
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope,
                                       AMQP.BasicProperties properties, byte[] body)
                    throws IOException {
                System.out.printf("receive message: "  + new String(body, StandardCharsets.UTF_8) +  ", deliveryTag: "  + envelope.getDeliveryTag()  + ", messageId: " +  properties.getMessageId());
                // Single message reply ack
                channel.basicAck(envelope.getDeliveryTag(), false);
            }
        });
        CountDownLatch latch = new CountDownLatch(1);
        Runtime.getRuntime().addShutdownHook(new Thread(() -> {
            try {
                channel.getConnection().close();
            } catch (IOException e) {
                System.out.println("close connection error." + e);
            }
            latch.countDown();
        }));
        latch.await();

        connection.close();
    }
}
```


<span id=".6ZSZ6K-v56CB77yIQU1RUO-8iQ=="></span>
## Error codes (AMQP)


|**Error code** |**Description** |**Handling method** |
|---|---|---|
|200 |Request succeeded. |None |
|403 |Permission error. |Ensure that the user has access permissions for the vhost, and that the username and password are configured correctly. |
|404 |Resource does not exist. |Ensure that resources already exist and meet expectations. |
|406 |Pre\-check failed. |Ensure that the parameters are correct when calling AMQP protocol methods. |
|503 |Invalid command. |Stop using AMQP protocol methods or Exchange types that are currently not supported by Message Queue for RabbitMQ. |
|541 |Internal server error. |After identifying the problem based on the error information returned, contact the Message Queue for RabbitMQ technical support personnel for assistance. |
