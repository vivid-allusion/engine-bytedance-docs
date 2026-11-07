---
title: "Preparations"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Apache-Java-SDK-Preparations"
---

Before you run Java SDK code to send and receive messages, you need to prepare your development environment by following the steps provided in this article.

<span id="4b2c06eb"></span>
## Development environment


|**software** |**version requirement** |
|---|---|
|[JDK](https://www.oracle.com/java/technologies/javase-downloads.html) |Version 1.8 or above. |
|[Maven](http://maven.apache.org/download.cgi#) |Version 2.5 or above. |


<span id="37d2ed5c"></span>
## Operation steps

<span id="54c2be1d"></span>
### 1 Create a resource

Before accessing the message queue Kafka version to send and receive messages, you need to create resources and users.


1. Create a Kafka instance in the Byteplus Engine console.

   Please refer to [Creating an instance](https://docs.byteplus.com/en/docs/kafka/creating-instance) the detailed operation steps.

2. Create Topic.

   Each message belongs to a Topic, and the Topic of interaction needs to be specified when sending and receiving messages. Please refer to [Creating a topic](https://docs.byteplus.com/en/docs/kafka/creating-topic) the detailed operation steps.

3. (Optional) Create SASL user and ACL.

   When creating an instance, you need to specify the username and password of the PLAIN mechanism. It is used to create a SASL user of PLAIN type. This user has read and write permissions for all Topics and Groups by default. You can access the message queue Kafka version through the SASL access point and consume messages using the PLAIN mechanism.

   If you need more fine grained permission control, you can also create a new SASL user and add an ACL to it to grant the user the specified permission for the specified resource. Please refer to [Creating a SASL user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser) the detailed operation steps.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When sending and receiving messages through the default access point, there is no need to create a SASL user and authenticate through a SASL user.   </div>
   

<span id="752d6cf8"></span>
### 2 Collect connection information

When calling the relevant interface class to send and receive messages, you need to configure parameters such as connection information in the code. Please refer to the following steps to obtain connection information before sending and receiving messages.


1. Collect access point addresses.

   After creating an instance, you can view the information of the access point in the **Service access** area on the overview page of the instance. For detailed instructions, please refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).

2. Get the Topic name.

   After creating the topic, you can view the Topic name in the **Topic Management** tab.

3. (Optional) Get the SASL username and password.

   When creating a SASL user, you need to specify the username and password of the SASL user. Please keep this information safe. After creating a PLAIN user, you can check the password in the **user management** tab, please refer to [Viewing a PLAIN SASL user password](https://docs.byteplus.com/en/docs/kafka/viewing-SASLuser-password) the detailed operation. If you forget the password of the SCRAM user, you can reset the user password. Please refer to [Resetting a SASL user password](https://docs.byteplus.com/en/docs/kafka/resetting-SASLuser-password) the detailed operation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please use the username and password of the corresponding type of user for SASL authentication according to the client side authentication mechanism. For example, the username and password of the PLAIN user should be used under the PLAIN mechanism. For detailed instructions, please refer to <a href="https://docs.byteplus.com/en/docs/kafka/viewing-endpoints">Viewing endpoints</a>.   </div>
   

<span id="f3077a13"></span>
### 3 (optional) Download Demo

Byteplus Engine Message Queue Kafka Edition provides you with a Demo for quick access and experience. Please download the demo and unzip it into your local project. The profile template is located at the path `{DemoPath}/src/main/resources/` In, you can refer to [Configuration file](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Configuration-file) learn about detailed parameter configuration.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc369bc253c4400a9f85e8326e182a8b~tplv-goo7wpa0wc-image.image" name="bp-kafka-java-demo.tar.gz">bp-kafka-java-demo.tar.gz</Attachment>
