---
title: "Prepare the environment"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Prepare_the_environment"
---

BytePlus message queue for RabbitMQ is fully compatible with open\-source RabbitMQ. Businesses can migrate to the cloud quickly without code changes, saving maintenance and usage costs.

<span id=".MSDlh4blpIfotKblj7c="></span>
## Prerequisites


* Before enabling the service, you need to register a BytePlus account and complete enterprise real\-name authentication. For pay\-as\-you\-go RabbitMQ instances, the account balance must be at least USD 100 to create and use the service normally. For creating a BytePlus account and completing enterprise authentication, please refer to  [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* RabbitMQ instances are enabled by default for private network (VPC) access. VPC provides network\-isolated virtual environments where only instances within the VPC can access the RabbitMQ instance. Before creating a RabbitMQ instance, ensure that available VPCs and subnets exist in the target region. For setup instructions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating a VPC, note the following:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The VPC and RabbitMQ instance must be in the same region. Cross\-region access is not supported.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Configure appropriate security groups and related rules.   </div>
   

* To access the RabbitMQ instance through VPC, please purchase a cloud server in the same region first. After that, configure its private network and set up the Java development environment. This section uses the ECS of the Linux system as an example to introduce the basic process. If accessing the RabbitMQ instance via public network, your cloud server or self\-built IDC must also have public network access.


<span id=".MyDlh4blpIflvIDlj5Hnjq_looM="></span>
## Operation steps


1. Prepare the server.

   To access the instance via VPC, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to buy an ECS cloud server. If accessing the instance via public network, you can set up the server environment directly in your local IDC.

2. Install JDK.

   It is recommended to use [JDK](https://www.oracle.com/java/technologies/javase-downloads.html) 1.8 or later versions.

3. Install Maven.

   It is recommended to use [Maven](http://maven.apache.org/download.cgi#) version 2.5 or later.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

[Create a RabbitMQ instance](https://docs.byteplus.com/en/docs/rabbitmq/Create_instance)
