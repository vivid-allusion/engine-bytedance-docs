---
title: "Message query"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/message-query-FAQ"
---

This topic provides answers to frequently asked questions (FAQs) related to message queries in Message Queue for Kafka.

<span id="bf65538f"></span>
## Why am I unable to query messages?

When you query messages in the Message Queue for Kafka console, you may fail to query messages even if the messages have been sent. In general, this issue is caused by the following reasons.


|Cause |Description |
|---|---|
|The messages have been deleted due to expiration. |You can set the message retention period for topics in a Kafka instance. Messages whose retention period has expired are automatically deleted. |
|The automatic message deletion feature is enabled, and the disk utilization is high. |If the automatic message deletion feature is enabled for your instance and the disk storage usage reaches the disk cleanup level, the back\-end service automatically deletes historical messages to release disk space. This ensures instance availability. In this case, messages that are not expired may be automatically deleted. As a result, you are unable to query these messages. |
|An incorrect timestamp has been set for a message. |When you query a message by time range, Message Queue for Kafka determines the time of the message according to its timestamp. The message timestamp (CreateTime) property is set by the client. If an incorrect timestamp has been set when a message is sent, you may fail to query the message. The following are some common scenarios:<br><br>An incorrect timestamp has been set so that the message cannot be queried. For example, the message timestamp is set to 0 or \-1.<br><br>The timestamp has been set to a point in time in the past. As a result, you cannot query the message corresponding to the incorrect timestamp and several messages before and after that message.<br><br>The timestamp has been set to a point in time in the future. As a result, you cannot query messages from the current time to the set future time even if the timestamp is correct. |


<span id="49560aa9"></span>
## Why can I query messages even though their retention period has expired?

The specified message retention period has ended for the messages in a topic of a Kafka instance, but you can still query these messages. This indicates that the messages have not been deleted yet.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Message Retention Period</strong> specifies the maximum retention period of a message when the disk capacity is sufficient. The default value is 72 hours, and the value of this parameter ranges from 1 hour to 2,160 hours. If the disk capacity is insufficient, the broker determines whether to delete historical messages before expiration according to the setting of the <strong>Whether to delete old messages</strong> parameter to ensure service availability.</div>


* <div data-tips="true" data-tips-type="tip">To avoid storage fragmentation in topics, each partition in a topic consists of multiple segment files of a specified size. Messages are stored in each segment file. By default, each segment file can be up to 1 GB in size. When the messages stored in a segment file exceed 1 GB in size, the back\-end service creates a new segment file for storing new messages. In addition, Kafka requires at least one segment file for storing messages.</div>



This issue is caused by the following reasons:


* When the Kafka broker automatically deletes historical messages according to the message retention period, messages are deleted by segment file. However, segment files smaller than 1 GB in size are retained. If the size of a segment file is less than 1 GB, neither the file nor its stored messages are deleted, regardless of whether the message retention period has expired.

* The segment file contains unexpired messages, that is, the message retention period has not ended for the message that corresponds to the largest timestamp in the segment file. In this case, the Kafka broker does not delete the segment file and its messages.

* The message timestamp (CreateTime) passed in when the client wrote a message is invalid, which affects the deletion of data on the broker. For example, a topic stores a message whose CreateTime is set to a specific point in time one year from now. As a result, the broker does not delete this message due to aging after the specified message retention period expires. Other messages in the same segment file as this message are also not deleted due to aging.


<span id="c8310056"></span>
## Why are messages that have been consumed still stored in a topic?

The deletion time of messages is independent of whether the messages have been consumed or not. When the disk capacity is sufficient, the back\-end service determines and deletes aged messages only if the set message retention period expires.

We recommend that you set a reasonable message retention period and instance storage space based on your business traffic. This prevents an excessive number of unaged messages from occupying a lot of disk space. For more information on how to set the message retention period, refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).
