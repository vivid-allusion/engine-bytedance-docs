---
title: "Preparations"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Preparations"
---

Before you use the open\-source SDK to connect to Message Queue for RabbitMQ for sending and receiving messages, you need to prepare the development environment by following the steps provided in this topic.

<span id=".5q2l6aqkMSDlvIDpgJrmnI3liqE="></span>
## Step 1: Enable the service

Before integrating Message Queue for RabbitMQ, you need to enable the service in the console and create a RabbitMQ instance. Message Queue for RabbitMQ offers multiple computing and storage specifications for you to choose from. Please select the instance specification according to your business requirements. For more details, see [Create Instance](https://docs.byteplus.com/en/docs/rabbitmq/Create_instance).

<span id=".5q2l6aqkMiDojrflj5blrp7kvovkv6Hmga8="></span>
## Step 2: Obtain instance information

After creating an instance, you can view the service access information for that instance on the instance details page. The **service access** section primarily displays the various access methods for the instance, such as the Web UI address under VPC and more. By accessing the address through the Web UI, you can log in to the open\-source RabbitMQ console to create resources and configure permissions. When sending and receiving messages using the open\-source Client SDK, you need to pass in parameters such as the AMQP endpoint in the code. Please securely store the relevant access point information according to business requirements.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Message Queue for RabbitMQ provides sample code for sending and receiving messages using the AMQP protocol for your reference. You can also implement business logic for other protocols on your own.</div>


<div data-tips="true" data-tips-type="tip">Before accessing the MQTT endpoint or the Web MQTT endpoint, please confirm that the <code>rabbitmq_mqtt</code> and <code>rabbitmq_web_mqtt</code> extensions have been enabled in the console. For detailed instructions on enabling the extension, please refer to <a href="https://docs.byteplus.com/en/docs/rabbitmq/Enable_extension">Extension Management</a>.</div>


<span id=".5q2l6aqkMyDliJvlu7rotYTmupA="></span>
## Step 3: Create resources

Before you can use a RabbitMQ instance to send and receive messages, you must first configure the Vhost and user, and create resources such as Exchange, Queue, and more. Do not directly use the default administrator account displayed in the Web UI to send or receive messages, as the default administrator is only configured with permissions for management operations and does not have permissions for reading or writing messages. You need to bind the target Vhost for users who are producing and consuming; otherwise, errors such as `access to vhost '/' refused for user 'xxx'` and `permission denied to connect` will occur during production or consumption. To bind a Virtual Host to a user, please see [Bind user and Vhost](https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost). You can create resources such as Exchange, Queue, and others in the following ways.


* Access the open\-source RabbitMQ Web UI console, then use it to create resources and configure permissions.

* Access the Web UI access point via the interface, and use the HTTP interface to create resources and configure permissions. For detailed operating procedures, please refer to [RabbitMQ Management HTTP API](https://rawcdn.githack.com/rabbitmq/rabbitmq-server/v3.9.10/deps/rabbitmq_management/priv/www/api/index.html).

* Create with Client SDK. Please view the corresponding sample code in the SDK list according to the programming language you are using.


<span id=".5q2l6aqkNCDmnI3liqHmjqXlhaU="></span>
## Step 4: Access the service

Call the Client SDK to send and receive messages.


* Based on the protocol type of your business, copy the corresponding AMQP or MQTT endpoint in the console and configure the relevant parameters.

* During the process of sending and receiving messages, use persistent connections and avoid establishing a new connection for each message, as this can result in a large amount of unnecessary resource consumption and may even trigger server\-side SYN Flood protection.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Next steps

Use Client SDK to send and receive messages. For sample code that demonstrates how to send and receive messages in Java, you can refer to the [Java SDK](https://docs.byteplus.com/en/docs/rabbitmq/Java_SDK_AMQP_protocol) and [Java SDK (MQTT protocol)](https://docs.byteplus.com/en/docs/rabbitmq/Java_SDK_MQTT_protocol).
