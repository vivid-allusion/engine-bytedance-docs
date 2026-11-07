---
title: "Creating a topic"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/creating-topic"
---

Topic is a collection of messages of the same type and is the basic unit of data writing operation in Message Queue for Kafka. This topic describes how to create a topic.

<span id="331e9e70"></span>
# Background information

In practical use cases, a topic often carries the same type of business traffic. Developers decide how to design different topics based on their system and architecture design. Every topic has multiple producers sending messages to it and multiple consumers consuming messages from it.

Partitions are physical components of a topic. A topic can be divided into multiple partitions, with each partition being an ordered queue. When creating a topic, specify the number of partitions. As business traffic grows, you can also add partitions at any time to improve the capacity of the instance to carry business traffic.

In Message Queue for Kafka, the supported topic creation methods for Kafka instances are controlled by the automatic topic creation feature. This feature is disabled by default.


* If the feature is disabled, you can only create topics in the console.

* If the feature is enabled, you can not only create topics in the console but also specify a non\-existent topic to which data is written when producing messages. In this case, the Kafka back\-end service automatically creates the specified topic for you.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instances of each instance type have a certain range of partition quotas and free partitions. Once free partitions are exhausted, buy additional partitions before you can continue to create topics or expand partitions. If the number of partitions reaches the maximum quota supported by the instance type, you must adjust the partition specification or get a larger partition quota to continue to create topics or expand partitions.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
# Prerequisites

Create a Message Queue for Kafka instance and ensure that the instance status is **Running**. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Manually creating a topic

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once a topic is created, its name cannot be modified, and the number of partitions can only be increased, not decreased. Make sure to provision partitions carefully when creating or modifying a topic.</div>


<div data-tips="true" data-tips-type="tip">In scenarios like application migration to the cloud or instance backups, if you want to create multiple topics at once, you can batch create topics by uploading a configuration file. For more information, refer to <a href="https://docs.byteplus.com/en/docs/kafka/batch-importing-SASLusers">Batch importing SASL users</a>.</div>



1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Topic management** tab.

5. Click **Create Topic**.

6. Specify the basic information of the topic.

   
   |**Parameter** |**Description** |
   |---|---|
   |Topic name |The name of a topic. It must meet the following requirements:<br><br><br>* Must be 3 to 64 characters in length.<br><br>* Must start with a letter or a digit.<br><br>* Can only contain letters, digits, hyphens ( \- ), underscores ( _ ), and periods (. ).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Once created, the topic name cannot be modified.</div><br> |
   |Description |Description of the topic. Describe its purpose, and business type, among other information. |
   

7. Configure the topic parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |No. of partitions |The number of partitions in the topic. The larger the number of partitions, the higher the concurrency of message consumption.<br><br>The default value is 12, the value range is from 1 to 300, and it must not exceed the remaining available partition count of the corresponding Kafka instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When modifying the Topic configuration, this parameter only supports addition but not reduction.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The partitions of a Topic will be randomly distributed and stored within the Kafka instance. To ensure that the partitions can be evenly distributed within the Kafka instance, it is recommended to set the number of Topic partitions to be an integer multiple of the number of Brokers in the corresponding Kafka instance.You can refer to <a href="https://docs.byteplus.com/docs/kafka/viewing-instance-details">Viewing instance details</a> to check the number of Brokers in the Kafka instance.</div><br> |
   |No. of replicas |The number of replicas for a partition. Data is backed up on the specified number of replicas to ensure high availability of the partition. The data availability can be guaranteed when a broker fails. The higher the number of replicas, the greater the data reliability.<br><br>The number of replicas can be set to 1, 2, or 3, with the default being 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Increasing the number of replicas consumes instance disk capacity, so make sure that enough capacity is available. Adding replicas consumes instance bandwidth resources, so we recommend that you perform this operation during off\-peak business hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Decreasing the number of replicas reduces data availability, so proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A topic with one replica cannot ensure data reliability, and does not support read and write operations during instance upgrades, so we recommend that you select two or three replicas.</div><br> |
   |Minimum number of synchronous replicas |The minimum number of in\-sync replicas for a topic, represented by the min.insync.replicas parameter. A larger value improves data reliability but reduces availability.<br><br><br>* When the number of replicas is 1, the minimum number of in\-sync replicas can only be 1.<br><br>* When the number of replicas is 2 or 3, the minimum number of in\-sync replicas cannot exceed the number of replicas minus 1. |
   |Message Retention Period |The maximum retention period of messages in the topic when disk capacity is sufficient. Consumers must consume messages before this time ends. Otherwise, messages are deleted. Deleted messages cannot be consumed.<br><br>The unit is hour and the value ranges from 0 through 2160. Currently, the maximum supported retention period is 90 days. By default, the message retention period applies to instances. You can also specify the message retention period for this topic here. The specified value only takes effect for this topic. |
   |Maximum Message Size |The maximum length of a single message in this topic.<br><br>The value ranges from 1 MB to 12 MB. By default, the maximum message size applies to instances. You can also specify the maximum message size for this topic here. The specified value only takes effect for this topic. |
   

8. Configure user permissions.

   Specify permissions on this topic for Simple Authentication and Security Layer (SASL) users in the instance.

   The default value is **All allowed**, meaning all SASL users have read and write permissions on this topic, even if the **All Permitted** permission is disabled. You can also choose custom settings to specify permission types for different SASL users. Custom permissions are:

   * Read\-only: only allows message subscription.

   * Write\-only: only allows message production.

   * Read\-write: allows message production and subscription.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Custom settings only take effect for SASL users who have disabled <strong>All Permitted</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you set custom permissions when creating a topic, Message Queue for Kafka automatically creates an ACL in the list. If you want to modify custom permissions after creating a topic, we recommend that you modify them through ACLs. For more information, refer to <a href="https://docs.byteplus.com/en/docs/kafka/creating-an-ACL">Creating an access control list</a>.   </div>
   

9. (optional) Configure Topic Tags.

   Click **Add tag**, enter the tag key and tag value, and add custom tags to the Topic.

   Tags are used to identify and classify cloud resources. Adding tags is beneficial for identifying and managing topics. Up to 20 tags can be added each time.

10. Click **Create**.

   You can view the topic you created on the **Topic Management** tab.


<span id="4a9a1570"></span>
## Automatically creating a topic

Enable the automatic topic creation feature in the console before you use it. Meanwhile, specify a non\-existent topic in the client SDK when writing messages. Default configurations for automatically created topics are as follows:


|**Parameter** |**Default Configuration** |
|---|---|
|Topic name |The topic name specified in the client SDK. It must meet the following requirements:<br><br><br>* Must be 3 to 64 characters in length.<br><br>* Must start with a letter or a digit.<br><br>* Can only contain letters, digits, hyphens ( \- ), underscores ( _ ), and periods (. ).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">It cannot start with <code>__</code>, otherwise automatic topic creation fails.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Including non\-compliant characters in the topic name leads to issues like failure to collect topic monitoring data.</div><br> |
|Description |None. |
|No. of partitions |Default number of partitions set when enabling the automatic topic creation feature. |
|No. of replicas |Default number of replicas set when enabling the automatic topic creation feature. |
|Minimum number of synchronous replicas |Defaults to 1. |
|Message retention period |Defaults to the message retention period of the instance. |
|Maximum message size |Defaults to the maximum message size of the instance. |
|User permissions |By default, the topic has no custom permissions. If ACL is enabled, only SASL users with the All Permitted permission have read and write access to the topic. |
|Tag |By default, this topic has no custom labels. |
|Message clearing strategy |For automatically created Topics, the message clearing strategy is DELETE by default. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">We recommend that you enable the automatic topic creation feature only for testing or data migration purposes. For production environments, especially those where performance and stability are critical, we recommend that you disable the feature.</div>


* <div data-tips="true" data-tips-type="tip">Automatic topic creation takes longer than manual topic creation, and the automatically created topics do not appear in the topic list until 2 minutes after creation.</div>


* <div data-tips="true" data-tips-type="tip">When modifying instance specifications, do not create topics through any method. Before creating a topic with the client, make sure the instance status is <strong>Running</strong>.</div>



<span id="6bcef29a"></span>
### Enabling the automatic topic creation feature


1. Log into [BytePlus Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Project and Region where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the **Topic management** tab, click **Set up automatic topic creation**.

5. Toggle the **Automatically create Topics** switch to enable the feature, and configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |ACL user automatic authorization |Whether to allow all ACL users to automatically create Topics.<br><br><br>* The switch is turned on by default, allowing all ACL users to automatically create topics. In this case, permissions to create and delete Topics for all users are created in the ACL management tab.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter switch is correlated with topic creation permission for all users. When topic creation permission for all users is removed, then the switch is turned off accordingly; when topic creation permission for all users is enabled, then the switch is turned on.</div><br><br><br><br>* When the switch is turned off, all ACL users cannot automatically create topics. You can then configure topic management permissions for the target user in the ACL management tab as needed. For more information, please see [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you actively disable this switch, all users' permissions to create and delete topics will not be removed. Please delete the create and delete permissions for all users in the <strong>ACL Management</strong> tab as needed. For more information, please see <a href="https://docs.byteplus.com/en/docs/kafka/deleting-an-ACL">Deleting an access control list</a>.</div><br> |
   |Default number of partitions |The default number of partitions for the automatically created topic.<br><br>The value ranges from 1 to 300 and cannot exceed the number of remaining partitions available in the instance. |
   |Default number of replicas |The default number of partition replicas for the automatically created topic.<br><br>The value can be set to 1, 2, or 3 replicas. |
   

6. In the pop\-up dialog box, click **Create**.


<span id="aaea49c3"></span>
### Automatically creating a topic with the Kafka client SDK

After enabling the automatic topic creation feature, you can specify a non\-existent topic name in the producer client SDK, requesting to write messages to the topic. Message Queue for Kafka automatically creates the specified topic in the corresponding instance upon receiving the request.

You can follow the sample Java code below to set the topic to which messages are written in the Kafka client SDK for producer instances.

```Java
    ......
    // Specify a non-existent topic name. The back-end service automatically creates the specified topic upon receiving the request.
    private void setTopic(Properties kafkaProperties) {
        topic  = kafkaProperties.getProperty("topic");
    }
    ......
```


<span id=".55u45YWz5pON5L2c"></span>
# Related operations

After creating a topic, you can modify its configurations and user permissions as needed or view detailed topic information.


* Modifying topic configurations

   You can modify the number of topic partitions and replicas, the minimum number of in\-sync replicas, message retention period, and maximum message size. For more information, refer to [Modifying topic configurations](https://docs.byteplus.com/en/docs/kafka/modifying-topic-configurations).

* Managing Topic tags

   You can filter topics by tags, bind and unbind tags in a batch. For more information, refer to [Managing topic tags](https://docs.byteplus.com/en/docs/kafka/topic-tags).

* Modifying user permissions

   You can configure permissions on the topic for SASL users through ACLs. For more information, refer to [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL).

* Viewing topic and partition details

   You can view the status, number of partitions, and more about the topic. For more information, refer to [Viewing topic details](https://docs.byteplus.com/en/docs/kafka/viewing-topic-details).

* Exporting a list of topics

   You can export a topic list from the console, including topic names and number of replicas. For more information, refer to [Exporting a list of topics](https://docs.byteplus.com/en/docs/kafka/exporting-topics).

* Deleting a topic

   We recommend that you delete a topic when it is no longer in use to save resources. For more information, refer to [Deleting a topic](https://docs.byteplus.com/en/docs/kafka/deleting-topic).
