---
title: "Topic and group management"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/topic-group-management-faq"
---

This topic provides answers to frequently asked questions (FAQs) related to topic and group management in Message Queue for Kafka.

<span id="e1120e5e"></span>
## How many topics are supported?

The number of topics is not limited in a Kafka instance. However, each topic must contain at least one partition. The maximum number of partitions varies with instance types. If the total number of partitions in existing topics already reaches the upper limit, new topics can no longer be created. To create a new topic, you must buy more partition quotas or upgrade your instance type.

<span id="edd167b2"></span>
## How many partitions are supported?

Multiple instance types are available for Message Queue for Kafka and each instance type supports a different maximum number of partitions. Each instance type offers a different number of free partitions. You can also buy more partitions as needed. Refer to the following table for the maximum number of partitions supported by each instance type.


|**Instance Type** |**Maximum Read Traffic (MB/s)**  |**Maximum Write Traffic (MB/s)**  |**Number of Free Partitions** |**Maximum Number of Partitions Allowable** |**Disk Capacity (GiB)**  |
|---|---|---|---|---|---|
|kafka.20xrate.hw |20 |20 |350 |350–1,000 |300–96,000 |
|kafka.30xrate.hw |30 |30 |350 |350–1,000 |300–96,000 |
|kafka.60xrate.hw |60 |60 |400 |400–1,000 |300–96,000 |
|kafka.100xrate.hw |100 |100 |600 |600–3,000 |600–96,000 |
|kafka.150xrate.hw |150 |150 |700 |700–3,000 |900–96,000 |
|kafka.200xrate.hw |200 |200 |750 |750–3,000 |1,200–96,000 |
|kafka.250xrate.hw |250 |250 |800 |800–3,000 |1,500–96,000 |
|kafka.300xrate.hw |300 |300 |900 |900–3,000 |1,800–192,000 |
|kafka.600xrate.hw |600 |600 |1,800 |1,800–5,000 |2,400–192,000 |
|kafka.800xrate.hw |800 |800 |2400 |2,400–6,000 |4,000–288,000 |
|kafka.1000xrate.hw |1,000 |1,000 |3,000 |3,000–7,000 |5,500–384,000 |
|kafka.1200xrate.hw |1,200 |1,200 |3,600 |3,600–8,000 |6,500–480,000 |
|kafka.1500xrate.hw |1,500 |1,500 |3,600 |3,600–8,000 |8,000–576,000 |


<span id="edafe455"></span>
## Are ACLs supported by topics?

Yes. Message Queue for Kafka supports access control lists (ACLs) for permission management. You can grant permissions on specified topics and groups to different Simple Authentication and Security Layer (SASL) users.

Go to the **ACL Management** tab of the Message Queue for Kafka console, then click **Add ACL** to configure an ACL. For more information, refer to [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL).

<span id="b6eac370"></span>
## How do I manage consumer offsets in a group?

The broker records the consumer offsets committed by consumer clients. In most cases, consumer offset commits depend on the SDK used by the connected Kafka client. The SDK specifies a consumer offset by using the following two mechanisms:


* Automatic commit: The SDK commits the offset of the latest consumed message plus 1 to the broker at the specified time intervals.

* Manual commit: The SDK commits the offset of the latest consumed message plus 1 to the broker through an application.


Go to the **Consumption status** area on the group details page of the Message Queue for Kafka console, find the **Submit offset position** column of the specified topic. The displayed offset is the consumer offset committed by the client. When the consumer client continues to consume messages, the consumption starts from this offset. For more information, refer to [Viewing consumption status in a group](https://docs.byteplus.com/en/docs/kafka/Viewing-consumption-status).

You can reset consumer offsets in a group as follows. For more information, refer to[Resetting consumer offsets](https://docs.byteplus.com/en/docs/kafka/Resetting-consume-offsets).


* Based on the latest offset: Skip all accumulated messages and start to consume messages from the latest offset. Accumulated messages are not deleted because of the reset.

* Based on a specified point in time: Start to consume messages at a specific point in time selected from a specified past period. This period is determined by the message retention period specified for the topic.

* Based on a specified offset: Start to consume messages from a specified offset in the current partition. After the reset, consumers in the group start to consume messages from the specified offset in the current partition.


<span id="9bbe8b65"></span>
## How do I delete the subscription relationship if no topic subscription is needed in a group?

A subscription relationship cannot be deleted by deleting the corresponding topic or group in the console. To delete the subscription relationship, unsubscribe from the topic using a Kafka client.

<span id="abffe7e0"></span>
## How do I delete messages in a topic?

You cannot delete a specified message in Message Queue for Kafka. However, you can delete messages in batches by deleting a topic or modifying the message retention period for a topic.


* Deleting a topic: When you directly delete a topic, all messages stored in the topic are deleted. Proceed with caution.

* Modifying the message retention period for a topic: A shortened message retention period speeds up message aging. Proceed with caution because messages can also be deleted in batches when you use this method.
