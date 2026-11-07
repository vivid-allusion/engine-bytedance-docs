---
title: "Instance management"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/instance-management-FAQ"
---

This topic provides answers to frequently asked questions (FAQs) related to instance management in Message Queue for Kafka.

<span id="3609c855"></span>
## Why am I unable to delete an instance?

In general, an instance may fail to be deleted because of the following reasons:


* Instance resources have not been cleared. Before you delete an instance, make sure that all services and resources such as groups, topics, and connectors have been deleted.

* The instance status does not meet the requirement. Make sure that the Kafka instance is in the **运行中** state and has no background tasks in progress.

* You cannot directly delete a subscription instance in the Message Queue for Kafka console. Instead, find the instance order in the Billing Center, then cancel the subscription.


<span id="e131f3e4"></span>
## Why am I charged for a pay\-as\-you\-go instance even if I do not use it after the purchase?

When you buy a pay\-as\-you\-go instance, BytePlus assigns corresponding resources to the instance. The pay\-as\-you\-go instance is billed starting from the time of its creation and fees are settled on the hour until the instance is deleted. Fee settlement is independent of whether the instance is used or not. We recommend that you buy instances of the corresponding specifications based on your business requirements.

<span id="fd6036cb"></span>
## Why does the error message "The InstanceNum has exceeded quota %!s(MISSING)" appear when I create an instance?

By default, you can create up to eight Kafka instances in each Region. The maximum total storage capacity of all instances under each BytePlus account is 90 TiB in each Region. If these limits are exceeded, the error message **The instance_num/storage_sum has exceeded quota** appears. If you want to increase the instance quota, submit an application in the Quota Center. For example, apply to increase the maximum number of instances (InstanceNum) in each Region to 16.

<span id="b8bad74b"></span>
## Why is historical data not deleted after I modify the message retention period for my instance?

Issue description: After you modify the message retention period for your instance, the message retention period of the topic is not automatically modified at the same time. In addition, the messages that have been retained for more than the new retention period are not automatically cleared from the topic.

Cause: Modifications to the message retention period of an instance do not take effect on existing topics. Therefore, the back\-end service cannot detect and delete expired messages. The retention period of messages in a topic is subject to the topic parameter settings. When creating a topic, you can configure the topic to follow the message retention period of the instance or specify a separate message retention period for the topic.
