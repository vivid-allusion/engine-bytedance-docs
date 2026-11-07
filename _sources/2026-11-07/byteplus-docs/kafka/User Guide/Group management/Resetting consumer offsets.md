---
title: "Resetting consumer offsets"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Resetting-consume-offsets"
---

For scenarios like clearing accumulated messages or processing offline data, where consuming messages from a specific past period or clearing all accumulated messages is required, resetting the offset is an option. You can reset consumer offsets and change the current consumption positions of consumers in the Message Queue for Kafka console. This feature allows you to consume messages directly from a specified point in time, the latest offset, or a specified offset.

<span id="背景信息"></span>
## Background information

Message Queue for Kafka allows you to reset consumer offsets at the group, topic, or partition levels. The following three methods are supported for resetting.


* Based on the latest offset: Skip all accumulated messages and start to consume messages from the latest offset. Accumulated messages are not deleted because of the reset.

* Based on a specified point in time: Start to consume messages at a specific point in time selected from a specified past period. This period is determined by the message retention period specified for the topic.

* Based on a specified offset: Start to consume messages from a specified offset in the current partition. After the reset, consumers in the group start to consume messages from the specified offset in the current partition.


<span id="前提条件"></span>
## Before you begin


* Message Queue for Kafka does not support online resetting of consumer offsets. Before you reset them, stop all consumer clients in the consumer group, ensuring that the group status is Empty.

* After stopping consumer clients, a specified timeout period must elapse before the server deems the consumers genuinely offline. The timeout period is specified by `ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG`, which defaults to 10,000 ms.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Group Management** tab to display the group list of the instance.

5. Select an appropriate method to reset consumer offsets depending on the granularity.

   * Reset the consumer offset for all topics subscribed to by the current consumer group.

      1. On the upper\-left corner of the **Consumption status** pane, click **Reset Consumer Offset**.

      2. In the pop\-up dialog box, confirm the topics requiring consumer offset resetting and select a reset method. The following two reset methods are supported:

      
      |**Reset Method** |**Description** |
      |---|---|
      |According to the latest offset |Skip all accumulated messages, starting consumption from the latest offset. |
      |According to the time point |Start consumption from a specific past point in time, as determined by the message storage time of the topics.<br><br>For resetting based on a point in time, you can specify any past moment within the message retention period of the Kafka instance, but not future moments or past moments beyond the storage time. |
      

      3. Click **OK**.

   * Reset the consumer offset for a specific topic subscribed to by the current consumer group.

      4. In the **Consumption status** pane, locate the topic and click **Reset Consumer Offset** in the **Actions** column.

      5. In the pop\-up dialog box, confirm the topics requiring consumer offset resetting and select a reset method. The following two reset methods are supported:

      
      |**Reset Method** |**Description** |
      |---|---|
      |According to the latest offset |Skip all accumulated messages, starting consumption from the latest offset. |
      |According to the time point |Start consumption from a specific past point in time, as determined by the message storage time of the topics.<br><br>For resetting based on a point in time, you can specify any past moment within the message retention period of the current topic, but not future moments or past moments beyond the storage time. |
      

      3. Click **OK**.

   * Reset the consumer offset for a partition.

      1. Expand the collapsed menu for the topic where the partition is located and click **Reset Consumer Offset** in the **Actions** column of the partition.

      2. In the pop\-up dialog box, confirm the topics requiring consumer offset resetting and select a reset method. The following three reset methods are supported:

      
      |**Reset Method** |**Description** |
      |---|---|
      |According to the latest offset |Skip all accumulated messages, starting consumption from the latest offset. |
      |According to the time point |Start consumption from an offset corresponding to a specific past point in time, as determined by the message retention period of the topic.<br><br>For resetting based on a point in time, you can specify any past moment within the message retention period of the current topic, but not future moments or past moments beyond the storage time. |
      |Specify offset |Start consumption from a specified offset in the current partition. After the reset, consumers in the group start to consume messages from the specified offset in the current partition. |
      

      3. Click **OK**.
