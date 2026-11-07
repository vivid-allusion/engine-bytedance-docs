---
title: "Create instance"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Create_instance"
---

Before connecting your application to the message queue for RabbitMQ, you need to create a RabbitMQ instance in the console. The message queue for RabbitMQ offers multiple instance specifications with different computing power and storage capacity. Choose the specification that fits your business needs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, you can create up to 5 RabbitMQ instances per region. Otherwise, you will encounter the error <strong>The Instance has exceeded quota</strong> when creating an instance. To increase quotas, submit an application in the <a href="https://console.byteplus.com/quota/productList/coParameterList?ServiceCode=RabbitMQ">Quota Center</a>. For example, to raise the maximum instance count (InstanceNum) per region up to 10.</div>


<span id="05b444e3"></span>
## Prerequisites


* If you need to access the message queue for RabbitMQ instance via a private network, first create an ECS cloud server, a VPC, and a subnet in the same region. After creating an instance, you can not change its VPC and subnet.

* If you need to access the message queue for RabbitMQ instance over the internet, first apply for an EIP in the same region. It is recommended that the EIP bandwidth limit exceeds the estimated peak public traffic. For detailed steps, see [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

* If you are creating a RabbitMQ instance for the first time, you need to complete cross\-service access authorization first. We recommend that you operate through the BytePlus main account. For detailed operation steps, refer to [cross-service access authorization](https://docs.byteplus.com/en/docs/rabbitmq/Cross_service_access_authorization).


<span id="9a32d0a5"></span>
## Operation steps


1. Log in to [Message Queue for RabbitMQ Control Console](https://console.byteplus.com/rabbitmq).

2. Select the region where you want to create the instance from the top menu bar.

3. On the **Instances** page, click **Create Instance** in the top left corner.

   When creating an instance for the first time, after clicking **Create Instance**, the page will automatically redirect to the cross\-service access authorization page. Please complete the authorization according to the page instructions. For detailed specifications, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/rabbitmq/Cross_service_access_authorization).

4. Fill in the basic configuration information for the RabbitMQ instance.

   
   |**Parameter** |**Description** |
   |---|---|
   |Instance name |Name of the RabbitMQ instance.  The following requirements must be met:<br><br><br>* May only include Chinese characters, letters, numbers, underscores (_), and hyphens (\-), and can not start with a number or hyphen.<br><br>* The length of characters ranges from 1 to 128.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no name is specified when creating an instance, the instance ID is used as the default name.</div><br> |
   |Instance description |Brief description of the RabbitMQ instance. |
   |Instance types |Type of the RabbitMQ instance.<br><br><br>* Stand alone: deploy with a single RabbitMQ agency.<br><br>* Cluster: deploy with multiple RabbitMQ brokers to achieve highly reliable message storage.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In a stand alone RabbitMQ instance, queues have no replica. Therefore, business can not recover within seconds after restarting the RabbitMQ node for instance upgrades. If you want to ensure business stability in such scenarios, choose the cluster version and use multi\-replica queues, such as mirrored queues or quorum queues.</div><br> |
   |Deployment method |The deployment mode of the instance in the current region. Supports the following settings:<br><br><br>* **Single availability zone deployment**: create a RabbitMQ instance in a specified availability zone within the current region. Single availability zone deployment reduces network latency and improves access speed. Now you need to specify 1 availability zone for the instance.<br><br>* **Multiple availability zone deployment**: create RabbitMQ instances across multiple availability zones within the current region. Cross\-available zone deployment improves availability but may cause network latency of 2ms to 3ms. Now you need to specify 3 availability zones for the instance. |
   |version |RabbitMQ version number; currently supports RabbitMQ `3.8` and `3.12`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The rabbitmq\-3.12 version natively supports the MQTT protocol. We recommend you to use version 3.12 for MQTT scenarios.</div><br> |
   |Computing specifications |Computing specifications of RabbitMQ instance<br><br>Instances with different computing specifications have varied recommended TPS peaks, suggested queue numbers, maximum connections, and storage thresholds. Please plan computing capacity and storage space based on your actual business needs and select specifications accordingly.<br><br>For detailed specifications on the instance's computing and storage, see [Product specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications). |
   |Storage specifications |Storage capacity of the RabbitMQ instance.<br><br>The storage capacity range depends on the computing specifications. Please set it reasonably according to business needs. |
   

5. Set access method.

   
   |**Access method** |**Description** |
   |---|---|
   |Private network |Please specify the private network where the RabbitMQ instance resides.<br><br>A private network (VPC, Virtual Private Cloud) is an isolated, self\-configured, and self\-managed virtual network environment built for cloud resources. If no private network is available under the current account, create a new one following the on\-screen instructions. For detailed steps, refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the instance is created, its associated private network can not be changed. Choose carefully when creating the instance.</div><br> |
   |subnet |Please specify the subnet where the RabbitMQ instance is located.<br><br>A subnet is a VPC network segment allocated within a specified available zone. It provides private IP addresses for cloud resources such as cloud servers and load balancers. If no private network is available under the current account, create a new one by following the on\-screen instructions. For detailed steps, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Once the instance is created, the corresponding subnet can not be changed. Choose carefully when creating the instance.</div><br> |
   |Public network access |Public network access is disabled by default. To enable it, check **Enable public network access** and select an EIP.<br><br>An EIP provides a dedicated public IP resource, including a public IP address and public outbound bandwidth service. The public address will bind your Elastic IP (EIP). Fees are charged by the EIP.<br><br>The public network can be disabled when you create and can be enabled or disabled after the creation is done. For details, see [Set public network access](https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access). |
   

6. (Optional) Set up SSL.

   After enabling the public network, SSL is enabled by default. So client connections to the instance need to be authenticated via SSL.

   After enabling SSL, data is transmitted with encryption, providing higher security. You can also enable public network access and SSL authentication after creating the instance. For details, refer to [Set public network access](https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">SSL\-encrypted transmission is supported only in the public network environment.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After enabling public network access, SSL is enabled by default and data is transmitted via SSL encryption. During this period, disabling SSL authentication is not supported.   </div>
   

7. Set the administrator username and password.

   Enter the administrator username and password, then re\-enter the password to confirm. Usernames and passwords must meet the following requirements:

   
   |**Configuration** |**Description** |
   |---|---|
   |Administrator username |Customize the administrator's username. The following requirements must be met:<br><br><br>* Only letters, numbers, hyphens (\-), and underscores (_) are allowed.<br><br>* The length of characters ranges from 3 to 64.<br><br>* The username "admin" can not be used as the administrator username. |
   |password |Administrator user password. The following requirements must be met:<br><br><br>* Include three of the following: uppercase letters, lowercase letters, numbers, and special characters. Special characters include `#_-+=`.<br><br>* The length of characters ranges from 8 to 32. |
   

8. (Optional) Set the **Project**.

   Select the IAM project of the currently created RabbitMQ instance from the drop\-down list. If no IAM project is specified, message queue for RabbitMQ will add the new instance to the IAM project named `Default`.

   The IAM project is a resource group in BytePlus Identity and Access Management (IAM), with different access policies for each project. IAM supports policy management. You are allowed to classify various cloud resources across multiple regions under this cloud account into different projects and create distinct access policies for each project to manage cloud resources flexibly.

   If you have not created any IAM projects or can not find a suitable IAM project, click **Create new project** to create a new IAM project.

9. (Optional) Set tags.

   Click **Add tag**, then enter the tag key and tag value to add tags to the instance.

   Tags are used to identify and classify cloud resources. You can categorize RabbitMQ instances using tags to facilitate searching and resource aggregation. For details, please refer to [Tag management](https://docs.byteplus.com/en/docs/rabbitmq/Tag_overview).

10. Select **Billing method** and click **Confirm order**.

   The message queue for RabbitMQ version supports pay\-as\-you\-go billing method. 

   
   |**Billing Types** |**Description** |
   |---|---|
   |Pay\-as\-you\-go billing |Use first, pay later. It is billed hourly so you can flexibly purchase and release resources as needed. |
   

11. Please confirm the order details and agree to the related agreements and then click **Buy now**.

   After purchasing, it takes about 3 to 15 minutes to create an instance. Please wait a moment. Thanks for your patience.

   You can view the created instances on the [Message Queue for RabbitMQ console](https://console.byteplus.com/rabbitmq) under the **Instances** page. If the instance status is **Running**, the instance is created successfully.
