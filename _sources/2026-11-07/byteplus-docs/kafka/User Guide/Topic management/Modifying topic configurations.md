---
title: "Modifying topic configurations"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/modifying-topic-configurations"
---

After creating a topic, you can modify the number of partitions and other topic configurations according to business traffic as needed, promptly expanding the capacity of the topic to handle business traffic.

<span id="前提条件"></span>
## Before you begin

Create a Message Queue for Kafka instance and a topic. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance) and [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic).

<span id="注意事项"></span>
## Precautions


* The number of partitions can only be increased, not decreased. Plan the number of partitions reasonably.

* The topic name cannot be modified.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Topic Management** tab.

5. Locate the target topic and click **Modify configuration** in the **Actions** column.

6. Configure the parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |No. of Partitions |The number of partitions in the topic. The larger the number of partitions, the higher the concurrency of message consumption.<br><br>The default value is 12, the value range is from 1 to 300, and it must not exceed the remaining available partition count of the corresponding Kafka instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When modifying the Topic configuration, this parameter only supports addition but not reduction.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partitions of a Topic will be randomly distributed and stored within the Kafka instance. To ensure that the partitions can be evenly distributed within the Kafka instance, it is recommended to set the number of Topic partitions to be an integer multiple of the number of Brokers in the corresponding Kafka instance.You can refer to <a href="https://docs.byteplus.com/docs/kafka/viewing-instance-details">Viewing instance details</a> to check the number of Brokers in the Kafka instance.</div><br> |
   |No. of replicas |The number of replicas for a partition. Data is backed up on the specified number of replicas to ensure high availability of the partition. The data availability can be guaranteed when a broker fails. The higher the number of replicas, the greater the data reliability.<br><br>The number of replicas can be set to 1, 2, or 3, with the default being 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Increasing the number of replicas consumes instance disk capacity, so make sure that enough capacity is available. Adding replicas consumes instance bandwidth resources, so we recommend that you perform this operation during off\-peak business hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Decreasing the number of replicas reduces data availability, so proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A topic with one replica cannot ensure data reliability, and does not support read and write operations during instance upgrades, so we recommend that you select two or three replicas.</div><br> |
   |Minimum number of synchronous replicas |The minimum number of in\-sync replicas for a topic, represented by the min.insync.replicas parameter. A larger value improves data reliability but reduces availability.<br><br><br>* When the number of replicas is 1, the minimum number of in\-sync replicas can only be 1.<br><br>* When the number of replicas is 2 or 3, the minimum number of in\-sync replicas cannot exceed the number of replicas minus 1. |
   |Message Retention Period |The maximum retention period of messages in the topic when disk capacity is sufficient. Consumers must consume messages before this time ends. Otherwise, messages are deleted. Deleted messages cannot be consumed.<br><br>The unit is hour and the value ranges from 0 through 2160. Currently, the maximum supported retention period is 90 days. By default, the message retention period applies to instances. You can also specify the message retention period for this topic here. The specified value only takes effect for this topic. |
   |Maximum Message Size |The maximum length of a single message in this topic.<br><br>The value ranges from 1 MB to 12 MB. By default, the maximum message size applies to instances. You can also specify the maximum message size for this topic here. The specified value only takes effect for this topic. |
   

7. In the pop\-up dialog box, confirm the risk warning and click OK.


<span id="4b5b5e46"></span>
## Related operations

If you modify Replicas when modifying topic configurations, the back\-end service automatically creates a background task with the task type **Change Topic Replicas** for monitoring the execution of the setting. You can view the task details on the **Background Task Management** tab. For more information, refer to [Managing background tasks](https://docs.byteplus.com/en/docs/kafka/managing-background-tasks).


* If the task status is **Implemented**, the task is successful and the number of replicas has been modified.

* If the task status is **Implemention failed**, the task failed. You can view the error and more in **Task details**.
