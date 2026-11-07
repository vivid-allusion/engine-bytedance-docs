---
title: "Viewing consumption status in a group"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Viewing-consumption-status"
---

After a group is created and consumption begins, you can view all consumer group information for the specified instance in the Message Queue for Kafka console, including subscribed topics, message accumulation, and the status of the consumer group.

<span id="前提条件"></span>
## Before you begin

Create a group. For more information, refer to [Creating a group](https://docs.byteplus.com/en/docs/kafka/creating-group).

<span id="操作步骤"></span>
## Procedure


1. on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Group Management** tab to display the group list of the instance.

   On the upper\-right corner of the tab, you can search for a group from numerous groups by group ID, and view the status of the specified group. Fuzzy search is supported.

5. Click a group ID to view the consumption status of the specified group.

   The group details page displays the consumption status of the group, including the **Overview Statistics** and **Consumption status** panes.

   * **Overview Statistics**: displays the number of topics subscribed by the current group, message accumulation, and the ID and status of the current group.

      
      |Category |Item |Description |
      |---|---|---|
      |Overview Statistics |Subscribe to Topics |The number of topics to which the current group is subscribed. |
      ||Kafka consumergroup lag |The number of unconsumed messages accumulated in the current group. The value 0 indicates no message accumulation. |
      |Group information |Group ID |The group ID. |
      ||State |The group status. For more information, refer to [Viewing consumption status in a group](https://docs.byteplus.com/en/docs/kafka/Viewing-consumption-status).<br><br><br>* PreparingRebalance: The consumer group is reassigning partitions.<br><br>* CompletingRebalance: The consumer group completes partition rebalance calculations.<br><br>* Stable: After the assignment results are synchronized to all consumers, the consumer group enters this state and starts consumption.<br><br>* Empty: No consumers are consuming messages in the consumer group. |
      ||Describe |A brief description of the group. |
      

   * **Consumption status**: displays the consumption status of the current group, including each subscribed topic and the number of unconsumed messages. You can also expand the collapsible list of the topic to view the offset consumption details for each partition of the topic.

      
      |**Category** |**Item** |**Description** |
      |---|---|---|
      |Topic level |Topic |The name of the topic to which the current group is subscribed. |
      ||No. of unconsumed messages |The number of unconsumed messages accumulated in this topic. |
      |Partition level |Partition number |The partition number in this topic. |
      ||No. of unconsumed messages |The number of unconsumed messages accumulated in this partition. |
      ||Submit offset position |The position of the consumed message committed in this partition. |
      ||Minimum offset position |The position of the earliest message in this partition. |
      ||Maximum offset position |The position for writing the next message in this partition. The message accumulation in a partition is the maximum offset position minus the committed offset position. |
      ||Consumer Information |The IP address and port number of the consumer client corresponding to this partition. |
      


<span id="Group状态说明"></span>
## Group status description

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use built\-in subscription and consumption management feature of Kafka, group states include PreparingRebalance, CompletingRebalance, Stable, and Empty. Third\-party open\-source components, such as Logstash, implement their own consumption management logic. For such clients, only the Empty state is available, and normal consumption occurs in the Empty state.</div>



|**Status** |**Description** |
|---|---|
|PreparingRebalance |The consumer group is undergoing partition reassignment, which calculates partitions each consumer must consume. Typically, joining or exiting a consumer group triggers this status.<br><br>This is a temporary status, existing only for a brief period under normal conditions. A prolonged existence of this status suggests the likelihood of abnormal consumers who continuously exit and join the consumer group.<br><br>Consumer groups in this status cannot engage in normal consumption. |
|CompletingRebalance |The consumer group completes the computing for partition reassignment and waits for all assignment results to be synchronized to consumers.<br><br>This is a temporary status, similar to PreparingRebalance, and consumer groups should not stay in this status for an extended period.<br><br>Consumer groups in this status cannot engage in normal consumption. |
|Stable |After the assignment results are synchronized to all consumers, the consumer group enters this state and starts consumption.<br><br>Consumer groups in this status can conduct normal consumption. |
|Empty |No consumers are consuming messages in the consumer group.<br><br>Consumer groups in this status may possess valid consumption progress, which is automatically cleared by the back\-end service upon expiration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Message Queue for Kafka supports the automatic group deletion (<strong>auto.delete.group</strong>) feature. You can specify whether to allow the back\-end service to automatically delete consumer groups that are in the Empty state. For more information, refer to <a href="https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter">Modifying parameter configurations</a>.</div><br> |
