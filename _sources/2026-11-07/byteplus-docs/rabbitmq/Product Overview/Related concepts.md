---
title: "Related concepts"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Related_concepts"
---

BytePlus uses RabbitMQ as its messaging engine. RabbitMQ is a producer\-consumer model that primarily handles reception, storage, and forwarding of messages. The following concepts are described based on RabbitMQ.

<span id="消息 （Message）"></span>
### Message

Messages generally consist of two parts: the message body and tags. Tags are mainly used to describe the message. The message body is the content of the message, typically in the form of a JSON body or data. Producers send messages and consumers consume messages. There is no direct contact between producers and consumers.

<span id="生产者（Producer）"></span>
### Producer

The party that sends messages to the queue. The ultimate goal of publishing a message is to deliver the content to other systems or modules, so that they can process the message according to the agreement.

<span id="消费者（Consumer）"></span>
### Consumer

The party that receives messages from the queue. The consumer subscribes to a RabbitMQ queue. When consumers consume a message, only the message body is consumed. In the process of message routing, tags are discarded. Only the message body is stored in the queue.

<span id="队列（Queue）"></span>
### Queue

Queue is used to store messages. Producers send messages to the queue and consumers retrieve and consume messages from it. Multiple consumers can subscribe to the same queue simultaneously, and messages in the queue are distributed to different consumers.

<span id="b36e4e07"></span>
### Virtual host

A Virtual Host provides the capability for logical isolation of resources. It allows users to create multiple independent messaging broker environments on the RabbitMQ server. Each vhost has its own Queue, Exchange, Binding, and permissions restrictions, enabling different applications or services to communicate in mutually isolated environments. Every RabbitMQ server has a default vhost, namely "/".

<span id="代理（Broker）"></span>
### Broker

Service node of message middleware

<span id="交换器（Exchange）"></span>
### Exchange

Also known as a router, it is responsible for routing the producer's messages to the corresponding Queue component. Exchange routes messages based on Binding Key, Routing Key, and Exchange Type properties.

<span id="绑定（Binding）"></span>
### Binding

Associates the Exchange component with the Queue component.

<span id="Binding Key"></span>
### Binding key

Through Binding Key, the Queue component is bound to the Exchange component. When a message's Routing Key matches the Binding Key, the message will be routed to the Queue component associated with that Binding Key. Multiple Queues can be bound to the same Exchange using the same Binding Key.

<span id="Routing Key"></span>
### Routing key

Messages sent to the Exchange by producers generally carry a Routing Key, which specifies the routing rules for that message. With a fixed Exchange Type and binding key, producers can specify where the message is directed by specifying a Routing Key.

<span id="Exchange Type"></span>
### Exchange type

Common types include Direct Exchange, Topic Exchange, and Fanout Exchange.


* Direct Exchange: The Exchange routes messages based on exact match rules from the Binding Key and Routing Key.

* Topic Exchange: The Exchange routes messages based on wildcard matching rules between the Binding Key and Routing Key.

* Fanout Exchange: The Exchange ignores the matching rules of Routing Key and Binding Key, routing messages to all Queues it is bound to.


<span id="连接（Connection）"></span>
### Connection

The physical TCP connection between producer or consumer application systems and the message queue for RabbitMQ.

<span id="通道（Channel）"></span>
### Channel

Channel is a virtual connection established within the physical TCP connection. After the producer or consumer client establishes a connection with the message queue for RabbitMQ, all AMQP commands (such as producing or consuming messages, creating, or subscribing to queues, etc.) are completed through the Channel within the Connection. Multiple Channels can be established simultaneously in one TCP connection to achieve multiplexing of the TCP connection.

<span id="4u3AkgaI"></span>
### AMQP protocol

Advanced Message Queuing Protocol, an application layer standard protocol that provides a unified messaging service, designed for message\-oriented middleware. AMQP defines a set of functional semantics of network protocols and message broker services. It ensures full functional interoperability between different client applications and message middleware.

<span id="rqaDi55i"></span>
### MQTT protocol

Message Queue Telemetry Transport Protocol, a message publishing/subscription transport protocol based on client\-server. It operates over the TCP/IP protocol. It is a protocol designed for remote devices with poor hardware performance and network conditions.

<span id="AhQXPHAu"></span>
### SASL

It is a mechanism that provides developers of applications and shared libraries with tools for authentication, data integrity checks, and encryption.
