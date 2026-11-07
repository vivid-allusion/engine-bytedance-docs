---
title: "Integrating existing MCP Servers into AgentKit Gateway"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_existing_MCP_Servers_into_AgentKit_Gateway"
---

As an enterprise developer who has deployed a self\-built or third\-party MCP Server (Model Context Protocol Server), you can use AgentKit to integrate your existing MCP Server as a backend service into the AgentKit MCP service centrally. This topic describes the complete process of integrating existing MCP Servers with AgentKit, covering connectivity verification, MCP service creation, MCP toolset configuration, agent code integration, and result checking.

## Scenario overview

When an enterprise has deployed a self\-built MCP Server (for example, an internal knowledge base retrieval or ticket system tool), or plans to integrate a third\-party MCP Server (for example, GitHub MCP, Notion MCP), AgentKit can be used to integrate these MCP Servers centrally, rather than having each agent connect directly to the backend endpoints.

The AgentKit Gateway forwards MCP requests without altering backend MCP protocol behavior and provides the following capabilities at the entry layer:

* **Unified inbound authentication:**  Adds unified access control for MCP services to prevent direct exposure of backend endpoints.

* **Unified tool discovery:**  Centrally manages tool entry points via MCP toolsets, reducing configuration costs in multi\-agent scenarios.

## Core concepts

### Streamable HTTP

Streamable HTTP is a transmission method for MCP, based on HTTP requests carrying JSON\-RPC (JSON Remote Procedure Call) messages, and supports returning results in a streaming manner.

In this topic, the backend MCP Server needs to provide a Streamable HTTP endpoint that can be called by the AgentKit Gateway, such as `https://your-mcp-server.internal:8080/mcp/v1` (the path can be customized).

### tools/list and tools/call

* tools/list: Used to enumerate the tool list provided by the backend MCP Server, returning the `result.tools` array.

* tools/call: Used to call a specific tool, usually containing the tool name and input parameters, such as ` {"query": "xxx"}`）。

### MCP toolset

An MCP toolset is used for organizing, retrieving, and managing authorization of tools within AgentKit.

* The Gateway transparently forwards the tools/list response from the existing backend MCP Server to the platform side.

* In AgentKit, you can associate MCP services with an MCP toolset to centrally orchestrate and manage tools.

## Prerequisites

* The AgentKit service has been activated. If AgentKit is not activated, log in to the[ AgentKit console ](https://console.byteplus.com/AgentKit)and follow the system prompts to complete the operations.

* The agent has been created via [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) and released to the AgentKit console agent runtime. For details, refer to [Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en).

* The existing MCP Server is running normally, and the backend must implement **a Streamable HTTP** transport endpoint for the MCP protocol that can respond to tools/list and tools/call requests, such as: `https://your-mcp-server.internal:8080/mcp/v1`.

* An accessible network environment is available where the AgentKit Gateway can access the existing MCP Server address.

   > **tip**

   > The AgentKit Gateway currently does not support private IP addresses as backends. We recommend using the following two methods for network connectivity.

   * **Same VPC**: subnets within the same VPC (Virtual Private Cloud) are, by default, interconnected and can be accessed directly via the private network.

   * **Cross VPC**: For  cross\-VPC scenarios, PrivateLink can be used to enable network communication between VPCs. For detailed procedures, see [Implementing private access between VPCs across accounts](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03).

   * **Public domain name**: Outbound policy needs to be configured for public domain names. You can configure a NAT Gateway for the VPC where the existing MCP Server resides. For details, see [Accessing public network via SNAT](https://docs.byteplus.com/en/docs/natgateway/Accessing-the-internet-using-SNAT) and [Providing services to public network via DNAT](https://docs.byteplus.com/en/docs/natgateway/Providing-services-over-the-internet-using-DNAT).

* The outbound credential is ready. The existing MCP Server is used as the backend service. You need to prepare an API Key/Token in advance as the outbound credential for the MCP service in AgentKit (for example, `Authorization: Bearer <token>` or a custom Header).

* (Optional) A gateway instance has been created. This topic provides an example on how to use **Share mode** to create an MCP service and an MCP toolset. For production environments, we recommend that you select the **Dedicated gateway** mode. You need to create a gateway instance in advance. For details, see [Creating enterprise gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances?lang=en).

## Precaution

* AgentKit Gateway only supports Streamable HTTP transport for MCP protocol versions 2025\-03\-26 and later. **Direct integration with MCP Servers using stdio transport or SSE‑only (Server‑Sent Events) is not supported.**  To integrate such servers, first use mcp‑proxy or equivalent tools to wrap the stdio process or SSE‑only service into a ** Streamable HTTP ** endpoint, then follow the procedures in this topic for integration.

* If you integrate an existing third‑party MCP Server (for example, GitHub MCP or Notion MCP), extra attention is required to ensure that the AgentKit Gateway can access the third\-party public domain name and that outbound security groups and proxy policies allow the AgentKit Gateway access requests.

## Procedure

In the following section, enterprise self\-built internal MCP Servers are taken as an example to describe the complete process for integrating existing MCP Servers into the AgentKit MCP service. In the actions described in this topic, we assume that you have ** 2 ** self\-hosted internal MCP Servers, both deployed on third\-party clouds (such as Alibaba Cloud). Network connectivity is established by accessing the backend services (the self\-hosted internal MCP Servers) over the public network.

### Step 1: Verify the connectivity of an existing MCP Server

Send a tools/list request to the Streamable HTTP endpoint of the existing MCP Server to verify network connectivity and protocol availability. The sample request code is as follows:

```Python
curl -i -N --max-time 20 \
  -X POST 'https://<mcp server url>' \
  -H 'Authorization: Bearer <apikey>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  --data-raw '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/list",
    "params": {
      "protocolVersion": "2025-11-25",
      "capabilities": {},
      "clientInfo": {
        "name": "curl-mcp-smoke-test",
        "version": "1.0.0"
      }
    }
  }'
```

**Parameter configuration table**

|**Parameter​**  |**Description** |**Sample value** |
|---|---|---|
|`<mcp server url>` |Replace the value with the endpoint of the existing MCP Server, which can be obtained from the basic information of the MCP Server. The `BytePlus` MCP service is taken as an example. Other MCP services are similar: |https://s8u4ei27vq8gixxxxxx.apigateway\-xx\-xxxx.comtest/mcp |
|`<apikey>` |Replace the value with the API Key information of the existing MCP Server, which can be obtained in the basic information. The `BytePlus` MCP service is taken as an example.  |O0omgYOtt6\-DseOtxxxxxx |
|`Content-Type` |The request body is JSON. |application/json |
|`jsonrpc` |The JSON\-RPC protocol version. |2.0 |
|`method` |The name of the calling method. |tools/list |
|`id` |The request identifier, used to match the response. |1 |

The existing MCP Server is accessible if it returns a JSON\-RPC response that contains a result.tools array. If a timeout, connection refusal, or a `5xx` error occurs, first troubleshoot the network, the path, and the status of the existing MCP Server before proceeding with subsequent operations.

### Step 2: Create an MCP service and configure inbound and outbound authentication

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Gateway \> MCP integration". On the "MCP Service" tab, click "Create MCP service".

3. Specify parameters based on the following table.

   > **tip**

   > The following table describes only the parameters required for this procedure. For more parameters and descriptions, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

   * **Basic information**

      |Parameter​ |Description |
      |---|---|
      |Term |Enter the name of the MCP service. After creation, you cannot change the MCP service name. Here, the name is **mcp_service_n5z3e0jb**. |
      |Associated gateway |Select the gateway type for the MCP service. Select **Share mode** in this example.<br><br><br>* **Dedicated gateway** (recommended): The MCP service runs on a gateway instance that you independently create. Resources are dedicated and not shared, ensuring stable capacity.<br><br>* **Share mode**: The MCP service runs on shared gateway resources provided uniformly by the platform. You do not need to create a gateway instance.<br><br><br>> **warning**<br><br><br>> **Share mode** is only used for illustration purposes. In actual production environments, use **Dedicated gateway**.<br> |
      |Access method |Select the method for accessing the MCP service. Select **Import MCP service** in this example. |
      |Protocol |Currently, only the ** Streamable HTTP** protocol is supported. |
      |Access path |Specify the access path of the newly created MCP service. For simplicity, the default access path `/mcp` is used here. |

   * **Network configuration**

      |Parameter​ |Description |
      |---|---|
      |Network configuration |Configure the network access method for the MCP service to specify networks of which types that can access the newly created MCP service. Select **Public network** and **Private network**, select the **Default** VPC, and the **Subnet\-KBA0** subnet.<br><br>> **warning**<br><br><br>> Currently, MCP toolsets do not support adding MCP services with only "Private network" enabled. If you need to expose tools within an MCP service from an MCP toolset via a private network, enable public network access at the same time. Select both **Public network** and**Private network**.<br><br><br><br>* **Public network**: Select this option to allow access by external services such as Trae, Codex, and more. Public network is the default access method.<br><br>* **Private network**: Select this option to allow access by agents on AgentKit only. After configuration, the service is not externally accessible and is available only for internal use. Any VPC and subnet within the same region. A maximum of one subnet can be selected per availability zone. |

   * **Authentication information**

      |Parameter​ |Description |
      |---|---|
      |Inbound identity authentication |Configure the identity authentication method for the MCP service. The configuration here is ** API Key / apikey_xfj5ew80** (automatically generated by the system).<br><br>Inbound identity authentication serves as the first security barrier for service access. It ensures that only authorized entities can call MCP services and prevents unauthorized access, data leakage, and malicious attacks.<br><br><br>* **API Key**: After you enter a name, an API Key will be automatically created and associated with the MCP service. After the MCP service is created, you can view the API Key on the MCP service details page.<br><br>* **OAuth JWT**: Use the OAuth authorization mode to apply for an access token and call APIs. This mode enhances security and simplifies configuration. Before configuring this option, ensure that you have [created a user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) and [a client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en).<br><br><br>> **warning**<br><br><br>> Enable inbound authentication for all MCP services in the production environment. An MCP endpoint with inbound authentication disabled is equivalent to exposing internal business APIs to the public network, which may be accessed without authorization, resulting in unauthorized access, privilege escalation, and data leakage risks.<br> |

   * **Backend configuration**

      |Parameter​ |Description |
      |---|---|
      |Service type |Configure the backend service (existing MCP Server) to be connected to the MCP service. In the actions described in this topic, the existing MCP Server is deployed on a third\-party cloud and accessed over the public network. Therefore, the configuration here is: **Fixed domain name**, which means accessing the backend MCP Server via its domain name over the public network.<br><br><br>* **veFaaS**: The existing MCP Server is deployed on BytePlus veFaaS.<br><br>* **VKE**: The existing MCP Server is deployed on BytePlus VKE.<br><br>* **ECS**: The existing MCP Server is deployed on BytePlus ECS.<br><br>* **Fixed domain name**: The existing MCP Server is exposed to the public network and can be accessed directly via its domain name. |
      |Domain name |Configure the URL of the first MCP Server used as a backend service. You do not need to change the port number. The default port for the HTTP protocol is 80, and the default port for the HTTPS protocol is 443. |
      |Outbound credential |Configure the outbound authorization for the MCP service to allow the agent to use this credential to access downstream resources. Here, configure **API Key / agentkit_model_key**. This API Key is newly added, and its configuration information is the API Key information of the existing MCP Server prepared in the "Prerequisites".<br><br><br>* **Add API Key**:<br><br>   1. In the API Key drop\-down list, click the "Add" button at the bottom.<br><br>   2. Refer to the image below to configure the API Key information and create an API Key named **agentkit_model_key**. The outbound credential used in this topic is the API Key `Authorization: Bearer sk-abc123`. Enter the corresponding information as follows:<br><br>      * **API Key:**  sk\-abc123<br><br>      * **Location:**  Header<br><br>      * **Parameter Name:**  Authorization<br><br>* **Outbound credential type**<br><br>   * **API Key**: Applicable to external services that use fixed keys for authentication.<br><br>   * **OAuth Client**: Applicable to downstream services that require authentication through the OAuth 2.0 process.<br><br>      * "OAuth Client (M2M)" access credentials are supported only when "Inbound identity authentication" is set to "API Key".<br><br>      * "OAuth Client (M2M)" and "OAuth Client (USER_FEDERATION)" access credentials are supported only when "Inbound identity authentication" is set to "OAuth JWT". |

4. Click the "Create" button to complete the creation of the first AgentKit MCP service that connects to the existing MCP Server.

5. Refer to steps 2 through 4 above to complete the creation of the second AgentKit MCP service that connects to the existing MCP Server.

   * **Basic information**

      |Parameter​ |Description |
      |---|---|
      |Term |Enter the name of the MCP service. Here, the name is **mcp_service_j3hrfb4m**. |
      |Associated gateway |Select the gateway type for the MCP service. Select **Share mode** in this example. |
      |Access method |Select the method for accessing the MCP service. Select **Import MCP service** in this example. |
      |Protocol |Currently, only the ** Streamable HTTP** protocol is supported. |
      |Access path |Keep the default access path `/mcp`. |

   * **Network configuration**

      |Parameters |Description |
      |---|---|
      |Network configuration |Configure the network access method for the MCP service. Here, select  **"Public network" and "Private network", the "Default" VPC, and the "Subnet\-KBA0" subnet**. |

   * **Authentication information**

      |Parameter​ |Description |
      |---|---|
      |Inbound identity authentication |Configure the identity authentication method for the MCP service. The configuration here is ** API Key / apikey_skrgvbq7** (automatically generated by the system).<br><br>> **warning**<br><br><br>> Enable inbound authentication for all MCP services in the production environment. An MCP endpoint with inbound authentication disabled is equivalent to exposing internal business APIs to the public network, which may be accessed without authorization, resulting in unauthorized access, privilege escalation, and data leakage risks.<br> |

   * **Backend configuration**

      |Parameter​ |Description |
      |---|---|
      |Service type |Configure the type of backend service (existing MCP Server) to be connected to the MCP service. Here, select **Fixed domain name**. |
      |Domain name |Configure the URL of the second MCP Server used as a backend service. You do not need to change the port number. |
      |Outbound credential |Configure the outbound authentication of the MCP service. Here, configure **API Key / inspection_api_key**. This API Key is newly added, and its configuration information is the API Key information of the existing MCP Server prepared in the "Prerequisites".<br><br>**The procedure for adding an API Key is as follows**:<br><br><br>   1. In the API Key drop\-down list, click the "Add" button at the bottom.<br><br>   2. Refer to the image below to configure the API Key information and create an API Key named **agentkit_model_key**. The outbound credential used in this topic is the API Key `Authorization: Bearer sk-abc456`. Enter the corresponding information as follows:<br><br>      * **API Key: ** sk\-abc456<br><br>      * **Location:**  Header<br><br>      * **Parameter Name:**  Authorization |

6. After you create the MCP services, you can view the **MCP access endpoint** for each service under the "Basic information" tab of the newly created MCP services.

### Step 3: Configure the MCP toolset

> **warning**

* > This step is **optional**. Scenario descriptions are as follows:

   * > **Required**: Create an agent and integrate tools converted from REST API/OpenAPI into the agent in the AgentKit console.

   * > **Optional**: You can skip this step in either of the following scenarios: Integrate tools converted from REST API / OpenAPI into the agent via VeADK; if the number of exposed MCP tools in the MCP service is small, there is no need to use an MCP toolset for category management.

* > **Since this topic involves two MCP services, MCP toolset configuration is required for easier tool management.**

1. In the left navigation pane, click "Gateway \> MCP integration". On the "MCP Toolset" tab, click "Create MCP toolset".

2. On the Create MCP toolset page, refer to the table below to complete the configuration.

   |Parameter​ |Description |
   |---|---|
   |**Basic information** ||
   |MCP toolset name |Enter the name of the MCP toolset. After creation, you cannot change the MCP toolset name. Here, the name is ** mcp_toolset_doc**. |
   |Associated gateway |Select the gateway type for the MCP toolset. Select **Share mode** in this example. |
   |Access path |Configure the access path for the MCP toolset. The default access path is `/mcp`. Here, the default value is retained. |
   |**Network configuration** ||
   |Network configuration |Configure the network access method for the MCP toolset to specify networks of which types that can access the newly created MCP toolset. Configure this section identically to the configurations of the MCP service: **select "Public network" and "Private network", the "Default" VPC, and the "Subnet\-KBA0" subnet**.<br><br>> **warning**<br><br><br>> The network configurations of the MCP service and MCP toolset are independent and do not affect each other.<br><br><br>> The network configuration for an MCP service defines which types of networks can access the service, while the network configuration for an MCP toolset defines which types of networks can access the toolset. This means the agent can directly call tools within the MCP service via access methods permitted by the service. It can also call tools added to the toolset through access methods permitted by the MCP toolset.<br> |
   |**Authentication information** ||
   |Inbound identity authentication |Configure the identity authentication method for the MCP toolset. Inbound identity authentication serves as the first security barrier for service access. It ensures that only authorized entities can call MCP services and prevents unauthorized access, data leakage, and malicious attacks. Here, configure **API Key / apikey_0zr88gxy** (automatically generated by the system).<br><br><br>* **API Key**: After you enter a name, an API Key will be automatically created and associated with the MCP service. After the MCP service is created, you can view the API Key on the MCP service details page.<br><br>* **OAuth JWT**: Use the OAuth authorization mode to apply for an access token and call APIs. This mode enhances security and simplifies configuration. Before configuring this option, ensure that you have [created a user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) and [a client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en).<br><br><br>> **warning**<br><br><br><br>* > API Key and OAuth JWT are mutually exclusive authentication methods. You can only enable one method per MCP toolset.<br><br><br>* > Up to 1 inbound identity authentication configuration is supported in API Key mode. Up to 5 clients can be associated in OAuth JWT mode.<br> |
   |**Tool management** ||
   |Calling mode |When an agent calls a toolset, the toolset can return all tools or filter target tools via semantic matching or tag filtering. Since the number of tools used in this operation is small, the configuration here is **Full return**.<br><br><br>* **Full return**: Returns all internal MCP tools directly after connecting to the MCP toolset. We recommend that you select this mode when the number of tools is small, for example, 20 or fewer.<br><br>* **Semantic retrieval**: Performs semantic matching based on the calling intent against tool descriptions and returns the best\-matching tools. We recommend that you select this mode when the number of tools is large and the caller is a general\-purpose agent.<br><br>* **Tag retrieval**: Filters required tools accurately based on tool tags. We recommend that you select this mode when the number of tools is large and the caller is a domain\-specific agent. |
   |Tool |Add tools to the MCP toolset. Click the "Add tool" button and select one or more target tools from the MCP services. You can select and combine tools from multiple MCP services to meet your business needs.<br><br>Here, select all tools under the two MCP services created in the previous step (**mcp_service_n5z3e0jb** and **mcp_service_j3hrfb4m**). In other words, after the tools of the enterprise's existing self\-built MCP Server have been connected to AgentKit, the agent only needs to connect to this MCP toolset to call these tools in a unified manner. |

3. Click the "Create" button to complete MCP toolset creation. A successful result is shown below.

   * In the "MCP tool" tab of the newly created MCP toolset, you can see the tools selected during creation.

   * In the "Test" tab of the newly created MCP toolset, follow the on\-screen instructions to test the toolset.

      * Step 1: Click the "Connect test" button.

      * Step 2: From the tools integrated with the MCP Server, select one for testing.

      * Step 3: Enter the required parameters and click the "Testing tool" button.

**At this point, you have integrated your enterprise's existing self\-built MCP Servers into AgentKit, and the tools from these servers are now available in the AgentKit MCP toolset. The next step is to integrate the MCP toolset into an agent. After integration, the agent can call these tools in a unified manner without the need to connect to each MCP Server individually.**

### Step 4: Integrate the MCP toolset into the agent code and verify

Here, the MCP toolset is integrated into the agent built with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en). This is to connect to the MCP endpoint exposed by the AgentKit gateway in the agent code and carry inbound credentials to complete tool discovery and calls.

1. In the "Basic information" tab of the MCP toolset **mcp_toolset_doc**, obtain the MCP toolset URL and inbound identity authentication API Key.

2. Under "API Access Key" in the [IAM console](https://console.byteplus.com/iam/keymanage), click the "Create Access Key" button to create an Access Key. After creation, copy the Access Key ID (AK) and Secret Access Key (SK).

3. The structure of your locally built VeADK agent project is as follows. You need to add AK/SK information and MCP toolset information for the agent.

   * **Project structure**

      ```Plain Text
      your_project
      ├── __init__.py 
      ├── .env 
      └── agent.py
      ```

   * **Set environment variables in the local environment**

      Execute the following command in your local terminal to set environment variables for the AK/SK credentials.

      > **warning**

      > Since AK/SK are highly sensitive credentials, directly writing them into static configuration files, such as `.env`, poses a security risk. When you configure AK/SK in the local development environment, we recommend managing them by exporting session\-level environment variables in the terminal.

      ```Bash
      # The platform AK and SK.
      export BYTEPLUS_ACCESS_KEY=<your_access_key>
      export BYTEPLUS_SECRET_KEY=<your_secret_key>
      ```

   * **Configure environment variables in **  **`.env`**

      1. In the virtual environment where the agent was created, execute `cd <project root directory>` to enter the project root directory.

      2. Execute `vim .env` to open the `.env` file.

      3. Press the` i` key to enter edit mode. In the  **`.env`** file, enter the following content to add the MCP toolset configuration.

         ```Bash
         TOOL_MCP_ROUTER_URL=<tool_mcp_router_url>
         TOOL_MCP_ROUTER_API_KEY=<tool_mcp_router_api_key>
         ```

         |Parameter​ |Source |
         |---|---|
         |<tool_mcp_router_url\> |`url` in the MCP toolset sample call. |
         |<tool_mcp_router_api_key\> |`Authorization` in the MCP toolset sample call. |

      4. Press the `esc` key to exit edit mode, and enter `:wq` to save and exit the file.

### Step 5: Verify the result

1. **Local test**.

   1. When you query the MCP tools that the agent can call, you can see that the returned tool list is consistent with the tools selected in the MCP toolset and the tools of the enterprise's existing MCP Server.

   2. Push local data online.

      1. Execute the `source .venv/bin/activate `command in the local terminal to reactivate the VeADK virtual environment. If you are already in the VeADK virtual environment, skip this step.

      2. Execute the `cd <Project directory>` command to enter the root directory of the agent project.

      3. Execute the` agentkit launch `command to deploy the agent to the AgentKit agent runtime.

2. **Online test**.

   1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).  In the agent runtime list, click "Online test" in the Actions column of the target agent.

## Troubleshooting

|**Symptoms** |**Possible causes** |**Repair suggestion** |
|---|---|---|
|tools/list returns an empty result |The existing MCP Server (backend service) contains no tools, or the AgentKit Gateway cannot connect to the backend service. |Check whether the backend service domain name or IP address configured when you create the MCP service in AgentKit is correct. |
|Gateway returns 500/503 |The existing MCP Server (backend service) did not respond or crashed |Check whether the status of the backend service is **Running**. |
|Backend returns 401 (outbound) |Invalid or expired outbound credential |Update the credential value in the Credential Provider; confirm that Prefix and ParameterName are consistent with the existing MCP Server. |
