---
title: "Integrating MCP services with gateway instances via private network domain names"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_MCP_services_with_gateway_instances_via_private_network_domain_names"
---

This topic describes how to integrate an existing HTTP service with an AgentKit agent through MCP when the backend service (MCP Server) is not publicly accessible. In this scenario, the MCP Server is reachable only through a domain name on the private network. Follow the steps in this topic to complete the integration.

## Application scenarios

* The MCP Server is deployed in a VPC, an enterprise IDC, or a private network environment on a third\-party cloud.

* The MCP Server is accessible internally through a private domain name.

* You need to use an AgentKit dedicated gateway as a unified MCP service entry and complete the calls within the private network security boundary.

## Solution overview

In this topic, the backend workload is deployed in a VPC on a third\-party cloud (such as Tencent Cloud), and the backend is exposed internally through a private domain name in Tencent Cloud Private DNS. You now need to use this private domain name as the MCP service backend in AgentKit and associate the MCP service with the AgentKit dedicated gateway.

In the preceding scenario, you need to use the AgentKit dedicated gateway to handle MCP requests, access the backend service through a private network egress, and resolve the target domain name through private DNS forwarding. During implementation, you can understand the process in four layers: the ** dedicated gateway entry**, **MCP service mapping**, **private network connectivity**, and ** private DNS resolution**. Only after all four layers are configured can the agent call the backend capabilities reliably.

|**Level** |**Required configuration** |**Target** |
|---|---|---|
|Dedicated gateway |Create a dedicated gateway that supports private network access and associate the VPC and subnet used for inbound and outbound traffic.<br><br><br>1. When you configure a private domain name for an MCP service on the dedicated gateway, specify the VPC and subnet.<br><br>2. Call the SpaceNetwork APIs to configure its private VPC egress. The egress must match the VPC and subnet configuration associated with the dedicated gateway. |Provides a unified access entry and defines the basic network boundary. As a result, when the gateway initiates outbound access to the specified private domain name, traffic can enter the BytePlus VPC and then reach the connected Tencent Cloud network environment. |
|MCP service |Access the backend service through a fixed domain name and set the network type to "Private network". |Map the backend APIs to MCP tool capabilities that agents can call. |
|Private network |Connect the routes and security policies between the network where the dedicated gateway resides (BytePlus) and the network where the backend resides (Tencent Cloud).<br><br>The VPC for AgentKit private outbound traffic under the BytePlus account communicates with the Tencent Cloud service VPC over a private network through TR/CEN and a dedicated connection. |Ensure that the outbound traffic of the AgentKit dedicated gateway can reach the private IP address of the Tencent Cloud business Server. |
|Private network DNS |Forward the resolution requests for the target private domain name to the authoritative DNS or the inbound DNS endpoint.<br><br><br>1. In Tencent Cloud Private DNS, create an inbound endpoint and record the inbound service IP address and the DNS port.<br><br>2. Call the related SpaceNetwork APIs to configure the IP address and port of the Tencent Cloud inbound endpoint as the resolution target for the corresponding private domain name. |Ensure that when AgentKit resolves the target private domain name on the BytePlus side, it can forward DNS queries to Tencent Cloud Private DNS. |

## Prerequisites

1. **You have completed the network preparation.**

   * **You have established network connectivity between the BytePlus VPC where the dedicated gateway resides and the VPC where the backend resides.**  In the example provided by this topic, the service is deployed on Tencent Cloud. Before you start the configuration, first establish private network connectivity between the BytePlus VPC and the Tencent Cloud VPC. This topic does not cover network connectivity operations. For detailed configuration, see [Direct Connect - Best practices](https://docs.byteplus.com/en/docs/directconnect/best-practices-overview?lang=en).

   * **You have allowed the business ports and the UDP/TCP port 53 that DNS requires** (if you use a custom DNS port, use the actual port). For the procedure in this topic, you need to create a Tencent Cloud Private DNS inbound endpoint. In the "Internal resolution/Service address" section of Tencent Cloud Private DNS, create an inbound endpoint, select the Tencent Cloud VPC already connected to the BytePlus VPC, and record the inbound service IP address. As per the standard, DNS uses port 53. We recommend allowing both UDP 53 and TCP 53. For configuration details, see [Private DNS service address](https://cloud.tencent.com/document/product/1338/123753) in the Tencent Cloud official documentation.

      > **tip**

      > If your business Server or DNS is deployed on Alibaba Cloud, the configuration approach is the same as for Tencent Cloud: create a PrivateZone inbound endpoint, record the inbound traffic service IP, and make sure that the security group allows traffic on port 53. For configuration details, see[Inbound endpoint](https://help.aliyun.com/zh/dns/pvtz-inbound-endpoint)in the Alibaba Cloud official documentation.

   * **You have completed the network planning for the AgentKit dedicated gateway.**  Determine the region and project for the dedicated gateway and MCP service that you will create later, as well as the VPC and subnet that support private network access.

2. **You have confirmed the actual backend service information.**

   * Prepare the backend private domain name (such as mcp\-api.example.internal), port, MCP path, and credentials, and configure the security group rules on the Tencent Cloud side that allow access to this backend.

   * The backend service runs properly, and the backend must implement the ** Streamable HTTP** transport endpoint of the MCP protocol and be able to respond to tools/list and tools/call requests.

   * Prepare the backend service API Key/Token in advance as the outbound credential for the MCP service in AgentKit (for example, `Authorization: Bearer <token>` or a custom Header).

3. **The AgentKit service has been activated**. If AgentKit is not activated, log in to the [AgentKit console](https://console.byteplus.com/AgentKit) and follow the system prompts to complete the operations.

4. The agent has been built with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) and published to the agent runtime in the AgentKit console. For details, refer to [Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en).

## Procedure

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
|`<mcp server url>` |Replace the value with the endpoint of the existing MCP Server, which can be obtained from the basic information of the MCP Server. The `BytePlus` MCP service is taken as an example.  |https://s8u4ei27vq8gixxxxxx.apigateway\-xx\-xxxx.comtest/mcp |
|`<apikey>` |Replace the value with the API Key information of the existing MCP Server, which can be obtained in the basic information. The `BytePlus` MCP service is taken as an example. Other MCP services are similar:<br><br>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d2557438177b06f3cea534e6f8e257af.png) |O0omgYOtt6\-DseOtxxxxxx |
|`Content-Type` |The request body is JSON. |application/json |
|`jsonrpc` |The JSON\-RPC protocol version. |2.0 |
|`method` |The name of the calling method. |tools/list |
|`id` |The request identifier, used to match the response. |1 |

The existing MCP Server is accessible if it returns a JSON\-RPC response that contains a result.tools array. If a timeout, connection refusal, or a `5xx` error occurs, first troubleshoot the network, the path, and the status of the existing MCP Server before proceeding with subsequent operations.

### Step 2: Create a gateway instance

A gateway instance is a dedicated gateway resource in AgentKit that provides a unified access entry for resources such as model services, MCP services, and MCP toolsets. Enterprise gateway instances are suitable for production environments or business scenarios that require independent capacity, resource isolation, centralized management of access entries, and separate billing.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, click "Create gateway".

3. On the creation page, configure the parameters as described in the following table.

   |Parameter​ |Description |
   |---|---|
   |**Basic information** ||
   |Instance name |Enter a name for the gateway instance. In this example, the name is **prod_mcp_gateway**.<br><br><br>* After the gateway instance is created, you can modify its name in the "Configuration information" section of the instance.<br><br>* We recommend that the instance name reflect the business, environment, and purpose. |
   |Billing method |Select the billing method for the gateway instance. Currently, only **Pay\-as\-you\-go** is supported. |
   |Gateway type |Select the gateway instance type. You can create only one gateway instance of each type. In this example, select **MCP gateway**. You can use MCP gateway to connect MCP resources (MCP services and MCP toolsets). |
   |**Specification configuration** ||
   |Gateway specification |Select the specification for the gateway instance. In this example, select **gateway_small_x2**.<br><br><br>* Different specifications support different resource limits, such as **QPS ** and the ** number of client connections**, and are charged at different fees. Select an appropriate specification to avoid affecting your business.<br><br>* For the fees of different specifications, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items). |
   |**Network configuration** ||
   |Availability zone |Select the availability zones where the gateway instance is deployed. To ensure high availability of the gateway instance, select at least two availability zones.<br><br><br>* Availability zone selection is required regardless of whether private network access is enabled.<br><br>* If private access is enabled, select subnets in the corresponding availability zones. |
   |Inbound access |Select the inbound access method for the gateway instance. In this example, select **Private network** and **Public network**. For the associated VPC and subnets, select the **VPC and subnets that have been connected to the Tencent Cloud network.** <br><br><br>* **Configuration instructions**<br><br>   * After the gateway instance is created, you cannot change the network access method.<br><br>   * **Public network** and ** Private network ** are supported. Configure at least one access method. You can also configure both access methods at the same time.<br><br>* **Available methods**<br><br>   * **Public network**: Callers are in the public network environment or need to access the gateway instance across networks. Examples include local development and debugging or cross\-VPC and cross\-environment access when Direct Connect or private network connectivity is unavailable.<br><br>   * **Private network**: Callers reside within a VPC in the same region or have network connectivity to the VPC via Direct Connect, VPN, CEN, or other methods, and traffic must stay within the private network.<br><br>      * **VPC**: Select the VPC for the gateway instance. We recommend that you select a VPC and subnets that are in the same region and under the same network plan as your main callers and backend resources.<br><br>      * **Subnet**: Select available subnets under the selected VPC. Select one subnet in each availability zone to ensure high availability of your service.<br><br><br>> **tip**<br><br><br>> If your callers reside in both the public network and the private network, you can enable both public network access and private network access. For example, developers perform development and debugging over the public network, and production services make calls within a VPC. We recommend that you prioritize private network access for production traffic and use public network access only for development and debugging or emergency use.<br> |
   |**Observability configuration** ||
   |Torch Log Service |Specifies whether to enable Torch Log Service (TLS) for the gateway instance. After TLS is enabled, you can view the service logs of the gateway instance to troubleshoot issues such as failures, abnormal requests, and runtime errors. In this example, this parameter is set to ** Enabled**.<br><br><br>* **Log feature**: If you do not want to enable this feature, you can manually uncheck the Torch Log Service checkbox. For more information, see [Viewing logs](https://docs.byteplus.com/en/docs/agentkit/Viewing_logs).<br><br>* **Log billing**: After you enable the log service, the platform activates the TLS service for you. **Using the log service incurs fees. For more information, see the ** [log billing instructions](https://docs.byteplus.com/en/docs/tls/billable_items?lang=en) **.**  |
   |Log project |Configure this parameter only after you enable Torch Log Service. Select the project to which the gateway instance logs are written. Under this log project, the gateway instance automatically generates a log topic named **agentkit\-gateway\-access\-log**. |
   |**Advanced configuration** ||
   |Associated project |A project is a collection of resources. You can add a new gateway instance to a project and manage it centrally at the project levellevel. This helps keep resources independent and maintain data security. For more information about projects, see [Managing projects](https://docs.byteplus.com/en/docs/agentkit/Managing_projects).<br><br><br>* By default, resources are associated with the **default** project. Each resource can belong to only one project.<br><br>* After you select a project, only users who have permissions on the project can use the created gateway instance. <br><br>* If no projects are available, you can click the "Create project" button to create one. After you create a project, return to this page to select the new project. |

4. In the ** Configuration details ** and ** Cost details** areas on the right side of the page, confirm the specification, gateway type, inbound access method, and fee items for the current configuration. Read and select the "I have read and agree xxx" checkbox, and then click "Buy now" to complete the operation.

### Step 2: Create an MCP service

1. On the Gateway instance page, click the name of the newly created gateway instance.

2. On the MCP tab, in the MCP Service section, click "Create MCP service".

3. Specify parameters based on the following table.

   > **tip**

   > The following table describes only the parameters required for this procedure. For more parameters and descriptions, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

   * **Basic information**

      |Parameter​ |Description |
      |---|---|
      |Term |Enter the name of the MCP service. After creation, you cannot change the MCP service name. In this example, the name is **mcp_service_fgajjno5**. |
      |Associated gateway |Select the gateway type for the MCP service. In this example, select **Dedicated gateway**. By default, the system selects the current dedicated gateway **prod_mcp_gateway**.<br><br><br>* **Dedicated gateway**: The MCP service runs on a gateway instance that you create separately. The resources are dedicated and cannot be shared, providing stable capacity assurance.<br><br>* **Share mode**: The MCP service runs on shared gateway resources provided by the platform. You do not need to create a gateway instance. |
      |Access method |Select the method for accessing the MCP service. Select **Import MCP service** in this example. |
      |Protocol |Currently, only the ** Streamable HTTP** protocol is supported. |
      |Access path |Specify the access path of the newly created MCP service. For simplicity, the default access path `/mcp` is used here. |

   * **Authentication information**

      |Parameter​ |Description |
      |---|---|
      |Inbound identity authentication |Configure the identity authentication method for the MCP service. In this example, the configuration is **API Key / apikey_f2ti3mtv** (automatically generated by the system).<br><br>Inbound identity authentication serves as the first security barrier for service access. It ensures that only authorized entities can call MCP services and prevents unauthorized access, data leakage, and malicious attacks.<br><br><br>* **API Key**: After you enter a name, an API Key will be automatically created and associated with the MCP service. After the MCP service is created, you can view the API Key on the MCP service details page.<br><br>* **OAuth JWT**: Use the OAuth authorization mode to apply for an access token and call APIs. This mode enhances security and simplifies configuration. Before configuring this option, ensure that you have [created a user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) and [a client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en).<br><br><br>> **warning**<br><br><br>> Enable inbound authentication for all MCP services in the production environment. An MCP endpoint with inbound authentication disabled is equivalent to exposing internal business APIs to the public network, which may be accessed without authorization, resulting in unauthorized access, privilege escalation, and data leakage risks.<br> |

   * **Backend configuration**

      |Parameter​ |Description |
      |---|---|
      |Service type |Configure the backend service (existing MCP Server) to be connected to the MCP service. In the actions described in this topic, the existing MCP Server is deployed on Tencent Cloud and is accessed over a private network. This means you access the MCP Server by using the backend service MCP Server domain name over the private network. In this example, set this parameter to **Fixed domain name.** <br><br><br>* **veFaaS**: The existing MCP Server is deployed on BytePlus veFaaS.<br><br>* **VKE**: The existing MCP Server is deployed on BytePlus VKE.<br><br>* **ECS**: The existing MCP Server is deployed on BytePlus ECS.<br><br>* **Fixed domain name**: The existing MCP Server is exposed to the public network and can be accessed directly via its domain name. |
      |Network types |Select the network access type of the MCP service. In this example, select **Private network**.<br><br>In private network access scenarios, an MCP service uses the inbound VPC of its associated gateway instance as the private network egress by default. |
      |Domain name |Configure the URL of the first MCP Server used as a backend service. You do not need to change the port number. The default port for the HTTP protocol is 80, and the default port for the HTTPS protocol is 443. |
      |Outbound credential |Configure the outbound authorization for the MCP service to allow the agent to use this credential to access downstream resources. In this example, configure ** API Key / inspection_api_key**. This is a newly added API Key, and its configuration is the backend service API Key information prepared in "Prerequisites".<br><br><br>* **Add API Key**:<br><br>   1. In the API Key drop\-down list, click the "Add" button at the bottom.<br><br>   2. Configure the API Key information as shown in the following figure, create an API Key named **inspection_api_key**, and then click "Confirm" to save. The outbound credential used in this topic is the API Key `Authorization: Bearer sk-abc123`. Enter the corresponding information as follows:<br><br>      * **API Key:**  sk\-abc123<br><br>      * **Location:**  Header<br><br>      * **Parameter Name:**  Authorization<br><br>* **Outbound credential type**<br><br>   * **API Key**: Applicable to external services that use fixed keys for authentication.<br><br>   * **OAuth Client**: Applicable to downstream services that require authentication through the OAuth 2.0 process.<br><br>      * "OAuth Client (M2M)" access credentials are supported only when "Inbound identity authentication" is set to "API Key".<br><br>      * "OAuth Client (M2M)" and "OAuth Client (USER_FEDERATION)" access credentials are supported only when "Inbound identity authentication" is set to "OAuth JWT". |

4. Click "Create" to finish creating the MCP service that connects MCP Server to AgentKit.

### Step 3: Configure the private egress VPC on the BytePlus side

When the backend service type is **Private domain name**, call additional network\-side APIs to complete the private egress network configuration so that the service can communicate properly.

1. Click [here](https://console.byteplus.com/iam/service/attach_role/?ServiceName=privatelink), and on the Cross\-service access request page, click "Authorize now" to create the **ServiceRoleForPrivateLink** role. This role allows PrivateLink to access other cloud service resources under your account for network connectivity.

2. Return to the [AgentKit console](https://console.byteplus.com/agentkit). On the Gateway instance page, click the gateway name **prod_mcp_gateway**, and on the "Configuration information" tab, obtain the IDs of the VPC, subnet, **SpaceNetwork**, and **EgressService**.

3. Call CreatePrivateEgressEndpoint, pass in the preceding IDs to create the private egress endpoint, and record the PrivateEgressEndpointId returned in the response.

   > **warning**

   > The `VpcId`and `SubnetId`that you pass in must **exactly match the outbound private network and subnet configured for the MCP service (mcp_service_fgajjno5)**.

4. Call ModifyPrivateEgressEndpoint, set `AppPrivateAccessEnabled` to `true`, and enable application private network access for ** ** PrivateEgressEndpoint.

### Step 4: Configure private DNS resolution

After you establish network connectivity, ensure that the dedicated gateway can resolve the private domain name of the backend service.

Call EnablePrivateEgressDns and pass in the obtained "EgressService" ID that you obtained earlier to enable DNS resolution for the private network egress. The steps in this topic require you to pass in the IP address and port of the Tencent Cloud Private DNS inbound endpoint.

> **tip**

> We recommend that you configure resolution by private domain name suffix. For example, if the customer backend is `mcp-api.service.internal.example.com`, the resolution scope should cover `service.internal.example.com`or the **root domain** of the actual private domain.

|**Parameter** |**Recommended** |**Validation method** |
|---|---|---|
|DNS Server IP |The inbound service IP address of the Tencent Cloud inbound endpoint. If there are multiple IP addresses, enter all of them. |Port 53 on this IP address is reachable from the BytePlus VPC subnet. |
|DNS Server Port |53<br><br>> **tip**<br><br><br>> If the cloud provider console displays a custom port, use the actual port shown on the page.<br> |The security group and the ACL both allow UDP and TCP traffic on port 53. |
|Domain |The private domain names that actually need to be forwarded. This prevents all DNS requests from being forwarded to Tencent Cloud.<br><br>This value must be consistent with the "fixed domain name" of the backend service that is specified for the MCP service in AgentKit. You can obtain this information from the basic information of the MCP service. |Resolving this domain name returns a Tencent Cloud private IP address. |

### Step 5: Integrate the MCP toolset into the agent code and verify it

Here, the MCP toolset is integrated into the agent built with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en). This is to connect to the MCP endpoint exposed by the AgentKit gateway in the agent code and carry inbound credentials to complete tool discovery and calls.

1. In the "Basic information" tab of the MCP service **mcp_service_fgajjno5**, obtain the MCP service URL and inbound identity authentication API Key.

2. Under "API Access Key" in the[ IAM console](https://console.byteplus.com/iam/keymanage), click the "Create Access Key" button to create an Access Key. After creation, copy the Access Key ID (AK) and Secret Access Key (SK).

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

      3. Press the `i` Key to enter edit mode. In the **` .env`** file, enter the following content to add MCP service configuration.

         ```Bash
         MCP_SERVICE_URL=<mcp_router_url>
         MCP_SERVICE_API_KEY=<mcp_router_api_key>
         ```

         |Parameter​ |Source |
         |---|---|
         |<mcp_router_url\> |`url` in the MCP service sample call. |
         |<mcp_router_api_key\> |`Authorization` in the MCP service sample call. |

      4. Press the `esc` key to exit edit mode, and enter `:wq` to save and exit the file.

### Step 5: Verify the result

1. **Local test**.

   1. Query the MCP tools that the agent can call. The returned tool list matches the tools exposed by the MCP service and the tools of the backend MCP Server.

   2. Push local data online.

      1. Execute the `source .venv/bin/activate `command in the local terminal to reactivate the VeADK virtual environment. If you are already in the VeADK virtual environment, skip this step.

      2. Execute the `cd <Project directory>` command to enter the root directory of the agent project.

      3. Execute the` agentkit launch `command to deploy the agent to the AgentKit agent runtime.

2. **Online test**.

   1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).  In the agent runtime list, click "Online test" in the Actions column of the target agent.

   2. After you enter the prompt "What MCP tools do you have?", the tools available in the enterprise's MCP Server will be returned.

## FAQ

|Issue |Solution |
|---|---|
|Domain name resolution failure |This issue is typically caused by forwarding rules that have not taken effect, a mismatch in the forwarding domain scope configuration, an unreachable DNS inbound endpoint, or port 53 not being open. We recommend that you troubleshoot in the following order: DNS reachability \-\> forwarding rule matching \-\> authoritative DNS records. |
|The domain name can be resolved but the service is unreachable |This indicates that the DNS configuration has taken effect, but the network path or security policy issues still exist. We recommend that you check the route table, service port access, backend listening address, and security group rules. |
