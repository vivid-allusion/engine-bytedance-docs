---
title: "Deleting a topic"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/deleting-topic"
---

We recommend that you delete a topic when it is no longer in use to save resources.

<span id="前提条件"></span>
## Prerequisites

Message Queue for Kafka instance and topic have been created.

<span id="注意事项"></span>
## Precautions

After the topic is deleted:


* Related producer and consumer services immediately terminate.

* The metadata and message data in the topic are automatically cleared, including the accumulated unconsumed messages, and data cannot be restored. Please exercise caution when performing this operation.


<span id="操作步骤"></span>
## Procedure


1. Log into [BytePlus Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Project and Region where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. Click the **Topic management** tab.

5. Delete one topic or multiple topics as needed.

   1. Delete one topic

      Find the desired topic and click **Delete** in the **Actions** column.

   2. Delete multiple topics in a batch

      Select the desired topics and click **Batch deletion** in the lower\-left corner of the page.

6. In the pop\-up dialog box, click **Delete**.
