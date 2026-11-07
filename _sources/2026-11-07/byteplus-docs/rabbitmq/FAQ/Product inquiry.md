---
title: "Product inquiry"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Product_inquiry"
---

<span id=".5pSv5oyB5ZOq5Lqb6K-t6KiA55qE5a6i5oi356uv77yf"></span>
## Which client languages are supported?

RabbitMQ supports the [AMQP 0-9-1](https://github.com/rabbitmq/amqp-0.9.1-spec) protocol and the MQTT protocol. Users can use any SDK that implements both the AMQP 0\-9\-1 protocol and the MQTT protocol to send and receive messages. For documentation on common programming languages and their corresponding SDKs, please refer to the table below.

For more information about the open\-source RabbitMQ SDK, please refer to [Clients Libraries and Developer Tools](https://www.rabbitmq.com/devtools.html).


|**Languages or frameworks** |**SDK** |
|---|---|
|Java |[RabbitMQ Java Client Library](https://www.rabbitmq.com/java-client.html) |
|Spring Framework |[Spring AMQP project for Java](https://spring.io/projects/spring-amqp) |
|.NET |[.NET SDK](https://www.rabbitmq.com/devtools.html#dotnet-dev) |
|Python |[Python SDK](https://www.rabbitmq.com/devtools.html#python-dev) |
|PHP |[PHP SDK](https://www.rabbitmq.com/devtools.html#php-dev) |
|Rust |[Rust SDK](https://www.rabbitmq.com/devtools.html#rust-dev) |
|C and C++ |[C and C++ SDK](https://www.rabbitmq.com/devtools.html#c-dev) |
|Go |[Go SDK](https://www.rabbitmq.com/devtools.html#go-dev) |
|JavaScript and Node |[JavaScript and Node SDK](https://www.rabbitmq.com/devtools.html#node-dev) |
|Objective\-C and Swift |[Objective-C and Swift SDK](https://www.rabbitmq.com/devtools.html#objc-swift-dev) |


<span id=".5pSv5oyB55qE5raI5oGv5L2T5pyA5aSn5piv5aSa5bCR77yf"></span>
## What is the maximum supported message size?

The server side of Message Queue for RabbitMQ supports a maximum message size of 32 MiB, and this limit cannot be changed. Messages that exceed the limit cannot be pushed successfully.

<span id=".5raI5oGv55qE5L-d55WZ5pe26Ze05piv5aSa5LmF77yf"></span>
## How long is the message retention period?

The retention period of a message on the server depends on the expiration time (TTL) set when the message is sent. Normally, if no expiration time is set, the message will be retained on the server until it is consumed, after which it will be automatically deleted. Additionally, messages that have not yet been persisted may be deleted when restarting the instance for various reasons.

<span id="1b933ab0"></span>
## Do historical messages that have already been consumed support backtracking?

Not supported.

Currently, after RabbitMQ successfully consumes a business message and the consumption is acknowledged (Ack), automatic message deletion is triggered. Historical messages that have already been consumed cannot be queried or retrieved, even if they are still within the message retention period.

<span id="ecbc8395"></span>
## Does the RabbitMQ MQTT protocol support second\-level topics?

Yes.

Message Queue for RabbitMQ is fully compatible with the MQTT protocol and supports second\-level and multi\-level topics. Additionally, you can consume messages by fuzzy matching the Topic.

<span id="fd156348"></span>
## You are able to consume MQTT protocol messages normally, but cannot query them through the Web UI's GetMessages?


* If the consumer is not online, there will be no queue, and messages cannot be queried.

* If the consumer is online but there are no messages accumulating, historical messages cannot be queried because they have already been cleared.


<span id="d0d1052b"></span>
## What are the effects of high disk usage rate and memory usage rate?

If the available disk space of a RabbitMQ instance or node is less than 2GiB, or if memory usage reaches 100%, the backend service prohibits data from being written to that instance or node. To prevent service interruptions caused by high disk or memory usage, it is recommended to set threshold monitoring alarms for disk capacity and memory usage. Address issues promptly when instance resource consumption is high. For the recommended alarm strategy, refer to [disk usage exceeding 85%](https://docs.byteplus.com/en/docs/rabbitmq/Recommended_alarm_rules#1c1f1b02).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For Cluster instances, in scenarios where data is unevenly distributed, there may be significant differences in disk usage rates across nodes, resulting in the storage space of nodes with lower disk usage rates not being effectively utilized. It is recommended to promptly adjust business logic to balance the data write volume among different nodes and avoid write skew.</div>


<span id=".5pSv5oyB55qEIFJhYmJpdE1RIOeJiOacrOWMheaLrOWTquS6m--8nw=="></span>
## Which RabbitMQ versions are supported?

Message Queue for RabbitMQ is compatible with open\-source RabbitMQ versions `3.8` and `3.12`.

<span id=".5piv5ZCm5pSv5oyB5aSa5Y-v55So5Yy66YOo572yIFJhYmJpdE1RIOWunuS-i--8nw=="></span>
## Does RabbitMQ support deploying instances across multiple availability zones?

Message Queue for RabbitMQ supports deployment of RabbitMQ instances across multiple availability zones, that is, it supports multiple AZs. Instances deployed across multiple available zones offer stronger disaster recovery capabilities, fully ensuring cluster data reliability and service availability.

When purchasing a RabbitMQ instance, set the Deploy method to the Multiple availability zone deployment option and select three availability zones to achieve cross\-AZ disaster recovery. After creating an instance, you cannot change its deploy method. For example, a single availability zone deployment instance cannot switch to multiple availability zone deployment.

For a purchased RabbitMQ instance, you can find the number of availability zones by going to the **Instance Details** tab and locating the **Basic Information** section, then checking the **availability zone** row. If the number of availability zones is greater than 1, the instance is deployed with multiple availability zones.

<span id="8d55a308"></span>
## Why is it not possible to delete a RabbitMQ instance?

When deleting an instance, you will often receive a prompt indicating that resources within the instance have not been cleaned up. Please go to the Web UI to delete them.

This is usually because there are resources such as Queues, Exchanges, Vhosts, and other resources within the instance. You need to delete these resources yourself before you can delete the RabbitMQ instance in the console.

<span id="50f64a6d"></span>
## When deleting Queues and Exchanges, `Access refused` is displayed.

Typically, users with non\-admin roles are responsible for producing and consuming messages; however, resource deletion in the Web UI is performed by admin users. Admin users often do not have a Vhost bound to send or receive messages.

At this point, when a user with the admin role deletes Queues and Exchanges, an `Access refused` message will be displayed. You need to bind the Vhost before you can delete these resources. For instructions, see [Binding users and Vhost](https://docs.byteplus.com/en/docs/rabbitmq/Bind_user_and_Vhost).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e839c1e326934daf90dfe7b142989396~tplv-goo7wpa0wc-image.image) </span>
