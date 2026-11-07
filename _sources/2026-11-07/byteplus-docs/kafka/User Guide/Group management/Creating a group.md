---
title: "Creating a group"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/creating-group"
---

Message Queue for Kafka allows you to create groups in the console or use the consumer SDK to parse and display group information. Once the flexible group creation feature is disabled, you can only create groups in the console. This topic introduces the methods and procedures for creating a group.

<span id="20e0a3c0"></span>
## Background information

Kafka's Consumer Group feature is a scalable and resilient mechanism for consumers. In Message Queue for Kafka, a group is a virtual grouping of consumers. All consumers in the group coordinate to consume all partitions in the subscribed topics.

In Message Queue for Kafka, the supported group creation methods for Kafka instances are controlled by the flexible group creation feature. This feature is enabled by default.


* If this feature is enabled, you can not only create groups in the console but also get, parse, and display the group information using the consumer SDK. Groups that are not created in the console can still call the relevant APIs of Apache Kafka to consume messages, commit consumer offsets, and perform other operations.

* If this feature is disabled, you can only create groups in the console.


<span id="9cfcb797"></span>
## Precautions


* The maximum number of groups that can be created per instance depends on the partition quota. The group quota for an instance is twice the partition quota. Consider the instance type is kafka.n3.x2.tiny. If only the free quota of 250 partitions is used, up to 500 groups can be created. If you buy 50 more partitions in addition to free 250 partitions, up to 600 groups can be created.

   The maximum number of partitions supported varies depending on instance types. For more information, refer to [Product specifications](https://docs.byteplus.com/en/docs/kafka/specifications).

* The flexible group creation feature is enabled by default. Once the feature is disabled, groups can only be created in the console, and group information cannot be parsed through the consumer SDK. However, this does not affect the consumption status of existing groups, and new data synchronization tasks or connectors can still be created.


<span id="77dce926"></span>
## Creating a group in the console


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. In the top menu bar, click **Group Management**.

5. On the upper\-left corner of the page, click **Create Group**.

6. Specify the basic information of the group.

   
   |Configuration Item |Description |
   |---|---|
   |Group ID |A group ID must meet the following requirements:<br><br><br>* Must be 3 to 128 characters in length.<br><br>* Can only contain letters, digits, at signs ( @ ), hyphens ( \- ), and underscores ( _ ).<br><br>* The group ID cannot be modified after the group is created. Set a group ID carefully. |
   |Describe |A brief description of the group. On the **Group Management** page, you can view or modify the description of the group you created. |
   |Tag |Click **Add** **tag** enter the tag key and tag value, and add a custom tag to the Group.<br><br>Tags are used to identify and classify cloud resources. Adding tags helps to identify and manage the Group. Up to 20 tags can be added each time. |
   

7. Click **Create**.


<span id="c08a34b5"></span>
## Configuring a group with an SDK

After the flexible group creation feature is enabled, you can specify a group ID that conforms to naming conventions in the consumer SDK for consumption. Message Queue for Kafka automatically parses, retrieves, and displays the information about this group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When configuring a group with an SDK, including non\-compliant characters in the group ID leads to issues like failure to collect group monitoring data.</div>


<span id="d34f9cf8"></span>
### 1. Enabling Automatically create groups

The **Automatically create** **groups** feature is enabled by default. If you disable the feature, you can re\-enable it by performing the following steps:


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. In the top menu bar, click **Group Management**.

5. On the upper\-left corner of the page, toggle the **Automatically Create Groups** switch to enable the feature.

6. In the pop\-up dialog box, click **OK**.


<span id="edf1e927"></span>
### 2. Specifying a group during consumption

After enabling the **Automatically Create Groups** feature, you can call APIs on the consumer client to create consumers, configure consumer groups, and subscribe to topics to start consumption. You can follow the sample code below to configure consumer groups in the consumer SDK for consumer instances.

```Java
// Set the startup parameters for the consumer.
    private void setProps(Properties kafkaProperties) {
        .......
        // Assign the consumer instance to a consumer group. Consumer instances in the same consumer group load balance messages to be consumed.
        props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("consumer.group.id"));
        .......
    }

// Construct a consumer object, which creates a consumer instance.
    private void newConsumer() {
        consumer = new org.apache.kafka.clients.consumer.KafkaConsumer(props);
    }

    // Subscribe to a topic.
    private void subscribed(Properties kafkaProperties) {
        // Set the topic that the consumer group subscribes to, with topicName being the name of the created topic.
        List subscribedTopic =  new ArrayList();
        subscribedTopic.add(kafkaProperties.getProperty("topicName"));
        consumer.subscribe(subscribedTopic);
    }
```
