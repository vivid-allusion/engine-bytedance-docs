---
title: "Creating resources"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/creating-resources"
---

This topic describes how to create a Kafka instance and a topic in the Message Queue for Kafka console.

<span id="准备工作"></span>
## Before you begin


* Activate Message Queue for Kafka and set up the development environment. Created Kafka instances run in virtual private clouds (VPCs). Before you create an instance, make sure that a VPC and a subnet are available. For more information, refer to [Setting up the development environment](https://docs.byteplus.com/en/docs/kafka/setting-up-environment).

* If you want to access a Kafka instance over the internet, first apply for an elastic IP address (EIP) in the same Region.


<span id="1 创建实例"></span>
## Step 1: Create an instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The first time you create a Kafka instance, you must complete cross\-service access authorization. We recommend that you operate with a BytePlus account. For more information, refer to <a href="https://docs.byteplus.com/en/docs/kafka/cross-service-authorization">Cross\-service access authorization</a>.</div>



1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region in which you want to create an instance.

3. On the upper\-left corner of the **Instances** page, click **Create Instance**.

4. Follow the on\-screen instructions to select the instance specifications and basic configurations, and click **Confirm the order**.

   For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance).

5. Confirm the order details, read and agree to the relevant agreement, then click **Buy now**.

   After the instance is created, you can view the endpoints on the **Instance Details** tab of the instance. For more information, refer to [Viewing instance details](https://docs.byteplus.com/en/docs/kafka/viewing-instance-details).


<span id="2 创建 Topic"></span>
## Step 2: Create a topic

To create a topic:


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the **Instances** page, click the name of the target instance.

3. On the **Topic Management** tab, click **Create Topic**.

4. In the **Create Topic** dialog box, configure the basic parameters of the topic.

   For more information, refer to [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic).

5. Click **Create**.


<span id="3 （可选）创建 SASL 用户"></span>
## (Optional) Step 3: Create a SASL user

After a Simple Authentication and Security Layer (SASL) user is created for a Kafka instance, the Kafka instance provides a SASL endpoint. You can use this endpoint to access the instance only after the data passes the SASL username and password authentication.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Skip this step if you use the default endpoint instead of a SASL username and password to access the instance.</div>


* <div data-tips="true" data-tips-type="tip">When you create a Kafka instance, a SASL PLAIN user is automatically created synchronously. If you want to access the instance by using the username and password of a SCRAM SASL user, follow the procedure given in this section.</div>


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, click the name of the instance.

4. On the **User Management** tab, click **Create user**.

5. Configure the relevant parameters.

   For more information, refer to [Creating a SASL user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser).

6. Click **Create**.

   After these resources are created, you can produce and subscribe to messages by using Message Queue for Kafka.


<span id="4 查看接入点"></span>
## Step 4: View endpoints

After an instance is created, you can view the endpoints of the instance in the console. To view endpoints:


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, click the name of the instance.

4. Navigate to **Instance Details \> Service access**, then view the internet\-facing access status and endpoints of the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The SASL public endpoint, also known as the SASL_SSL endpoint, is displayed only if the internet\-facing access feature is enabled for the instance. If the instance is connected by using this endpoint, SSL authentication must be performed on messages from clients.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">An instance endpoint is displayed in the format of <code>domain name:port number</code>. When you connect to an instance, specify the complete endpoint information, including the domain name and port number.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on instance endpoints, refer to <a href="https://docs.byteplus.com/en/docs/kafka/viewing-endpoints">Viewing endpoints</a>.   </div>
