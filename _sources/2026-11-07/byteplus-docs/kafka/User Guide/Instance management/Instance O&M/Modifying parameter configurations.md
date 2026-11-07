---
title: "Modifying parameter configurations"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter"
---

After creating a Kafka instance, you can modify the parameter configurations at the instance or topic level as needed, such as maximum message size, message retention period, and more.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Message Queue for Kafka allows you to configure certain parameters at both the instance and topic levels. You can specify various message policies for different scenarios. For example, configure **Message retention period** to specify a message deletion policy upon expiration and **Automatically delete old messages** to specify a disk capacity threshold policy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instance\-level parameter configurations determine the default parameter values of the instance. This means that topics created after instance configuration modification use these default values. The actual effective <strong>Message retention period</strong> and other configurations are determined by the parameter configurations of each topic.</div>


<span id=".56OB55uY5a656YeP6ZiI5YC8562W55Wl"></span>
### Disk capacity threshold policy

After setting the message retention period, if the disk capacity of the instance is sufficient, expired messages are automatically deleted on schedule. However, if messages surge within a short period, the unexpired messages quickly fill up the disk space of a single broker or the entire instance, resulting in production and consumption issues. Message Queue for Kafka ensures service availability through threshold policy management when disk capacity is insufficient.

Kafka instances allow you to specify a disk cleanup threshold, and the disk cleanup threshold is the same for each broker. If the overall disk utilization of the instance reaches the cleanup threshold, or if the disk utilization of a specific broker reaches the cleanup threshold due to data skew, historical messages are deleted in the order they were stored on the Kafka instance, regardless of whether they exceed the message retention period. This process continues until the disk utilization becomes normal, preventing Kafka instance anomalies due to excessively high disk utilization and replica inconsistencies due to brokers being unable to sync data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When the automatic deletion policy is triggered, if the message write rate exceeds the speed of disk cleanup, the back\-end service pauses writing data before the disk is filled.</div>


* <div data-tips="true" data-tips-type="tip">We recommend that you set threshold monitoring alarms for broker disk capacity so that you can address the issue promptly before the disk utilization approaches the cleanup threshold, preventing messages from being deleted before natural aging. For more information on the recommended alarm strategies, refer to <a href="https://docs.byteplus.com/en/docs/kafka/recommended-alarm-rules">Instance disk utilization exceeds 30% and disk skew rate exceeds 30%</a>.</div>



<span id="d4d41e7e"></span>
### Message deletion policy upon expiration

Message Queue for Kafka manages message deletion policies upon expiration. You can configure the **Message retention period** parameter to specify the storage duration of messages on the Kafka instance when disk capacity is sufficient.

When disk capacity is sufficient, the Kafka instance periodically detects and automatically cleans up messages that exceed the retention period. However, each partition retains at least one currently used log file, so some messages are still retained even if they exceed the retention period. As a result, you may query messages that exceed the retention period.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Modifying instance parameter configurations do not affect the parameter configurations of existing topics. If a maximum message size and a message retention period are set for a topic, modifying these parameters at the instance level does not affect this topic.

* Modifying the consumer offset retention period of an instance triggers a rolling restart of the instance. Make sure that an automatic reconnection policy is configured on the business side.

* Before modifying the MessageMaxByte parameter, make sure that the new message size matches the configuration of the production and consumer clients. Otherwise, messages may be lost.


<span id=".5L-u5pS55a6e5L6L55qE55qE5Y-C5pWw6YWN572u"></span>
## Modifying instance parameter configurations

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before modifying the parameter configurations, ensure that the Kafka instance status is <strong>Running</strong>.</div>


The procedure is as follows:


1. Log in to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. On the **Instance Details** tab, click **Modify** in the **Parameter configuration** pane.

4. Specify the new configuration, and click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Maximum message size |The maximum size of a single message that can be sent and received by Message Queue for Kafka. The parameter configuration must match that of the producer and consumer clients to avoid message loss.<br><br>Unit: MB. Value range: 1–12. Default value: 10. |
   |Message retention period |The maximum retention period of messages when disk capacity is sufficient. Unit: hour. Value range: 1–2160, which means messages can be retained for a maximum of 90 days.<br><br>When the disk utilization reaches 90%, to ensure service availability, the back\-end service automatically deletes some historical messages. For more information, refer to **Disk capacity threshold policy**. |
   |Consumer offset retention period |The maximum retention period of a consumer offset. From when a consumer offset is committed, consumer offsets whose retention period exceeds the specified period are deleted. Each time a consumer offset is committed to a topic partition, the retention period of the consumer offset is reset to zero.<br><br>Unit: minute. Value range: 1–10080, which means consumer offsets can be retained for a maximum of 7 days. Default value: 4,320 minutes, equivalent to 3 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Changing the consumption point retention time of an instance will trigger a rolling restart of the instance, which may result in brief unavailability of the service. It is recommended that you implement a reconnection mechanism in the client to avoid disconnection and inability to reconnect.</div><br> |
   |Message time type |The type of the message timestamp. It defaults to CreateTime. The following options are supported:<br><br><br>* LogAppendTime: The time when a message is written to the Kafka instance is used as the message timestamp.<br><br>* CreateTime: The time when the producer creates the message, that is, the message timestamp of the CreateTime type passed in by the client. |
   |Automatically Delete Groups |Whether to automatically delete the group. The feature is disabled by default.<br><br><br>* After this feature is enabled, if all consumers in a consumer group are in the Empty state, the consumer group is automatically deleted after the consumer offset retention period expires.<br><br>* After this feature is disabled, the automatic deletion of data related to the message consumption progress does not affect the status of consumer groups, and the system does not automatically delete groups in the Empty state.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Changing the consumption point retention time of an instance will trigger a rolling restart of the instance, which may result in brief unavailability of the service. It is recommended that you implement a reconnection mechanism in the client to avoid disconnection and inability to reconnect.</div><br> |
   

5. In the pop\-up dialog box, confirm the new parameter name and the runtime values before and after the modification, then click **OK**.


<span id="1b9c235b"></span>
## Modifying topic parameter configurations

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Topic parameter configurations can only be modified when the Kafka instance status is <strong>Running</strong> and the topic status is <strong>In service</strong>.</div>


The procedure is as follows:


1. Log in to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Topic management** tab.

5. Locate the target topic and click **Modify configuration** in the **Actions** column.

6. Configure the parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |No. of Partitions |The number of partitions in the topic. The larger the number of partitions, the higher the concurrency of message consumption.<br><br>The default value is 12 and the value ranges from 1 through 300. The number of partitions must be an integer multiple of the number of brokers. For more information, refer to [Viewing node information](https://docs.byteplus.com/en/docs/kafka/viewing-broker-information) to view the number of brokers for the current instance.<br><br>The number of partitions can only be increased and must not exceed the remaining available partitions of the Kafka instance. |
   |No. of replicas |The number of replicas for a partition. Data is backed up on the specified number of replicas to ensure high availability of the partition. The data availability can be guaranteed when a broker fails. The higher the number of replicas, the greater the data reliability.<br><br>The number of replicas can be set to 1, 2, or 3, with the default being 3.<br><br>Increasing the number of replicas consumes instance disk capacity, so make sure that enough capacity is available. Adding replicas consumes instance bandwidth resources, so we recommend that you perform this operation during off\-peak business hours.<br><br>Decreasing the number of replicas reduces data availability, so proceed with caution.<br><br>A topic with one replica cannot ensure data reliability, and does not support read and write operations during instance upgrades, so we recommend that you select two or three replicas. |
   |Minimum number of synchronous replicas |The minimum number of in\-sync replicas for a topic, represented by the min.insync.replicas parameter. A larger value improves data reliability but reduces availability.<br><br>When the number of replicas is 1, the minimum number of in\-sync replicas can only be 1.<br><br>When the number of replicas is 2 or 3, the minimum number of in\-sync replicas cannot exceed the number of replicas minus 1. |
   |Message retention period |The maximum retention period of messages in the topic when disk capacity is sufficient. Consumers must consume messages before this time ends. Otherwise, messages are deleted. Deleted messages cannot be consumed.<br><br>The unit is hour and the value ranges from 0 through 2160. Currently, the maximum supported retention period is 90 days. By default, the message retention period applies to instances. You can also specify the message retention period for this topic here. The specified value only takes effect for this topic. |
   |Maximum message size |The maximum length of a single message in this topic.<br><br>The value ranges from 1 MB to 12 MB. By default, the maximum message size applies to instances. You can also specify the maximum message size for this topic here. The specified value only takes effect for this topic. |
   

7. Click **OK**.
