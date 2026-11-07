---
title: "Viewing instance details"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/viewing-instance-details"
---

After Kafka instances are created, you can view the Kafka instance list and detailed information for each instance in the console. This includes basic information like instance status, instance configurations like instance specifications and storage space, access details like endpoints for different protocols, and payment information.

<span id="查看实例详情"></span>
## Viewing instance details


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, view basic information about the instance.

   The instance list displays instances in the current Region. You can view details such as the instance name and ID, status, Availability Zone, virtual private cloud (VPC), topic, group, instance description, billing type, associated project, and creation time.

4. Click the instance name to view its detailed information on the **Instance Details** tab.

   The **Instance Details** tab displays basic information like instance status, instance configurations like instance specifications and storage space, access details like endpoints for different protocols, and payment information.


<span id="实例基本信息"></span>
## Instance basic information

The instance list displays basic information, such as the name and ID of the instance. The items are described as follows:


|**Parameter** |**Description** |
|---|---|
|Instance Name/ID |The name and ID of the instance.<br><br>If no instance name is specified, the instance ID is used as the default instance name. |
|State |Instance status. |
|Availability Zone |The Region and Availability Zone of the instance. |
|VPC |The VPC of the instance once internal access is enabled. |
|Topic |The number of topics created in the current instance. |
|Group |The number of groups created in the current instance. |
|Tag |The tags of the current instance. |
|Billing methods |The billing method of the instance. |
|Affiliated project |The IAM project associated with the instance. |
|Create Time |The time when the instance was created. |


<span id="实例详细信息"></span>
## Instance details

The **Instance Details** tab displays the instance resource statistics, basic information, configurations, access details, payment information, and more. Detailed descriptions are as follows.


| |**Parameter** |**Description** |
|---|---|---|
|Resource Statistics |Topic |The number of topics created in the current instance. |
||Group |The number of groups created in the current instance. |
||partition |The number of the used and remaining available partitions in the current instance. |
|Basic information |Instance ID |The instance ID. |
||Instance name |The instance name. |
||Availability Zone |The Availability Zone of the instance. |
||Instance description |The instance description. |
||Version |The Kafka version, supporting 2.2.2 and 2.8.2. |
||VPC |The VPC of the instance once internal access is enabled. |
||Subnet |The name of the VPC subnet of the instance after internal access is enabled. |
||Tag |The tags of the Kafka instance.<br><br>Tags consist of key\-value pairs and are used to identify cloud resources. You can use tags to classify cloud resources with the same characteristics from different dimensions such as purposes, types, owners, and environments. This helps you filter and aggregate data, and manage cloud resources easily. For more information, refer to [Tag overview](https://docs.byteplus.com/en/docs/kafka/tag-overview). |
||Affiliated project |The IAM project associated with the instance. |
|Instance Configuration |Instance specification |The instance type and storage specification. |
||Calculation specification |The extended description of instance type, usually displaying the peak values of read and write traffic. |
||Used/Available Storage Space |The storage space of the instance, including the total space, used space, and the current water level percentage. |
||Storage type |The volume type for storing data in the instance. Options are ESSD_FlexPL and ESSD_PL0. ESSD_FlexPL has better IOPS performance. The storage type cannot be changed once the instance is created. |
|Parameter configuration |Message retention period |The maximum retention period of messages when the disk capacity of brokers is sufficient. If the disk capacity of brokers is insufficient, historical messages are automatically deleted by default to maintain service availability. |
||Consumer offset retention period |The maximum retention period of a consumer offset. |
||Maximum message size |The maximum size of a single message that can be sent and received by Message Queue for Kafka. |
||Message time type |The type of the message timestamp.<br><br><br>* LogAppendTime: The time when a message is written to the Kafka instance is used as the message timestamp.<br><br>* CreateTime: The time when the producer creates the message, that is, the message timestamp of the CreateTime type passed in by the client. |
||Automatically Delete Groups |Whether a group is automatically deleted.<br><br><br>* After this feature is enabled, if all consumers in a consumer group are in the Empty state, the consumer group is automatically deleted after the consumer offset retention period expires.<br><br>* After this feature is disabled, the automatic deletion of data related to the message consumption progress does not affect the status of consumer groups, and the system does not automatically delete groups in the Empty state. |
|Service access |Public Network Access |The current internet\-facing access status. You can enable or disable internet\-facing access for the instance here. Once enabled, the associated public IP address can also be viewed here.<br><br>For more information, refer to [Enabling internet-facing access](https://docs.byteplus.com/en/docs/kafka/enabling-internet-facing). |
||Default access point |Supports standard access over the PLAINTEXT protocol. It allows direct access without configuring an account and a password. |
||SASL_Access Point |Supports secure access over the SASL_PLAIN protocol. Simple Authentication and Security Layer (SASL) username and password authentication is required for login.<br><br>For more information on SASL users, refer to [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL). |
|Payment information |Billing Method |The billing method of the instance. |
