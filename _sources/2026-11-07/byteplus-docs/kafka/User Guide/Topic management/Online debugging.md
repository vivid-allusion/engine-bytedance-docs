---
title: "Online debugging"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/online-debugging"
---

Message Queue for Kafka allows online debugging of message delivery through the console. You can conduct tests on sending normal messages and use the message query feature to confirm their successful delivery. This topic describes how to send test messages online.

<span id="背景信息"></span>
## Background information

After creating a Kafka instance and a topic, you can perform simple online business debugging in the Message Queue for Kafka console to verify if message delivery works properly. Message Queue for Kafka has an online message sending feature. You can send custom test messages to a specified topic. You can also specify the message key and partition for post\-send message query and filtering. After sending a message, you can use the message query feature to verify if the message has been successfully sent to the Kafka instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The custom message content sent during online debugging is not actual business messages and may generate some dirty data, affecting the order of messages. We recommend that you use this feature only for test scenarios such as application access and consumption verification.</div>


<span id="前提条件"></span>
## Before you begin


* Create a Kafka instance. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance).

* Create a topic. For more information, refer to [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region.

3. On the **Instances** page, click the name of the instance.

4. On the **Topic Management** tab, locate the topic, and click **Send message** in the **Actions** column.

5. Specify the relevant settings for the message.

   
   |**Parameter** |**Description** |
   |---|---|
   |Message Key |The message key.<br><br>This parameter is optional. If you specify a message key when sending a message, you can query the message by message key after the message is sent. |
   |Message content |Custom message content. It must be 1 to 1,000 characters in length. |
   |Send to the specified partition |Whether to specify a topic partition when sending a message. Options are:<br><br><br>* **Yes**: During online debugging, the message is sent to a specified topic partition.<br><br>* **No**: During online debugging, the message is sent to a random topic partition. |
   |Partition ID |The partition ID of the topic. This parameter is only required when **Send to the specified partition** is set to **Yes**. This parameter specifies to which topic partition the message is sent during online debugging.<br><br>Value range: 0–11. You can view the partition list on the topic details page. For more information, refer to [Viewing topic details](https://docs.byteplus.com/en/docs/kafka/viewing-topic-details). |
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28a6a973794344de8f9e98a68a60dacc~tplv-goo7wpa0wc-image.image) </span>

6. Click **OK**.

   After the message is sent, the page displays the result of the message delivery. The topic name and partition ID corresponding to the message are also displayed. You can query the message by topic name, partition ID, and the time the message was sent.


<span id="后续操作"></span>
## What to do next

After sending a message, you can use the online message query feature to verify if the message has been successfully sent to the Kafka instance. Message offsets cannot be accessed in online debugging. Therefore, we recommend that you query the message by time the message was sent. For more information, refer to [Message query](https://docs.byteplus.com/en/docs/kafka/message-query).
