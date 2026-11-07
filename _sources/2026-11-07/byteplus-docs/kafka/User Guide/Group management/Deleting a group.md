---
title: "Deleting a group"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/deleting-group"
---

If a consumer group is no longer needed, you can manually delete the consumer group in the Empty state through the console or an open API. This topic describes how to delete a group in the console.

<span id="bd87fe9e"></span>
## Background information

Once all consumers in a group complete consumption and the consumer offset expires, the group automatically enters the Dead state. Message Queue for Kafka supports the automatic group deletion feature. Once enabled, groups in the Dead state are automatically deleted during the data reclaiming process. For more information, please see [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter). If the automatic group deletion feature is disabled, you can also manually delete groups in the Empty state through the console or an open API.

<span id="前提条件"></span>
## Prerequisites

Before deleting a group, make sure that no consumption is in progress and the group status is Empty.

<span id="注意事项"></span>
## Precautions


* If valid consumption progress still exists in a group, deleting the group also synchronously removes the corresponding consumer offsets.

* Deleting a group on the Kafka instance does not cancel subscriptions to a topic. To cancel a group's subscription to a specific topic, you need to delete the relevant code in the client side.


<span id="操作步骤"></span>
## Procedure


1. Log into [BytePlus Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Project and Region where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. Click the **Group management** tab to display the group list of the instance.

5. Delete one group or multiple groups as needed.

   1. Delete one group

      Find the desired group and click **Delete** in the **Actions** column.

   2. Delete multiple groups in a batch

      Select the desired groups and click **Delete** in the lower\-left corner of the page.

6. In the pop\-up dialog box, confirm the group you want to delete, and then click **Delete**.
