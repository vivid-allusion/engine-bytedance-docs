---
title: "Message production and consumption"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/message-production-consumption-faq"
---

This topic provides answers to frequently asked questions (FAQs) related to message production and consumption in Message Queue for Kafka.

<span id="87880676"></span>
## Are delayed messages supported by Kafka instances?

No, Message Queue for Kafka does not support delayed messages.

<span id="31858b2f"></span>
## How do I view the IP addresses from which messages are being consumed?

To view the client IP addresses from which messages are being consumed:


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Group Management** tab to display the group list of the instance.

5. Click a group ID to view the consumption status of the specified group.


In the **Consumption status** area, expand the topic, then view the client IP addresses in the **Consumer Information** column.

If the **Consumer Information** column is empty, no clients are consuming messages in the partition, or the consumers are using third\-party Kafka clients.

<span id="a34a6dc0"></span>
## How can I determine whether a message has been sent successfully?

After a client sends a message to a Kafka instance, you can determine whether the message has been sent successfully using the following methods.


|Method |Description |
|---|---|
|Querying messages |Query messages by consumer offset or time on the **Message Query** page of the Message Queue for Kafka console. If the message can be queried, the message has been sent successfully. |
|Viewing the number of messages stored in the topic |On the **Topic Management** page of the Message Queue for Kafka console, click the name of the target topic to view the number of messages in the **No. of stored messages** column. If the number of messages stored is consistent with the number of messages sent, the message has been sent successfully. |
|Viewing the callback |In most cases, Kafka clients return a Callback or Future after a message is sent. If a Callback is received, the message has been sent successfully. |


<span id="0be37e15"></span>
## How many connections to a broker can a producer establish?

In most cases, each producer establishes two TCP connections to a broker, including one for updating metadata and one for sending messages.
