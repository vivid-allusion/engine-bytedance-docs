---
title: "Instance management"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Instance-management-faq"
---

This topic provides answers to frequently asked questions (FAQs) related to instance management in Message Queue for Kafka.

<span id="45c664a8"></span>
## How do I select an instance type and storage specification?

Message Queue for Kafka offers multiple instance types for your choice. You can select an instance type and storage specification based on the maximum read and write traffic, storage space, and number of partitions that are required by your business.


* Read and write traffic:

   * Select the traffic specifications based on the maximum read traffic and maximum write traffic of the network interface, whichever is higher.

   * We recommend that you estimate the maximum traffic based on your actual traffic plus 30%, then select a suitable instance type by considering other specifications.

* Storage space: Actually occupied storage space = Business message volume × Number of replicas ÷ 75%

   * Message Queue for Kafka supports multi\-replica data storage. The storage space of a Kafka instance is the sum of the storage space of all replicas.

   * Some storage space is used for storing logs and metadata. Redundant messages also occupy additional space. For these reasons, the actual available storage space is less than the storage specification you set. We recommend that you reserve a storage space of around 25%.

* Number of partitions: Specify the number of partitions based on your business requirements. Each instance type offers a certain number of free partitions. You can also buy more partitions.


<span id="341abeef"></span>
## How do I select a volume?

You can specify the volume type for data storage when creating a Kafka instance. The volume type can be ESSD_FlexPL or ESSD_PL0. Compared with ESSD_PL0, ESSD_FlexPL delivers higher input/output operations per second (IOPS) and better stability in high message throughput scenarios where a large number of messages are accumulated.


* If the peak traffic is greater than 100 MB/s, use ESSD_FlexPL.

* You cannot modify the storage type after an instance is created. Proceed with caution.


<span id="c6fe8ca3"></span>
## How do I delete or unsubscribe from an instance?

Before you delete or unsubscribe from an unnecessary instance that is in the **Running** state, clear all resources and services of the instance.


* Deleting or unsubscribing from a pay\-as\-you\-go instance: Clear all resources of the instance, then find the instance on the **Instances** page. In the **Actions** column, click **Detele**.

* Deleting or unsubscribing from a subscription instance: Clear all resources of the instance, find the order of the instance in the **Billing center**, then cancel the subscription.


<span id="0c755eb7"></span>
## Is message compression supported?

Yes, Kafka instances can send and receive compressed messages. To use message compression, you must enable the feature on the Message Queue for Kafka client. The following table describes the compression formats supported by Message Queue for Kafka and the related resource overheads.


|Item |Description |
|---|---|
|Supported compression formats |Message Queue for Kafka supports multiple open source compression formats. Among them, LZ4 consumes more resources on instances. We recommend that you use other compression formats such as Snappy. |
|How to enable |In the configuration file of the producer, set the `compression.type` parameter. By default, this parameter is set to `none`, indicating that compression is disabled. To use the `Snappy` compression format, set this parameter to `snappy`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Message compression consumes additional CPU resources. We recommend that you enable the feature in compression scenarios such as log collection. Do not enable this feature in other scenarios unless otherwise required.</div><br> |


<span id="e03009e8"></span>
## Can I deploy a Kafka instance across Availability Zones?

Yes, Message Queue for Kafka allows you to deploy an instance across Availability Zones. Namely, multi\-AZ instances are supported. Multi\-AZ instances deliver excellent disaster recovery capabilities and can ensure cluster data reliability and service availability.

When you buy a Kafka instance, you can set its deployment method to multi\-AZ deployment and select three Availability Zones to achieve cross\-AZ disaster recovery. After an instance is created, you cannot modify its deployment method. That is to say, the deployment method of an existing instance cannot be changed from single\-AZ deployment to multi\-AZ deployment.

To view the number of Availability Zones for an existing Kafka instance, go to **Instance Details \> Basic information \> Availability Zone**. If the number of Availability Zones is greater than 1, the instance is deployed across Availability Zones.

<span id="7cdf0ae3"></span>
## How do I change the deployment method of an instance from single\-AZ deployment to multi\-AZ deployment?

After an instance is created, you cannot modify its deployment method. That is to say, the deployment method of an existing instance cannot be changed from single\-AZ deployment to multi\-AZ deployment. If a multi\-AZ instance is required, we recommend that you buy a new instance and migrate the data of the existing instance to the new one.

<span id="be5e6172"></span>
## Is my business affected if I change the instance specification or scale up the instance?

Message Queue for Kafka allows you to change the instance type, storage specification, and number of partitions for an instance. The specific impacts of changes to these specifications on the instance are as follows:


* If you change the instance type, the brokers in an instance are restarted sequentially on a rolling basis. This may cause transient connections between the client and some brokers. If you upgrade the instance type, a partition rebalance event occurs. In this case, the back\-end service automatically performs data migration. We recommend that you upgrade instance configurations during off\-peak hours.

* Increasing the storage space or the number of partitions does not interrupt your business.


<span id="d53b36b6"></span>
## How do I add partitions to an instance?

Each instance type of Message Queue for Kafka supports a certain range for the number of partitions and offers a different number of free partitions. You can buy partitions within the range allowed for the corresponding instance type as needed. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).

After buying partitions, refer to [Modifying topic configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) to add partitions to a topic. This way, the message processing performance of the topic is improved.

<span id="fde33c6d"></span>
## Can I delete a partition?

No, you cannot directly delete a partition or decrease the number of partitions in an existing topic. To decrease the number of partitions in a topic, delete the existing topic, create a new one, and then reset the number of partitions of the new topic.

<span id="3d6c4de3"></span>
## Why am I unable to reduce the number of partitions?

Due to the limits of Apache Kafka, you are not allowed to reduce the number of partitions in a topic.

<span id="3816bbef"></span>
## Is scaling down of instances supported?

No, Message Queue for Kafka does not support scaling down of instances. You cannot reduce the storage space of an instance or downgrade the instance type.

<span id="c191a8e8"></span>
## Do I have to use a SASL_SSL endpoint when I access an instance over the internet?

You can use a SASL_SSL or SASL_PLAINTEXT endpoint when you access an instance over the internet.

Select a suitable endpoint based on whether an SSL certificate is required.


* SASL_SSL endpoint: An SSL certificate is required for message authentication and encryption. This ensures data security and prevents data interception and eavesdropping when data is being transferred over the network. Using a SASL_SSL endpoint improves security when compared with ordinary access over the internet. Currently, one\-way authentication is supported, that is, only the client verifies the certificate of the Kafka instance.

   For more information on how to connect to a Kafka instance by using a SASL_SSL endpoint, refer to[Connecting to an instance by using a SASL_SSL endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL).

* SASL_PLAINTEXT endpoint: No SSL certificate is required, and the Kafka client code can be configured easily and quickly.

   For more information on how to connect to a Kafka instance by using a SASL_PLAINTEXT endpoint, refer to [Connecting to an instance by using a SASL_PLAINTEXT endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_PLAINTEXT).


<span id="支持哪些语言的客户端？"></span>
## What programming languages of clients are supported?

Message Queue for Kafka supports TCP client SDKs in all programming languages provided by Apache Kafka. We provide code examples for programming languages such as Java, Go, and Python for your reference. For more information, refer to [Overview](https://docs.byteplus.com/en/docs/kafka/SDK-overview).

<span id="支持的消息体最大是多少？"></span>
## What is the maximum message size supported in Message Queue for Kafka?

Message Queue for Kafka allows you to customize the maximum message size based on instances and topics. Messages beyond the limits cannot be pushed. The maximum message size (MessageMaxByte) is 10 MB by default. You can set it between 1 MB and 12 MB.

The maximum message size can be adjusted using the following methods:


* Modify the related instance parameter to adjust the maximum message size at the instance level. For more information, refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).

* Modify the related topic parameter to adjust the maximum message size at the topic level. For more information, refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).


<span id="消息的保留时间是多久？"></span>
## How long is the message retention period?

Message Queue for Kafka allows you to customize the message retention period based on instances and topics. If the disk capacity is sufficient, messages are automatically cleared when their retention period expires. The message retention period (LogRetentionHours) is 72 hours by default. You can set it between 1 hour and 2,160 hours.

The message retention period can be adjusted using the following methods.


|Method |Description |
|---|---|
|Modifying the **Message Retention Period** parameter of an instance |After a message retention period is specified for an instance, the setting takes effect on all new topics that are created in the instance. The message retention period for all new topics follows the instance configuration by default. For more information, refer to [Modifying instance parameters](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).<br><br>Adjustments to the message retention period of an instance do not take effect on existing topics. We recommend that you manually modify the parameters of existing topics based on your business requirements. |
|Modifying the **Message Retention Period** parameter of a topic |After a message retention period is specified for a topic, the setting takes effect only on the current topic. For more information, refer to [Modifying topic parameters](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).<br><br>If the message retention period of a topic is shortened, the back\-end service re\-examines the retention period of existing data according to the new configuration. Some messages may be determined as expired and thus deleted. |


In addition, Message Queue for Kafka allows you to configure the disk capacity threshold policy by specifying the **Automatically delete old messages** parameter. When the disk capacity reaches the threshold, Message Queue for Kafka automatically deletes historical messages or suspends the writing of new data according to the policy. This prevents exceptions caused by a disk utilization of 100% to Kafka instances. If the disk capacity threshold policy is configured, messages may be deleted before the specified maximum retention period ends. For this reason, pay attention to the disk capacity of your instance on a regular basis. If the disk capacity is insufficient, upgrade your instance specifications at the earliest opportunity. For more information on the disk capacity threshold policy, refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter).

<span id="56263916"></span>
## What versions of Apache Kafka are supported?

Message Queue for Kafka is compatible with Apache Kafka versions 2.2.2 and 2.8.2. We recommend that you use Kafka clients corresponding to these versions.

Message Queue for Kafka is fully backward compatible with earlier client versions. You can also use Apache Kafka clients of other versions. For example, you can select a Kafka instance of version 2.x when you create a self\-managed Kafka project of version 0.x, 1.x, or 2.x. The following table describes the compatibility of specific versions.


|Kafka Instance Version |Compatible Apache Kafka Version |Compatibility |
|---|---|---|
|2.2.2 |≤ 2.2.x |100% |
|2.8.2 |≤ 2.8.x |100% |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Message Queue for Kafka does not guarantee functional compatibility with higher client versions. This is because unique functionalities of higher client versions may be used on the business side, such as MirrorMaker 2.</div>
