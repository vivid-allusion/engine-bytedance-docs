---
title: "Creating an instance"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_an_instance"
---

Before using the API gateway, you must first create gateway instances that are isolated from each other in terms of resources. This article describes how to create an API gateway instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

API Gateway currently supports the following two gateway instance types, as shown in the following table.


|Gateway types |Descriptions |
|---|---|
|Standard gateway |Provides a complete set of gateway features and supports connecting to multiple backend services. Includes: Vital Kubernetes Engine, Function Service (FaaS), Elastic Compute Service, and more. |
|Serverless gateway |For BytePlus Function Service (FaaS), the API Gateway specifically provides Serverless gateway instances. The features and limitations are as follows:<br><br><br>* Connect to the backend: This service only supports connecting to BytePlus Function Service (FaaS).<br><br>* Billing: Instance hosting fees are waived; CLB specification fees and public network fees are charged. Among them, public network fees are charged based on actual data usage only.<br><br>* Specifications: Selection of node specifications and quantity is not supported. Only the Small I specification is supported for CLB.<br><br>* Quota: Each BytePlus root user is allowed to create only one per region. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The BytePlus account has been registered and real\-name authentication has been completed.

* The VPC and its subnets have been created in the region where the API Gateway is deployed. If you want to deploy the API gateway across multiple availability zones, you must first create subnets in the target availability zones. For detailed actions, refer to [Create a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* To use the monitoring feature, complete the following preparations:

   * Activate Vital Managed Service for Prometheus.

   * In the region where your API Gateway business is located, [Create a VMP workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

   * To enable default alerts, please create the [Alert aggregation policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules) and [Alert notification policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules) in advance.

* To use the Logs feature, you must complete the following preparations:

   * Activate BytePlus Log Service TLS.

   * A log project has been created on the TLS side. The API gateway automatically creates a default log topic. If you want to use your own log topic, please create it beforehand.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* The gateway only supports connecting to Elastic Compute Service instances within the same VPC. If you need to connect to Elastic Compute Service, create a gateway instance in the VPC associated with the target Elastic Compute Service.

* The gateway only supports connection to Vital Kubernetes Engine within the same VPC. If you need to connect to Vital Kubernetes Engine, please create a gateway instance under the VPC planned for the target cluster.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **Instance Management**. On the Instance Management page, click **Create Instance**.

4. On the Create Instance page, configure the instance information as required.

   * **Basic Information**

      
      |Configuration Item |Descriptions |
      |---|---|
      |Region |Select the region for the API Gateway service. For the currently supported regions, refer to [Regions and Availability Zones](https://docs.byteplus.com/en/docs/apig/Regions_and_availability_zones). |
      |Gateway types |Select the gateway type to create. You cannot change the gateway type after creation.<br><br><br>* **Standard Gateway**: Provides a full set of gateway features and supports connection to multiple backend services.<br><br>* **Serverless gateway**: For BytePlus Function Service (FaaS), API Gateway specifically provides gateway instances of the Serverless type. |
      |Instance Name |Customize the API gateway instance name. Instance names must not be duplicated within the same Account. |
      |Notes |The remarks for the API gateway instance can be empty. |
      

   * **Specifications and configurations**

      
      |Configuration Item |Descriptions |
      |---|---|
      |Node specifications |For the standard gateway, you can select appropriate node specifications based on business requirements. |
      |Number of Nodes |For standard gateways, you can select an appropriate number of nodes according to business requirements.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To ensure high availability of the API gateway, select at least two nodes.</div><br> |
      |VPC |Select the VPC to which the cluster belongs. VPC provides an isolated, configurable, and manageable virtual network environment for the cluster.<br><br>If no available VPC exists, see [Create a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) for instructions on how to create one.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Gateway instances must be in the same VPC as backend Upstream resources, such as Elastic Compute Service and container server clusters.</div><br> |
      |Availability zone |An availability zone is a physical area within the same region where power and network infrastructure are independent. Different availability zones within a region are interconnected through an internal network.<br><br><br>* To meet disaster recovery requirements, please select at least two availability zones.<br><br>* After you check an availability zone, you must further select a subnet within the target availability zone. When selecting a subnet, the system displays the number of available IP addresses for that subnet.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Select an appropriate subnet based on your network planning. If too few IP addresses are available in the subnet, you may not be able to create cloud resources in this subnet later.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The subnet where the API gateway instance is located must have at least two available IP addresses.</div><br> |
      |Network model |Select the network type Allows selection of **public network** and **private network**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">At least one network type must be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Different network types have different billing rules.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">By default, the Serverless Gateway uses the <strong>public network</strong> type. The <strong>private network</strong> type can also be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After creation, the network type cannot be changed through configuration. If you need to change the network type, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000170">Submit a ticket</a>.</div><br> |
      |CLB specifications |Gateway instances use CLB as the gateway entry point. For a standard gateway, you can select an appropriate CLB specification based on business requirements. |
      |Public network billing |Select the billing method for the public network. For the standard gateway, the following two billing methods are supported:<br><br><br>* **Bandwidth cap billing**: Charges are based on the bandwidth cap you specify. The platform will limit bandwidth according to the cap you specify. Please set the bandwidth cap according to your business needs.<br><br>* **Billed based on actual outbound traffic**: Charges are based on the actual outbound traffic you use. For business scenarios characterized by large bandwidth fluctuations, charging based on actual traffic is more cost\-effective than charging based on the maximum bandwidth. |
      

   * **Observability**

      
      |Configuration Item |Descriptions |
      |---|---|
      |Monitoring alerts |The API gateway connects to the VMP Service of BytePlus, providing free monitoring and alerting capabilities for basic gateway metrics. To use the monitoring alert feature, please enable this switch.<br><br><br>* **Prometheus Workspace**: Required configuration after enabling monitoring alerts. Select the Prometheus workspace prepared in the prerequisites. All monitoring data from the current gateway instance will be collected and stored in the Prometheus workspace you have bound.<br><br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><br>* <div data-tips="true" data-tips-type="danger">After you bind the Prometheus workspace, you cannot change it.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">Deleting a Prometheus workspace may result in the permanent loss of gateway monitoring data. Please proceed with caution.</div><br> |
      |Enable alerts |Enable default alert notifications? Once enabled, APIG will provide default alerts to monitor the stability of your business.<br><br>You can customize alert rules. For detailed instructions, refer to [Alerting rule](https://docs.byteplus.com/en/docs/vmp/Alerting-rule).<br><br><br>* **Alert aggregation policy**: This is a required configuration after enabling alerts. Select the alert aggregation policy prepared in the prerequisites. The alert aggregation policy is used to specify the alert aggregation period and notification period in the system.<br><br>* **Alert notification policy**: Can be configured after alert is enabled. Select the alert notification policy prepared in the prerequisites.<br><br>   An alert notification policy is used to specify which alert contact groups should receive alerts when alerts of different severity levels occur. If not configured, only alert events will be generated and alert notifications will not be sent. |
      |Torch Log Service |The API gateway is based on BytePlus Torch Log Service TLS and provides you with persistently stored user access logs. To use the Logs feature, check this switch. |
      |log project |A log project is a fundamental resource management unit in Torch Log Service, used to isolate log resources and provide Identity and Access Management among multiple users, projects, or products. Please select the target log project. |
      |log topic |A log topic is the basic unit for log management in Torch Log Service. Each log topic is used to store logs of different types or categories within the same application.<br><br><br>* **Default configuration**: When you select the default configuration, the gateway will automatically create a topic named `gateway id-accessLog` under the current project.<br><br>* **Use an existing log topic**: Choose to use a log topic that has already been created. |
      |Tracing |Whether to enable the tracing feature for the API Gateway instance. After enabling, you need to select the backend Service for link tracing.<br><br><br>* **Application Performance Monitoring Full Link Edition**: Use APMPlus as the backend service for link tracing of API gateway instances. When you select this option, you need to configure the following:<br><br>   * API Key: Configure the API key for Application Performance Monitoring Full Link Edition.<br><br>* **Torch Log Service**: This service is used as the backend for API gateway instance link tracing. When you select this option, you need to configure the following:<br><br>   * **Log project**: Select the log project in Torch Log Service.<br><br>   * **Access Key ID**: The AccessKey ID (AK) of the BytePlus root user.<br><br>   * **Secret Access Key**: The Secret Access Key (SK) of the BytePlus root user. |
      

   * **Resource management**

      Select the resource project (Project) to which the API Gateway belongs. A resource project is a resource grouping and management mechanism provided by BytePlus that helps users achieve logical resource isolation. Through resource projects, you can perform project\-based authorization, bill splitting, and other operations.

5. Once configuration is complete, please carefully confirm the configuration details and order costs.

6. After confirming the information is correct, please read the "API Gateway Service Terms" and check the box to agree. Then, click **Confirm Order** to start creating the gateway instance.


<span id="7HUlCaA6"></span>
## Result validation

After the gateway instance is created, you can view the created gateway instance on the instance management page. A status of **Running** indicates that the creation was successful.

Click the gateway instance name to enter the instance details page, where you can view overview information, resource information, monitoring information, log information, and more.
