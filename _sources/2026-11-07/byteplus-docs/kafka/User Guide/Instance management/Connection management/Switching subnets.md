---
title: "Switching subnets"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/switching-subnets"
---

After associating a virtual private cloud (VPC) and subnets with an instance, you can switch subnets in the VPC as needed. This topic describes how to switch subnets in a VPC.

<span id="背景信息"></span>
## Background information

After associating a VPC and subnets with an instance, if you must replan your business network or switch networks, you can switch the subnet for your Kafka instance in the VPC by associating another subnet with the instance. After switching to another subnet, the IP addresses of all private endpoints of the instance are changed to another private IP address in the new subnet. However, the endpoint domain name and port of the instance are not changed, ensuring that existing client connections are not affected.

<span id="前提条件"></span>
## Before you begin

Create a subnet with at least six idle IP addresses in the same VPC.

<span id="注意事项"></span>
## Precautions


* The VPC cannot be modified. When switching subnets, only other subnets in the same VPC can be selected.

* The endpoint of a Kafka instance is in the form of a domain name. Switching subnets modifies the private IP address corresponding to the domain name. Make sure to clear the client's DNS cache. Switching subnets does not modify the endpoint of the instance, negating the need for modifications to JDBC or other application connection strings.

* When starting to switch subnets, a background task is generated for the Kafka instance and displayed in the background task list. You can view the progress of the subnet switch in time. For more information, refer to [Managing background tasks](https://docs.byteplus.com/en/docs/kafka/managing-background-tasks).

* During the switching process, the Kafka client is disconnected from some brokers. Make sure that your service has an automatic reconnection mechanism.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the **Instances** page, click the name of the target instance.

3. In the **Basic information** pane of the **Instance Details** tab, locate the **Subnet** column and click **Modify**.

4. In the pop\-up dialog box, select a new subnet. If no suitable subnet is available, create a subnet following the prompts.

5. Click OK.
