---
title: "Creating an instance"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/creating-instance"
---

Before you can use Message Queue for Kafka, a Kafka instance must be created in the console. Message Queue for Kafka offers a variety of instance types to meet different computational and storage needs. Select an instance type that best suits your business needs. This topic describes how to create a Kafka instance.

<span id="前提条件"></span>
## Before you begin


* The first time you create a Kafka instance, you must complete cross\-service access authorization. We recommend that you operate with a BytePlus account. For more information, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/kafka/cross-service-authorization).

* To access Message Queue for Kafka instances through a virtual private cloud (VPC), create an Elastic Compute Service instance, a VPC, and a subnet in the same Region, with at least six idle private IP addresses in the subnet. You cannot modify the VPC of an instance once the instance is created.

* To enable internet\-facing access to Message Queue for Kafka, apply for Elastic IP Address (EIP) in the same Region, ensuring the allocated EIP bandwidth exceeds the estimated peak of internet traffic.


<span id="注意事项"></span>
## Precautions

By default, you can create up to eight Kafka instances in each Region. The maximum total storage capacity of all instances under each BytePlus account is 90 TiB in each Region. If these limits are exceeded, the error message **The instance_num/storage_sum has exceeded quota** appears. If you want to increase the instance quota, submit an application in the Quota Center. For example, apply to increase the maximum number of instances (InstanceNum) in each Region to 16.

<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region in which you want to create an instance.

3. On the upper\-left corner of the **Instances** page, click **Create Instance**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating an instance for the first time, clicking <strong>Create Instance</strong> automatically redirects you to the cross\-service access authorization page. Follow the prompts to complete authorization. For more information, refer to <a href="https://docs.byteplus.com/en/docs/kafka/cross-service-authorization">Cross\-service access authorization</a>.   </div>
   

4. Specify **Basic information** for the Kafka instance.

   
   |**Parameter** |**Description** |
   |---|---|
   |Instance Name |The name of the Kafka instance. It must meet the following requirements:<br><br>Can only contain Chinese characters, letters, digits, underscores ( _ ), and hyphens ( \- ).<br><br>Cannot start with a digit or a hyphen ( \- ).<br><br>Must be 1 to 128 characters in length.<br><br>If no instance name is specified, the instance ID is used as the default instance name. |
   |Instance Description |A brief description of the Kafka instance. Must be 1 to 128 characters in length. |
   

5. Specify **Specification configuration** for the Kafka instance.

   
   |**Parameter** |**Description** |
   |---|---|
   |Deployment plan |How the instance is deployed in the current Region. The following options are supported:<br><br><br>* **Single Availability Zone Deployment**: creates the Kafka instance in a specified Availability Zone in the current Region. It can reduce a network latency and accelerate access.<br><br>   In this case, one Availability Zone must be specified for the instance.<br><br>* **Multiple Availability Zone Deployment**: creates the Kafka instance across multiple Availability Zones in the current Region. It can increase availability but introduces a network latency of 2 ms to 3 ms.<br><br>   In this case, three Availability Zones must be specified for the instance.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since there are only two Available Zones in the China(HongKong) Region and the Asia Pacific (Johor) Region, when purchasing Kafka instances in these two Regions, only   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Single Availability Zone Deployment</strong> can be selected.   </div><br>    |
   |Version |Kafka version. The supported Apache Kafka versions are:<br><br><br>* **2.2.2**<br><br>* **2.8.2** |
   |Calculation specification |The instance type of the Kafka instance.<br><br>Different instance types offer varying peak read and write traffic, number of partitions, and storage specification thresholds. Plan the demands for computing power and storage space as needed, and select an appropriate instance type. |
   |Storage type |The volume type for storing data in the Kafka instance. The volume type can be ESSD_FlexPL or ESSD_PL0. Compared with ESSD_PL0, ESSD_FlexPL delivers higher input/output operations per second (IOPS) and better stability in high message throughput scenarios where a large number of messages are accumulated.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the peak traffic is greater than 100 MB/s, use ESSD_FlexPL.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The storage type cannot be modified after an instance is created. Proceed with caution when you select the storage type.</div><br> |
   |Storage Specifications |The storage capacity of the Kafka instance.<br><br>The storage capacity depends on instance types. Set the storage capacity as needed. |
   |No. of Partitions |The number of partitions for the Kafka instance. Set the number of partitions as needed.<br><br>Different instance specifications offer varying free partition quotas. Additional charges apply for the number of partitions exceeding the free quota. For more information on the range of partitions that can be created for each specification, refer to [Product specifications](https://docs.byteplus.com/en/docs/kafka/specifications). For more information on billing methods of partitions, refer to [Billing items](https://docs.byteplus.com/en/docs/kafka/billable-items). |
   |Advanced parameters |The advanced parameters of the Kafka instance, including the maximum message size. For more information, refer to the table below. |
   

   Configuration instructions of advanced parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |Maximum message size |The maximum size of a single message that can be sent and received by Message Queue for Kafka. The parameter configuration must match that of the producer and consumer clients to avoid message loss.<br><br>Unit: MB. Value range: 1–12. Default value: 10. |
   |Message retention period |The maximum retention period of messages when disk capacity is sufficient. Unit: hour. Value range: 1–2160, which means messages can be retained for a maximum of 90 days.<br><br>When the disk utilization reaches 90%, to ensure service availability, the back\-end service automatically deletes some historical messages. For more information, refer to [Disk capacity threshold policy](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter). |
   |Consumer offset retention period |The maximum retention period of a consumer offset. From when a consumer offset is committed, consumer offsets whose retention period exceeds the specified period are deleted. Each time a consumer offset is committed to a topic partition, the retention period of the consumer offset is reset to zero.<br><br>Unit: minute. Value range: 1–10080, which means consumer offsets can be retained for a maximum of 7 days. Default value: 4,320 minutes, equivalent to 3 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Modifying the consumer offset retention period of an instance triggers a rolling restart, which may result in short service downtime. We recommend that you implement a reconnection mechanism on the client to avoid issues with the client being unable to reconnect after disconnecting.</div><br> |
   |Message time type |The type of the message timestamp. It defaults to CreateTime. The following options are supported:<br><br><br>* LogAppendTime: The time when a message is written to the Kafka instance is used as the message timestamp.<br><br>* CreateTime: The time when the producer creates the message, that is, the message timestamp of the CreateTime type passed in by the client. |
   |Automatically Delete Groups |Whether to automatically delete the group. The feature is disabled by default.<br><br><br>* After this feature is enabled, if all consumers in a consumer group are in the Empty state, the consumer group is automatically deleted after the consumer offset retention period expires.<br><br>* After this feature is disabled, the automatic deletion of data related to the message consumption progress does not affect the status of consumer groups, and the system does not automatically delete groups in the Empty state.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Modifying this parameter configuration triggers a rolling restart, which may result in short service downtime. We recommend that you implement a reconnection mechanism on the client to avoid issues with the client being unable to reconnect after disconnecting.</div><br> |
   

6. Specify **Network configuration** for the Kafka instance.

   
   |**Parameter** |**Description** |
   |---|---|
   |Access Method |How the Kafka instance is accessed.<br><br><br>* Virtual Private Cloud: Specify the VPC and subnet where the Kafka instance is located. A virtual private cloud (VPC) is an isolated, customizable, and self\-managed virtual network environment for cloud resources. Create a VPC following the prompts if none is available.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once the instance is created, the corresponding VPC cannot be modified. Exercise caution when creating an instance.   </div><br>   <br><br>* Public Network Access: Internet\-facing access is disabled by default. To enable it, check the **Enable Public Network Access** check\-box and select an EIP. An EIP offers independent public IP resources, including public IP addresses and public outbound bandwidth. Your public address is associated with your EIP, with costs incurred by EIP.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When internet\-facing access is enabled, Message Queue for Kafka assigns a public endpoint to the instance so that clients can connect to the Kafka instance over the internet. Select a suitable endpoint depending on whether SSL authentication is needed. The client supports one\-way SSL authentication for server certificates, and data transmission is encrypted, offering higher security compared to standard internet\-facing access methods.   </div><br>    |
   |Allowlist |Associate the Kafka instance with an allowlist. After the instance is associated with an allowlist, only the IP addresses and CIDR blocks in the allowlist can access the instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The default value is default, with the IP address being 0.0.0.0. If the default value is used when creating an instance, the back\-end service allows all IP addresses to access the Kafka instance. For security reasons, we recommend that you associate the instance with an existing allowlist or promptly create an allowlist as prompted when creating an instance.</div><br><br><br>You can check one of the check\-boxes to associate the instance with an existing allowlist or a new allowlist.<br><br>Associating with an existing allowlist: Associate the instance with an existing allowlist. Set **Binding Mode** to **Associate with an existing allowlist**, and select an existing allowlist. An instance can be associated with a maximum of 100 allowlists.<br><br>Associating with a new allowlist: Create an allowlist and associate the instance with it. For more information on how to configure an allowlist, such as an allowlist name, refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/kafka/creating-allowlist). |
   

7. Specify the advanced configurations.

   Specify **Affiliated project** and **Tag**.

   
   |Parameter |Description |
   |---|---|
   |Affiliated project |Select an Identity and Access Management (IAM) project for the Kafka instance.<br><br>If you have not created any IAM projects or do not have an appropriate IAM project to choose from, click **Create Project** to create an IAM project. If no IAM project is specified, Message Queue for Kafka adds the new instance to an IAM project named `default`.<br><br>IAM projects serve as resource groups in BytePlus IAM, each with its own set of access control lists. With IAM policy management, you can categorize various cloud resources across multiple Regions in the account into different projects and create distinct access policies for each project, enabling flexible management of cloud resources. |
   |Tag |The tag of the instance. Tags are used to identify and categorize cloud resources. You can classify Kafka instances by tag for simplified instance search and resource aggregation. For more information, refer to [Tag overview](https://docs.byteplus.com/en/docs/kafka/tag-overview).<br><br>Click **Add tag** then type a tag key and a tag value to add a tag to the instance. |
   

8. Specify **Billing Method** and click **Confirm Order**.

   Message Queue for Kafka supports pay\-as\-you\-go methods. Pay\-as\-you\-go allows hourly post paid billing. You can buy and release resources on demand. After creating a pay\-as\-you\-go instance, you can convert it to a subscription instance as needed.

9. Confirm the order details, read and agree to the relevant agreement, then click **Buy Now**.

10. On the **Instance** page, view the instance you created.

   Creating an instance takes approximately 3 to 15 minutes. Your patience is appreciated The **Running** status indicates that the instance has been successfully created.
