---
title: "Java SDK (MQTT protocol)"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Java_SDK_MQTT_protocol"
---

This topic uses call to the Client SDK for Java as an example to describe the process of sending and receiving messages over the MQTT protocol using the open\-source SDK, and provides corresponding sample code. The message sending and receiving process of SDKs for other languages or frameworks is similar.

<span id="368b6b51"></span>
## Note


* This topic uses sending and receiving messages using the MQTT protocol as an example to demonstrate sample code for message production and consumption. Based on the protocol type used in your business, copy the MQTT access point from the console and configure the relevant parameters.

* During message transmission and reception, use persistent connections and avoid creating a new connection for each message, as this will result in significant unnecessary resource consumption and may even trigger SYN Flood protection on the server.


<span id="8eef2753"></span>
## Example projects

For sample code on sending and receiving messages with RabbitMQ, refer to the official RabbitMQ documentation [RabbitMQ SDK usage examples](https://rabbitmq.com/getstarted.html) and the sample code project for common scenarios, [rabbitmq-tutorials](https://github.com/rabbitmq/rabbitmq-tutorials), on [GitHub](https://github.com/rabbitmq).

In addition, Message Queue for RabbitMQ provides a sample project, [Java SDK Demo for the MQTT protocol](https://rabbitmq-demo.tos-cn-beijing.volces.com/MQTT-DEMO.zip), for your reference.

<span id="a55d36fb"></span>
## Environment setup


1. Install JDK8 or a later version of JDK in the client environment.

2. Add a dependency.

   * If the project is built using Maven, add the following dependencies to the `pom.xml` file.

      ```XML
      <dependency>
        <groupId>org.eclipse.paho</groupId>
        <artifactId>org.eclipse.paho.client.mqttv3</artifactId>
        <version>1.2.5</version>
      </dependency>
      ```
      

   * If the project uses Gradle, add the following dependency:

      ```JSON
      compile 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.2.5'
      ```
      


<span id="663d0b35"></span>
## Access configuration

When using the Client to connect to a RabbitMQ instance for message production and consumption, you need to configure the following parameters in the code. Please ensure that these parameters are configured correctly in the Client code.


|**Parameter Name** |**Parameter description** |
|---|---|
|host |Access point domain name: Go to the RabbitMQ console instance details page and obtain the domain part displayed under **MQTT access point**, for example, rbtmq\-xxxxxxx.rabbitmq.ixxx.com. |
|port |Access point port: Go to the instance details page in the RabbitMQ console and retrieve the port number displayed for the **MQTT access point**, for example, 8883. |
|username |To obtain the access username, please go to the RabbitMQ console instance details page, use the **Web UI access point** to enter the RabbitMQ Cluster web console page, and check the **Users** tab.<br><br>Make sure that the user account has already been bound to the vhost to be accessed. For specific instructions, see [Bind User and Vhost](https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost). |
|password |To access the user password, go to the RabbitMQ console instance details page, enter the RabbitMQ Cluster Web console page via the **Web UI access point**, and check the **Users** tab. |


<span id="a33a64b2"></span>
## Message production

Example code for message production is as follows:

```Java
package org.example;
import org.eclipse.paho.client.mqttv3.*;


public class RabbitMQMQTTProducer {
    //Release client
    public static void main(String[] args) {
        String url = "ssl://xxxxxx.rabbitmq.xxx.com:8883"; // MQTT broker server address, public network connection.
        /* String url = "tcp://xxxxxx.rabbitmq.ixxx.com:1883"; // MQTT broker server address, private network connection.  */
        String clientId = "publisher-xxx"; // Client ID, user-defined.
        String topic = "my-topic"; // Published topics.
        String message = "Hello, MQTT!"; // Content of the published message.
        String username = "demo-user"; // Username for the MQTT broker server.
        String password = "demo-user-password"; // Password for the MQTT broker server.

        try {
            MqttClient client = new MqttClient(url, clientId);
            MqttConnectOptions connOpts = new MqttConnectOptions();
            connOpts.setCleanSession(true);
            connOpts.setUserName(username);
            connOpts.setPassword(password.toCharArray());

            // Establish connection
            client.connect(connOpts);
            // Create a message object
            MqttMessage mqttMessage = new MqttMessage(message.getBytes());
            mqttMessage.setQos(1); // Set the QoS (Quality of Service) level for the message

            // Publish message
            client.publish(topic, mqttMessage);
            // Disconnect
            client.disconnect();
        } catch (MqttException e) {
            e.printStackTrace();
        }
    }
}
```


<span id="4b9e1f44"></span>
## Message consumption

Example code for message consumption is as follows:

```Java
import org.eclipse.paho.client.mqttv3.*;

public class RabbitMQMQTTConsumer {
    public static void main(String[] args) {
        String broker = "ssl://xxxxxx.rabbitmq.xxx.com:8883"; // MQTT broker server address, public network address.
        /* String url = "tcp://xxxxxx.rabbitmq.ixxx.com:1883"; // MQTT broker server address, private network address. */
        String clientId = "consumer-xxx"; // Client ID
        String topic = "my-topic"; Subscribed topics
        String username = "demo-user"; // Username for the MQTT broker server
        String password = "demo-user-password"; // Password for the MQTT broker

        try {
            MqttClient client = new MqttClient(broker, clientId);
            MqttConnectOptions connOpts = new MqttConnectOptions();
            connOpts.setCleanSession(true);
            connOpts.setUserName(username);
            connOpts.setPassword(password.toCharArray());

            // Set up message arrival callback handler
            client.setCallback(new MqttCallback() {
                @Override
                public void connectionLost(Throwable cause) {
                    System.out.println("Connection lost: " + cause.getMessage());
                }

                @Override
                public void messageArrived(String topic, MqttMessage message) throws Exception {
                    System.out.println("Received message from topic: " + topic);
                    System.out.println("Message: " + new String(message.getPayload()));
                }

                @Override
                public void deliveryComplete(IMqttDeliveryToken token) {
                }
            });

            // Establish a connection
            client.connect(connOpts);

            // Subscribe to topics
            client.subscribe(topic);

            // Wait for the message to arrive
            synchronized (client) {
                client.wait();
            }

            // Disconnect
            client.disconnect();
        } catch (MqttException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
