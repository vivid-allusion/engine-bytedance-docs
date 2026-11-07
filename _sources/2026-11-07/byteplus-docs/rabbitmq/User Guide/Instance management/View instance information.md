---
title: "View instance information"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/View_instance_information"
---

After creating a RabbitMQ instance, you can view the RabbitMQ instances and details for each instance on the console, including basic information, instance specifications, storage configurations, access information for each protocol endpoint, and billing details.

<span id=".5p-l55yL5a6e5L6L6K-m5oOF"></span>
## View instance details


1. Log in to the [Message Queue for RabbitMQ console](https://console.byteplus.com/rabbitmq).

2. Select the region where the instance is located from the top menu bar.

3. View the basic information of the instance on the **Instances** page.

   The instance list displays all instances under the current region. You can check the instance name and ID, status, tags, availability zone, VPC, instance type, specifications, version, billing method, creation time, and associated project in the list.

4. Click the instance name to view detailed information on the **Instance information** tab.

   The **Instance information** tab shows details including instance basic information, specifications and storage configuration, access endpoints for various protocols, and billing information.


<span id=".5a6e5L6L5Z-65pys5L-h5oGv"></span>
## Instance basic information

The instance list displays the instance name, ID, and other basic information. The description for each item is as follows.


|**Configuration** |**Description** |
|---|---|
|Instance name/ID |Name and ID of the instance.<br><br>If no name is specified when creating the instance, the instance ID is used as the instance name by default. |
|Status |Instance running status. |
|Tags |Tags of the instance.<br><br>Tags consist of key\-value pairs and are used to identify cloud resources. They help classify cloud resources with similar characteristics from different dimensions such as purpose, owner, or environment. With the help, it is easier to filter, aggregate, and manage resources in the cloud. For details, refer to [Tag management](https://docs.byteplus.com/en/docs/rabbitmq/Tag_overview). |
|Availability zone |Availability zone of the instance. |
|Private network |VPC where the instance is located after enabling VPC access. |
|Instance types |Basic types of instances.<br><br><br>* Stand alone: Deploy a single RabbitMQ broker.<br><br>* Cluster: Deploy multiple RabbitMQ brokers to achieve highly reliable message storage. |
|Specification |Instance specifications. |
|version |RabbitMQ version. Currently supports `3.8` and `3.12` versions. |
|Billing method |The billing method for the instance. |
|creation time |Instance creation time. |
|Project |IAM project the instance belongs to.<br><br>To change the associated project, manage it in the **IAM console \> resource management**. |


<span id=".5a6e5L6L6K-m57uG5L-h5oGv"></span>
## Instance details

The **Instance information** tab displays the basic information, instance configuration, access information, and payment information of the instance, explained in detail below.


|**Category** |**Configuration** |**Description** |
|---|---|---|
|Basic information |Instance ID |Instance ID. |
||Instance name |Name of the instance. |
||Description |Instance description. |
||version |RabbitMQ version.<br><br>Currently supports `3.8` and `3.12` versions. |
||Tags |RabbitMQ instance tags.<br><br>Tags consist of key\-value pairs and are used to identify cloud resources. They help classify cloud resources with similar characteristics from different dimensions such as purpose, owner, or environment. With the help, it is easier to filter, aggregate, and manage resources in the cloud. For details, refer to [Tag management](https://docs.byteplus.com/en/docs/rabbitmq/Tag_overview). |
||Private network |VPC where the instance is located after enabling VPC access. |
||Subnet |VPC subnet name where the instance is located after enabling VPC access. |
||Availability zone |Availability zone of the instance. |
||Project |IAM project the instance belongs to.<br><br>To change the associated project, manage it in the **IAM console \> resource management**. |
||creation time |Instance creation time. |
|Instance configuration |Instance types |Basic types of instances. |
||Instance specifications |Instance computing specification and storage specification. |
||Used/Available storage space |Instance storage space, including total space and used space. |
|Service access |Public network access |Toggle for public network access method.<br><br>When enabled, each access point provides a public network address. You can choose the appropriate access method based on your business needs. |
||SSL |Whether SSL authentication is enabled.<br><br>Enabling SSL encrypts data transmissions, providing higher security. When public network access is enabled, SSL authentication is turned on by default and can not be disabled. |
||Administrator username and password |The administrator username and password for the open\-source web UI are not displayed in detail in the console.<br><br>After creating a RabbitMQ instance, keep the username and password safe. If lost, click **Reset** to reassign the username and password. You can also change the username and password in the web UI. |
||Private network address supports public network parse |Indicates whether private IP address support for public network parse is enabled. |
||Web UI endpoint |Access address for RabbitMQ open\-source web UI. |
||Web MQTT access point |The access point for the Web MQTT protocol.<br><br>After enabling the rabbitmq_web_mqtt extension, this access point's detailed information will appear in the console.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After enabling public network access, the access point address for the public network environment is displayed. The public network environment currently does not support SSL access. You can connect via WebSocket (ws), but WebSocket (wss) is not supported.</div><br> |
||AMQP endpoint |Entry point for the AMQP protocol.<br><br>You can use the AMQP protocol to access RabbitMQ through this entry point. |
||Stomp access point |Access point for the Stomp protocol.<br><br>After enabling the rabbitmq_stomp extension, the console will display detailed information about this access point.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After enabling public network access, the access point address for the public network environment is displayed. The public network environment currently does not support SSL access. You can connect via WebSocket (ws), but WebSocket (wss) is not supported.</div><br> |
||MQTT access point |The MQTT protocol access point.<br><br>The console shows detailed information of this access point only after enabling the rabbitmq_mqtt extension. If public network access is not enabled, only access point addresses in the private network environment are displayed. |
|Payment information |Billing method |The billing method for the instance. |
||Expiration time |Instance expiration time. |
