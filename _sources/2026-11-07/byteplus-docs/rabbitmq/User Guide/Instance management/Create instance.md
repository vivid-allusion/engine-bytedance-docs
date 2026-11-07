---
title: "Create instance"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Create_instance_1"
---

Before integrating the application with the message queue for RabbitMQ, please create a RabbitMQ instance in the console. The message queue for RabbitMQ offers multiple instance specifications with varying computing power and storage capacity. You can choose the specification based on your actual business needs. This section describes the operation steps to create a RabbitMQ instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, you can create up to 5 RabbitMQ instances per region. Otherwise, instance creation fails with the error <strong>The Instance has exceeded quota</strong>. To increase the quota, submit an application in the <a href="https://console.byteplus.com/quota/productList/coParameterList?ServiceCode=RabbitMQ">Quota Center</a>. For example, you can apply to raise the maximum number of instances (InstanceNum) per region, up to 10.</div>


<span id="05b444e3"></span>
## Prerequisites


* If you need to access the message queue for RabbitMQ instance through a private network, first create an ECS cloud server, private network, and subnet in the same region. After creating instance, you can not change its private network and subnet.

* If you need to access message queue for RabbitMQ instance through the public network, first apply for an EIP in the same region. It is recommended that the EIP bandwidth limit exceeds the estimated peak public network traffic. For detailed steps, refer to [Apply for EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

* If creating a RabbitMQ instance for the first time, you must complete cross\-service access authorization first. It is recommended to use the BytePlus main account to perform this. For details, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/rabbitmq/Cross_service_access_authorization).


<span id="9a32d0a5"></span>
## Operation steps


1. Log in to the [Message Queue for RabbitMQ console](https://console.byteplus.com/rabbitmq).

2. Select the region where you want to create the instance from the top menu bar.

3. On the **Instances** page, click **Create Instance** in the upper left corner.

   When creating an instance for the first time, after clicking **Create Instance**, the page will redirect automatically to the cross\-service access authorization page. Follow the prompts to complete authorization. For detailed notes, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/rabbitmq/Cross_service_access_authorization).

4. Fill in the basic configuration information for the RabbitMQ instance.

   
   |**Parameter** |**Description** |
   |---|---|
   |Instance name |Name of the RabbitMQ instance. Must meet the following requirements:<br><br><br>* Can only include Chinese characters, letters, numbers, underscores (_), and hyphens (\-). It cannot start with a number or hyphen.<br><br>* Length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no name is specified when creating the instance, the instance ID will be used as the instance name by default.</div><br> |
   |Instance description |Brief description of the RabbitMQ instance. |
   |Instance Types |Type of RabbitMQ instance.<br><br><br>* Stand alone: Be deployed with a single RabbitMQ agency.<br><br>* Cluster: deploy multiple RabbitMQ brokers to ensure highly reliable message storage.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In a stand alone RabbitMQ instance, queues have no replicas. Therefore, restarting the RabbitMQ node for instance upgrades can not guarantee business recovery within seconds. If you want to ensure business stability in such scenarios, choose the cluster version and use multi\-replica queues. For example, you can choose mirrored queues or quorum queues.</div><br> |
   |Deployment method |The instance deploy method in the current region. Supports settings:<br><br><br>* **Single availability zone deployment**: create a RabbitMQ instance in the specified availability zone within the current region. Deploying within a single availability zone reduces network latency and improves access speed. You need to specify 1 availability zone for the instance at this time.<br><br>* **Multiple availability zone deployment**: create RabbitMQ instances across multiple availability zones in the current region. Cross\-availability zone deployment improves availability but may cause network latency of 2ms to 3ms. You need to specify 3 availability zones for the instance at this time. |
   |version |RabbitMQ version number, currently supports RabbitMQ `3.8` and `3.12` versions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">rabbitmq\-3.12 version natively supports MQTT protocol, recommending version 3.12 for MQTT scenarios.</div><br> |
   |Computing Specifications |Computing specifications of the RabbitMQ instance.<br><br>Instances with different computing specifications have varying recommended TPS peaks, suggested queue counts, maximum connections, and storage specification thresholds. Plan computing power and storage space based on actual business needs and select computing specifications accordingly.<br><br>For detailed information about instance computing and storage specifications, see [Product Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications). |
   |Storage specifications |The storage capacity of the RabbitMQ instance.<br><br>The storage capacity range depends on the compute specification. Set it reasonably according to your business needs. |
   

5. Set access method.

   
   |**Access Method** |**Description** |
   |---|---|
   |Private network |Please specify the private network where the RabbitMQ instance resides.<br><br>The private network (VPC, Virtual Private Cloud) is an isolated, self\-configured, and managed virtual network environment for cloud resources. if there is no available private network under the current account, create a new private network following the page instructions. For detailed steps, refer to [Create private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the instance is created, the associated private network cannot be changed. Choose carefully when creating an instance.</div><br> |
   |Subnet |Specify the subnet where the RabbitMQ instance is located.<br><br>a subnet is a segment of the VPC network assigned within a specified availability zone, providing private IP addresses for cloud resources such as cloud servers and load balancers. if there is no available private network under the current account, create a new private network following the page instructions. see [Create subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet) for detailed steps.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After instance creation, the associated subnet cannot be modified. Choose carefully when creating an instance.</div><br> |
   |Public network access |Public network access is off by default. To enable it, check **Enable public network access** and select an EIP.<br><br>The EIP provides independent public IP resources, including the public IP address and outbound bandwidth service. The public address will bind to your Elastic Public IP (EIP). Fees are charged by the EIP.<br><br>You can choose not to enable public network access during creation. After creating the instance, you can also enable or disable public network access. For details, refer to [Set public network access](https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access). |
   

6. (Optional) configure SSL.

   When enabling public network access, SSL is enabled by default, requiring client connections to authenticate via SSL.

   After enabling SSL, data is transmitted with encryption, providing higher security. You can also enable public network access and SSL authentication after creating the instance. For details, refer to [Setting up public network access](https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">SSL\-encrypted transmission is supported only in public network environments.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After enabling public network access, SSL is enabled and SSL encryption is used by default. During public network access, disabling SSL authentication is not supported.   </div>
   

7. Set the administrator username and password.

   Enter the administrator username and password, then re\-enter the password for confirmation. Usernames and passwords must meet the following requirements:

   
   |**Configuration** |**Description** |
   |---|---|
   |Administrator username |Customize the administrator username. Must meet the following requirements:<br><br><br>* Can only include English letters, numbers, hyphens (\-), and underscores (_).<br><br>* The length must be between 3 and 64 characters.<br><br>* admin cannot be used as the administrator username. |
   |Password |User password. Must meet the following requirements:<br><br><br>* Include at least three types among uppercase letters, lowercase letters, numbers, and special characters. Special characters include `#_-+=`.<br><br>* Length must be between 8 and 32 characters. |
   

8. (optional) Set the **Project**.

   Select the IAM project associated with the current RabbitMQ instance from the dropdown list. By default, the project is set as **default**. You can choose the target project from the dropdown list and it shall not be left empty.

   The IAM project is a resource group in BytePlus access control (IAM), with different access policies for each project. IAM supports policy management. You can categorize various cloud resources across multiple regions under this cloud account into different projects. Besides, you can create distinct access strategies for each project to enable flexible resource management.

   If you have not created any IAM projects or do not have a suitable IAM project to choose from, click **Create new project** to create one.

9. (optional) Set tags.

   Click **Add tag**, enter the tag key and tag value to add tags to the instance.

   Tags identify and classify cloud resources. You can categorize RabbitMQ instances with tags to facilitate instance search and resource aggregation. For detailed information, refer to [Tag management](https://docs.byteplus.com/en/docs/rabbitmq/Tag_overview).

10. Select **Billing method** and click **Confirm order**.

   The Message Queue for RabbitMQ version supports pay\-as\-you\-go and subscription billing methods. Each billing method has different payment methods, prices, and charging rules. Select the appropriate billing type according to your business needs.

   
   |**Billing method** |**Description** |
   |---|---|
   |Pay\-as\-you\-go billing |Use first, pay later. It is billed hourly so you can flexibly purchase and release resources as needed.<br><br>After creating a pay\-as\-you\-go instance, you can convert it to subscription instance based on business needs. |
   |Subscription |Pay in advance before use. The minimum purchase period is one month.<br><br>After choosing subscription, you need to select the **Subscription duration** and whether to enable auto\-renewal upon expiration. Once auto\-renewal is enabled, BytePlus will automatically deduct your account balance before the instance expires. No manual action is required. |
   

11. Confirm the order details, agree to the relevant agreements, and then click **Buy now**.

   After successfully purchasing the instance, it takes about 3 to 15 minutes to create. Please wait a moment. Thanks for your patience.

   You can view created instances in the [message queue for RabbitMQ console](https://console.byteplus.com/rabbitmq) under the **Instances** page. An instance status of **Running** indicates successful creation.
