---
title: "Creating MCP toolsets"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/MCP_toolset"
---

An MCP toolset is a unit for managing tools under an MCP service. You can use a toolset to centrally manage a group of related MCP tools and make them available for AI applications or agents to call. An MCP toolset supports three tool matching modes: full return, semantic retrieval, and tag retrieval. You can flexibly choose one based on the number of tools and business scenarios, improving call accuracy while reducing token consumption. This topic describes how to create an MCP toolset.

## Background information

The tools in an MCP toolset support multiple calling modes to accommodate different application scenarios.

|**Calling mode** |Description |**Application scenarios** |
|---|---|---|
|Full return |Returns all tools in the MCP toolset. |The number of tools in the MCP toolset is small (for example, no more than 20). |
|Semantic retrieval |Accepts a task request and performs semantic matching based on the calling intent and MCP tool descriptions, returning the most relevant tools.<br><br>If you use semantic retrieval mode, **tool indexing** fees are charged separately. You can review the billing granularity and reference prices first. For more information, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items). |The MCP toolset contains a large number of tools, and the caller is a general\-purpose agent. |
|Tag retrieval |Filters MCP tools accurately by specifying tags. Tags must be added to tools in the MCP toolset before use. |The MCP toolset contains a large number of tools, and the caller is a domain\-specific agent. |

## MCP protocol version

The MCP protocol version defines the message format, capability declaration, initialization method, and invocation behavior. Full return, semantic retrieval, and tag retrieval are tool matching methods provided by MCP toolsets and do not represent different MCP protocol versions. Clients should call tools/list and tools/call in the message format defined by the protocol version they are using. MCP toolsets are compatible with the following MCP protocol versions:

* **`2026-07-28`**

* **`2025-11-25`**

* **`2025-06-18`**

* **`2025-03-26`**

For more information about compatibility with MCP protocol version **`2026-07-28`** **,**  its stateless mechanism, and how to use Multi Round\-Trip Requests (MRTR), see [MCP protocol version compatibility](https://docs.byteplus.com/en/docs/agentkit/MCP_protocol_version_compatibility).

## Prerequisites

* An MCP service has been created. For more information, see [MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

* You are familiar with the billing items and descriptions for MCP toolsets. **The MCP Toolset is a paid feature**. Before you create an MCP toolset, we recommend that you review the relevant fees. For more information, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).

* (Optional) To access a VPC, make sure that BytePlus VPC has been activated and that a VPC and security group have been created in the region where you want to deploy the MCP service. For more information, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. Click "Create MCP toolset". Then, refer to the table below to configure the parameters. After configuration, click "Create" to complete the operation.

   |Parameter​ |Description |
   |---|---|
   |**Basic information** ||
   |MCP toolset name |Enter the name of the MCP toolset. The name cannot be modified after the MCP toolset is created. |
   |Associated gateway |Select the gateway type for the MCP toolset.<br><br><br>* **Dedicated gateway** (recommended): The MCP toolset runs on a gateway instance that you create separately. The resources are dedicated and cannot be shared, providing a stable capacity guarantee. This mode is suitable for production environments with high reliability requirements. After you select this option, specify an associated gateway instance. If no gateway instance is available, select "Create" from the drop\-down list to create one. For detailed operations, see [Creating gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances).<br><br>* **Share mode**: The MCP toolset runs on shared gateway resources provided uniformly by the platform. You do not need to create a gateway instance. In share mode, throttling limits such as QPS apply. This mode is suitable for proof\-of\-concept (POC) or low\-traffic testing scenarios. We do not recommend that you use this mode in production environments.<br><br><br>> **warning**<br><br><br>> After an MCP toolset is created, its associated gateway cannot be changed. Choose the associated gateway carefully based on your business scenario.<br> |
   |Access path |Configure the access path for the MCP toolset. The default access path is `/mcp`. |
   |**Network configuration** ||
   |Network access |When ** Associated gateway** is set to **Share mode**, you need to configure this parameter. In **dedicated gateway ** mode, the MCP toolset uses the network access configuration of the associated gateway instance.<br><br>Configure the network access method for the MCP toolset to specify networks of which types that can access the newly created MCP toolset.<br><br><br>* **Public network**: Select this option to allow access by external services such as Trae, Codex, and more. Public network is the default access method.<br><br>* **Private network**: Select this option to allow access by agents on AgentKit only. After configuration, the service is not externally accessible and is available only for internal use. Any VPC and subnet within the same region. A maximum of one subnet can be selected per availability zone. |
   |**Authentication information** ||
   |Inbound identity authentication |Configure the identity authentication method for the MCP toolset. Inbound identity authentication serves as the first security barrier for service access. It ensures that only authorized entities can call MCP toolsets and prevents unauthorized access, data leakage, and malicious attacks.<br><br><br>* **API Key**: After you enter a name, an API Key will be automatically created and associated with the MCP toolset. After the MCP toolset is created, you can view the API Key on the MCP toolset details page.<br><br>* **OAuth JWT**: Use the OAuth authorization mode to apply for an access token and call APIs. This mode enhances security and simplifies configuration. Before configuring this option, ensure that you have [created a user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) and [a client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en).<br><br><br>> **warning**<br><br><br><br>* > API Key and OAuth JWT are mutually exclusive authentication methods. You can only enable one method per MCP toolset.<br><br><br>* > Up to 1 inbound identity authentication configuration is supported in API Key mode. Up to 5 clients can be associated in OAuth JWT mode.<br> |
   |**Tool management** ||
   |Calling mode |When an agent calls a toolset, the toolset can return all tools or filter target tools via semantic matching or tag filtering.<br><br><br>* **Full return**: Returns all internal MCP tools directly after connecting to the MCP toolset. We recommend that you select this mode when the number of tools is small, for example, 20 or fewer.<br><br>* **Semantic retrieval**: Performs semantic matching based on the calling intent against tool descriptions and returns the best\-matching tools. We recommend that you select this mode when the number of tools is large and the caller is a general\-purpose agent. If you use semantic retrieval mode, **tool indexing** fees are charged separately. For more information, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).<br><br>* **Tag retrieval**: Filters required tools accurately based on tool tags. We recommend that you select this mode when the number of tools is large and the caller is a domain\-specific agent.<br><br>   > **warning**<br>   <br><br>   > Before using the "Tag retrieval" mode, make sure to add tool tags to the tools in the toolset. We recommend that you add no more than 10 tool tags to each tool.<br>    |
   |Tool |Add tools to the MCP toolset. Click the "Add tool" button and select one or more target tools from the MCP services. You can select and combine tools from multiple MCP services to meet your business needs.<br><br><br>* When Associated gateway is set to **Share mode**, you can select only MCP services that meet all of the following conditions: the gateway mode of the MCP service is Share mode, the inbound identity authentication method is API Key, and the network type is public network.<br><br>* When Associated gateway is set to **Dedicated gateway**, you can select only MCP services in the current gateway instance whose inbound identity authentication method is API Key. The network type is not restricted. Both public network and private network are supported. |
   |**Advanced configuration** ||
   |Associated project |Configure this parameter when **Associated gateway** is set to **Share mode**. When **Associated gateway** is set to **Dedicated gateway**, the associated project of the MCP toolset is the same as that of the associated gateway instance.<br><br>A project is a collection of resources. You can add the MCP toolset to a project and manage it centrally at the project level, which helps keep resources independent and maintain data security. For more information about projects, see [Managing projects](https://docs.byteplus.com/en/docs/agentkit/Managing_projects).<br><br><br>* By default, the project is default. Each resource can only belong to one project.<br><br>* After a project is selected, the created MCP toolset can only be used by users who have permission on that project. <br><br>* If no projects are available, you can click the "Create project" button to create one. After you create a project, return to this page to select the new project. |
   |tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources.<br><br>Click the "+ Add tag" button, select an existing tag or enter a new tag, and then associate the tag with the MCP toolset. For more information, refer to [Tag management](https://docs.byteplus.com/en/docs/agentkit/Tag_management).<br><br>> **tip**<br><br><br>> You can associate up to 20 tags per request and up to 50 tags with a single resource.<br> |

4. After creation, you can view the newly created MCP toolset in the MCP toolset list.

> **warning**

> After an MCP toolset is created, when a request is sent to the MCP toolset, the MCP toolset accesses the associated MCP service to call tools. The number of generated requests is **counted toward the usage statistics of both the MCP toolset and the MCP service**. For more information, see[Instructions on MCP request count](https://docs.byteplus.com/en/docs/agentkit/MCP_request_counting_rules?lang=en).
