---
title: "Message query"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/message-query"
---

After integrating with Message Queue for Kafka, if message consumption issues occur, you can use the message query feature to view detailed message content of Kafka instances. This helps you verify whether the message details of Kafka instances align with those of producer or consumer clients and troubleshoot production or consumption issues.

<span id="背景信息"></span>
## Background information

Message Queue for Kafka offers the following methods for querying message details:


* Query by offset: queries messages at a specified offset in a specific partition and topic, suitable for scenarios where the ID of the partition messages are sent to and the message offset are exact.

* Query by time: queries the list of messages within a specific time range in a specific topic, specified partition, or all partitions. Querying by time range filters out a list messages that meet the criteria, suitable for scenarios where the time period for message sending is exact.


We recommend that you use the message query feature in the following scenarios:


* View the specific content of messages to verify if it is consistent with that of the producer or consumer client.

* Download specific message content for further troubleshooting.


<span id="注意事项"></span>
## Precautions


* The storage time of messages in Message Queue for Kafka is specified by the **Message Retention Period** parameter. Messages stored longer than the specified storage time are regularly deleted by the system. As a result, when you view message content, expired messages may be deleted. The message expiration deletion policy can be altered by modifying the **Message Retention Period** parameter. For more information, refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).

* In case of insufficient storage space, the back\-end service deletes historical messages, so some messages may be deleted and cannot be queried.

* For each query, the page displays up to 16 results, and the total size of the message content cannot exceed 10 MiB. If the size of a single message body is large, for example, the total size of 10 messages does not exceed the limit but 11 messages would, then only the first 10 results are returned. You can click **Click to load more** to view more results. For large data volumes, we recommend that you narrow the time range and conduct batch queries.

* The console displays at most 1 KiB of content for each retrieved message, with portions exceeding 1 KiB automatically truncated. To view full message content, download the message for local viewing.


<span id="前提条件"></span>
## Before you begin

Deploy a service on the producer client and integrate it with Message Queue for Kafka.

<span id="按位点查询消息"></span>
## Querying messages by offset


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. In the top menu bar, click **Message Query**.

5. Choose **Check by offset** and specify **Topic**, **Partition**, and **Offset** for messages you want to query.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Upon setting the <strong>Topic</strong> and partition, the page prompts for an optional range of starting offsets. Set a starting offset within the specified range. Otherwise, no messages are queried.   </div>
   

6. Click **query**.

   The page displays messages that meet the filtering conditions, including the topic name, partition, offset, key, value, message size, and storage time.

   
   |**Item** |**Description** |
   |---|---|
   |Topic name |The topic where the message was sent. |
   |Partition |The topic partition corresponding to the message. |
   |Offsets |The offset of the message. |
   |Key |The key of the message. If a key is not specified during message sending, it is displayed as "\-". The key is forcibly converted into a string for display on the page. |
   |Value |The message body, which is the specific content of the message. For easier viewing, the message content is forcibly converted into a string on the page.<br><br>The console displays at most 1 KiB of content for each retrieved message, with portions exceeding 1 KiB automatically truncated. To view full message content, download the message and decode it for review. |
   |Value message size |The length of the message body, measured in bytes. |
   |Storage time |The storage time of the message, as specified by the `timestamp` in `ProducerRecord`. |
   


<span id="按时间查询消息"></span>
## Querying messages by time


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. In the top menu bar, click **Message Query**.

5. Choose **Query by time** and specify the topic and partition of messages you want to query and the time range during which the messages are stored.

6. Click **query**.

   The page displays messages that meet the filtering conditions, including the topic name, partition, offset, key, value, message size, and storage time.

   
   |**Item** |**Description** |
   |---|---|
   |Topic name |The topic where the message was sent. |
   |Partition |The topic partition corresponding to the message. The option **All** is supported, allowing for querying messages in all partitions. |
   |Offsets |The offset of the message. |
   |Key |The key of the message. If a key is not specified during message sending, it is displayed as "\-". The message content is forcibly converted into a string. |
   |Value |The message body, which is the specific content of the message. The message content is forcibly converted into a string.<br><br>The console displays at most 1 KiB of content for each retrieved message, with portions exceeding 1 KiB automatically truncated. To view full message content, download the message and decode it for review. |
   |Value message size |The length of the message body, measured in bytes. |
   |Storage time |The storage time of the message, as specified by the `timestamp` in `ProducerRecord`. |
   


<span id="下载消息"></span>
## Downloading messages

Upon locating the specified message, you can download its specific content on the message query tab and compare it with the message content on the producer or consumer client, facilitating the troubleshooting of production and consumption issues.

Batch downloading messages is not supported.


1. Query messages by either offset or time.

2. In the query results, locate the message and click **Download message** in the **Actions** column.

   A `.txt` format file containing the full message content is automatically downloaded.
