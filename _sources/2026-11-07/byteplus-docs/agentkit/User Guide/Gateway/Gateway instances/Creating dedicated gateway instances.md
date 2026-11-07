---
title: "Creating dedicated gateway instances"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances"
---

A gateway instance is a dedicated gateway resource in AgentKit that provides a unified access entry for services such as model services, MCP services, and MCP toolsets. Gateway instances are suitable for production environments or business scenarios that require independent capacity, resource isolation, centralized management of access entries, and separate billing. After you create a gateway instance, you can associate the instance with service resources of the corresponding type, such as MCP services, MCP toolsets, or model services. This topic describes how to create a gateway instance.

## Prerequisites

* Gateway instances are **pay\-as\-you\-go** resources. Before creating a dedicated gateway instance, ensure your BytePlus account has an available balance greater than **USD 5**. If the balance is insufficient, please go to the console to recharge before proceeding.

* **You understand the billing methods, specifications, and billing items of gateway instances**. The gateway instance that you create in this topic is a **dedicated gateway instance**. Using a dedicated gateway instance incurs fees. For the billing items and reference prices, see[ Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).

* (Optional) To configure private network access, make sure that you have activated  Virtual Private Cloud (VPC) and have available VPC and subnet resources. For more information, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

> **warning**

> After creating the gateway instance, you may not be able to modify configurations such as gateway type, network access method, and the gateway of associated resources. Confirm your business scenario, network access method, and required specification capabilities before you create the instance. The limits displayed in the console shall prevail.

## Limits

* Gateway instances currently support only the ** pay\-as\-you\-go** billing method.

* A gateway instance of a specific type can be associated only with resources of the corresponding type.

   * **MCP gateway:**  A gateway instance can connect only to MCP services and MCP toolsets.

   * **Model gateway:**  A gateway instance can connect only to model services.

   * **Agent runtime gateway**: A gateway instance can connect only to runtime instances.

* Gateway instances of different specifications have different upper limits on QPS, client connections, and the number of resources that can be associated. Select an appropriate gateway specification based on your business requirements.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, click "Create gateway".

   > **tip**

   > If you are creating a gateway for the first time, click "Create gateway" in the upper\-right corner of the page. Otherwise, click "Create gateway" in the upper\-left corner of the gateway instance list.

3. On the creation page, configure the parameters as described in the following table.

   |Parameter​ |Description |
   |---|---|
   |**Basic information** ||
   |Instance name |Enter a name for the gateway instance.<br><br><br>* After the gateway instance is created, you can modify its name in the "Configuration information" section of the instance.<br><br>* We recommend that the instance name reflect the business, environment, and purpose, for example, prod_mcp_gateway_01. |
   |Billing method |Select the billing method for the gateway instance. Currently, only **Pay\-as\-you\-go** is supported. |
   |Gateway type |Select the gateway instance type. You can create only one gateway instance of each type.<br><br><br>* **MCP gateway**: Used to connect to MCP resources (MCP services and MCP toolsets). If the resource to be associated with the gateway instance is an MCP resource, select this type.<br><br>* **Model gateway**: Used to connect to model services. If the resources to be associated with the gateway instance are model services, select this type.<br><br>* **Agent runtime gateway**: Used to connect to runtime resources. If the resource to be associated with the gateway instance is a runtime resource, select this type.<br><br><br>> **warning**<br><br><br>> Each gateway instance can be associated only with resources of its corresponding type. That means an MCP gateway can be associated only with MCP resources, a model gateway only with model services, and an agent runtime gateway only with runtime instances.<br> |
   |**Specification configuration** ||
   |Gateway specification |Select the specification for the gateway instance. The resource limits, such as **QPS** and ** the maximum number of client connections**, and fees vary by specification. Select an appropriate specification to avoid affecting your business. For the fees for each specification, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items). |
   |**Network configuration** ||
   |Availability zone |Select the availability zones where the gateway instance is deployed. To ensure high availability of the gateway instance, select at least two availability zones.<br><br><br>* Availability zone selection is required regardless of whether private network access is enabled.<br><br>* If private access is enabled, select subnets in the corresponding availability zones. |
   |Inbound access |Select the inbound access method for the gateway instance.<br><br><br>* **Configuration instructions**<br><br>   * After the gateway instance is created, you cannot change the network access method. <br><br>   * **Public network ** and **Private network** are supported. Configure at least one access method. You can also configure both access methods at the same time.<br><br>* **Available methods**<br><br>   * **Public network**: Callers are in the public network environment or need to access the gateway instance across networks. Examples include local development and debugging or cross\-VPC and cross\-environment access when Direct Connect or private network connectivity is unavailable. When you use this method, the access endpoint is exposed to the public network. Therefore, you need to apply stricter controls over the allowed access sources and authentication settings. We recommend that you enable public network access only when it is necessary.<br><br>   * **Private network**: Callers reside within a VPC in the same region or have network connectivity to the VPC via Direct Connect, VPN, CEN, or other methods, and traffic must stay within the private network. When you use this method, the access endpoint resides in your private network, which inherently reduces public network exposure. This method is more suitable for production workloads that have stricter requirements for data security and access boundaries.<br><br>      * **VPC**: Select the VPC for the gateway instance. We recommend that you select a VPC and subnets that are in the same region and under the same network plan as your main callers and backend resources.<br><br>      * **Subnet**: Select available subnets under the selected VPC. Select one subnet in each availability zone to ensure high availability of your service.<br><br><br>> **tip**<br><br><br>> If your callers reside in both the public network and the private network, you can enable both public network access and private network access. For example, developers perform development and debugging over the public network, and production services make calls within a VPC. We recommend that you prioritize private network access for production traffic and use public network access only for development and debugging or emergency use.<br> |
   |**Observability configuration** ||
   |Torch Log Service |Specifies whether to enable Torch Log Service (TLS) for the gateway instance. After TLS is enabled, you can view the service logs of the gateway instance to troubleshoot issues such as failures, abnormal requests, and runtime errors.<br><br><br>* **Log feature**:<br><br>   * The log service is ** enabled** by default. If you do not need it, you can manually uncheck the Torch Log Service checkbox.<br><br>   * For more information about TLS features, see [Viewing logs](https://docs.byteplus.com/en/docs/agentkit/Viewing_logs).<br><br>* **Log billing**:<br><br>   * After you enable the log service, the platform activates the TLS service for you and writes your dedicated gateway logs to the default log topic of the selected log project.<br><br>   * **Using the log service incurs fees. For more information, see the ** [log billing instructions](https://docs.byteplus.com/en/docs/tls/billable_items?lang=en) **.**  |
   |Log project |Configure this parameter only after you enable Torch Log Service. Select the project to which the gateway instance logs are written. Under this log project, the gateway instance automatically generates a log topic named **agentkit\-gateway\-access\-log**. |
   |**Advanced configuration** ||
   |Associated project |A project is a collection of resources. You can add a new gateway instance to a project and manage it centrally at the project levellevel. This helps keep resources independent and maintain data security. For more information about projects, see [Managing projects](https://docs.byteplus.com/en/docs/agentkit/Managing_projects).<br><br><br>* By default, resources are associated with the **default** project. Each resource can belong to only one project.<br><br>* After you select a project, only users who have permissions on the project can use the created gateway instance. <br><br>* If no projects are available, you can click the "Create project" button to create one. After you create a project, return to this page to select the new project. |
   |Tag |A tag is a ** key\-value ** pair used to identify cloud resources. Tags help you categorize cloud resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources.<br><br>Click "+ Add tag", select an existing tag or enter a new tag to associate the tag with the gateway instance. For more information, refer to [Tag management](https://docs.byteplus.com/en/docs/agentkit/Tag_management).<br><br>> **tip**<br><br><br>> You can associate up to 20 tags per request and up to 50 tags with a single resource.<br> |

4. In the ** Configuration details ** and ** Cost details** areas on the right side of the page, confirm the specification, gateway type, inbound access method, and fee items for the current configuration. Read and select the "I have read and agree xxx" checkbox, and then click "Buy now" to complete the operation.

5. Return to the gateway instance list page to view the creation result. In the list, you can view information about the newly created gateway instance, such as its name, status, specification, and inbound access method.
