---
title: "Delivering event notifications to Message Queue for Kafka"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delivering-event-notification-to-message-queue-for-kafka"
---

To monitor changes to your TOS bucket resources in real time, you can configure event notification rules. These rules allow you to receive alerts when specific events occur. TOS supports routing these notifications directly to Message Queue for Kafka. This topic describes the prerequisites and steps for configuring an event notification rule to deliver messages to Message Queue for Kafka.

<span id="RGxBuXON"></span>
## Background information

[Message Queue for Kafka](https://docs.byteplus.com/docs/kafka/what-is-message-queue-for-kafka) is a distributed messaging middleware service that is built based on Apache Kafka. TOS supports pushing event notifications directly to Message Queue for Kafka. If you have configured consumers in Message Queue for Kafka, it will deliver received messages to them. When the consumers receive the messages, they execute the relevant operations based on the predefined business logic.

<span id="H4u48RHq"></span>
## Prerequisites


* You have created a Message Queue for Kafka instance. For instructions, see [Create instance](https://docs.byteplus.com/docs/kafka/creating-instance).

* You have created a Message Queue for Kafka topic. For instructions, see [Create topic](https://docs.byteplus.com/docs/kafka/creating-topic).

* You have created a SASL user. You must set the **Password type** to **PLAIN** and enable the ALL Permitted option to grant the user write access to the topic. For instructions, see[ Create SASL user](https://docs.byteplus.com/docs/kafka/creating-SASLuser).


<span id="3u7c5df6"></span>
## Notes


* A bucket can create a maximum of 30 event notification rules.

* An object cannot match multiple rules that include the same event type. This means that, within the same bucket, **event types and prefixes/suffixes** across different rules cannot overlap.

* The total JSON description size of all event notification rules in a bucket cannot exceed 20 KB.


<span id="iP4aZQKi"></span>
## Creating an event notification rule


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. In the **Buckets** list, click the bucket you want to configure.

3. In the left navigation pane, select **Basic configurations \> Event notification**.

4. On the **Event notification** page, click **Create rule**.

5. On the **Create event notification** page, set the following parameters:

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |Basic configurations |Event name |Specify the name of the event notification rule. Naming rules:<br><br><br>* Event names must be unique within the bucket.<br><br>* Length must not exceed 255 characters. |
   ||Prefix |Enter the prefix of the object(s) to be matched.<br><br>For example, if the prefix is set to **test/** , then objects in the `test` directory will be matched. |
   ||Suffix |Enter the suffix of the object(s) to be matched.<br><br>For example, if the suffix is set to  **.png**, then all objects in `PNG` format will be matched.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If neither a prefix nor a suffix is set, all objects in the bucket will be matched.</div><br> |
   |Event type |Events |Select the event(s) to be notified. For a list of types supported by TOS, see [Supported event types](https://docs.byteplus.com/docs/tos/Event-notification-overview#.5pSv5oyB55qE5LqL5Lu257G75Z6L).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the same event type is selected in different rules, the object\-matching scopes for this event type must not overlap. This means that a single object cannot trigger multiple rules containing the same event type.</div><br><br><br><div data-tips="true" data-tips-type="warning">For example, if Rule A is created to send a notification for PutObject events on objects with the suffix <code>png</code>, Rule B cannot be configured to trigger for PutObject events on objects with the same suffix <code>png</code>. If there is an overlap, the creation of the rule will fail.</div><br> |
   |Data target |Target type |Select **Kafka**.To select multiple instances, click **Add row**. Up to five instances can be set. |
   ||Role |Click **Click to Authorize**, and TOS will automatically create the role TOSNotiKafkaRole to grant TOS access to Message Queue for Kafka. |
   ||Instance ID |Select the desired Message Queue for Kafka instance(s).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no instance is available, you can create one through the <a href="https://console.byteplus.com/kafka/region:kafka+ap-southeast-1/">Message Queue for Kafka console</a>. For instructions, see <a href="https://docs.byteplus.com/docs/kafka/creating-instance">Create instance</a>.</div><br> |
   ||Topic |Select the desired Message Queue for Kafka topic(s). |
   ||User name |Select the applicable Message Queue for Kafka SASL user(s). |
   

6. Once you have finished configuring, click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The event notification rule takes effect five minutes after creation.   </div>
   

<span id="R6C0Y2xF"></span>
## Viewing event notification messages

You can view event notification messages in the Message Queue for Kafka console. Follow these steps:


1. Log in to the [Message Queue for Kafka console](https://console.byteplus.com/kafka/region:kafka+ap-southeast-1/).

2. In the top menu bar, select the region of the instance that is associated with your event notification rule.

3. In the **Instances** list, click the instance name.

4. On the Instance details page, click the **Message query** tab.

5. Select **Query by time** and the desired **Topic**. Set **Partition** to **All** and specify the query time range. Then, click **Query**.

   The page displays a list of messages that match the filter criteria. This list includes the following information: topic name, partition, offset, key, value, value message size, and storage time. The **Value** column shows the specific content of event notifications. To learn more about event notification parameters, see [Event Notification structure](https://docs.byteplus.com/docs/tos/Event-notification-overview).
