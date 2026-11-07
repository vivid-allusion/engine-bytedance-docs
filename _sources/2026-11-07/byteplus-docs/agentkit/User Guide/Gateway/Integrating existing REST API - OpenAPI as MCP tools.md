---
title: "Integrating existing REST API/OpenAPI as MCP tools"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_existing_REST_API_OpenAPI_as_MCP_tools"
---

For enterprise developers with existing REST APIs or OpenAPI specifications, you can use AgentKit Gateway's **HTTP to MCP** protocol mode to instantly package backend interfaces such as ticket, order, approval, and CRM into MCP tools callable by agents, **without modifying backend code.**  This topic covers the complete closed\-loop process, including preparing the OpenAPI file, creating an MCP service, configuring inbound and outbound authentication credentials, generating a toolset, integrating agent code, and verifying results.

## Scenario overview

Enterprises often have accumulated a large number of REST\-style business systems internally, such as ticket systems, order centers, approval flows, CRM, and internal knowledge base search interfaces. To enable agents to call these systems, there are usually two approaches:

* **Modify the backend**: Each system needs to reimplement an MCP protocol. This solution is costly, time\-consuming, and requires cooperation from business teams.

* **Gateway\-side conversion**: AgentKit Gateway reads the OpenAPI description file and automatically maps each HTTP interface to an MCP tool. This solution enables zero backend modification.

**HTTP to MCP** is the second approach. Gateway completes protocol translation at the entry layer: The agent side initiates standard tools/list and tools/call requests, and Gateway translates them into HTTP requests (GET / POST / PUT / DELETE + JSON body) recognizable by the backend according to the OpenAPI definition, then returns the response to the agent.

In addition to protocol translation, Gateway also provides the following capabilities at the entry layer:

* **Unified inbound authentication:**  When an agent calls the Gateway, identity is verified via an API Key or OAuth JWT, preventing backend interfaces from being directly exposed externally.

* **Unified outbound credential injection:**  The API Key, Bearer Token, or OAuth Token required by backend systems is centrally managed and does not enter agent code.

* **Unified tool governance:**  Multiple backend APIs can be aggregated into an MCP service or MCP toolset entry exposed to agents.

## Core concepts

### HTTP to MCP

HTTP to MCP is a protocol mode provided by AgentKit Gateway. Gateway reads the OpenAPI file and automatically generates an MCP tool for each combination of path and method (for example, POST /v1/estimate\-calories becomes estimate_calories).

* Tool name and description: By default, extracted from OpenAPI's operationId and summary/description.

* Tool input parameter Schema: Extracted from OpenAPI's parameters and requestBody and directly exposed to the model.

### OpenAPI file

The OpenAPI file is a standard YAML/JSON file that describes REST APIs, containing the service address, path, method, parameters, request body, and response body structure.

In this topic, the OpenAPI file is the **only source of tools** for HTTP to MCP—all tool names, descriptions, parameters, and schemas are derived from the OpenAPI definition. The quality of the file directly determines how accurately the model selects tools and passes parameters.

### MCP proxy vs HTTP to MCP

|**Item** |**MCP proxy** |**HTTP to MCP** |
|---|---|---|
|Backend requirement |The backend has implemented the MCP protocol (Streamable HTTP) |The backend is an ordinary REST / HTTP service with an OpenAPI 3.0 description. |
|Tool definition source |Dynamically returned by the backend MCP Server tools/list |Automatically generated after the Gateway reads the OpenAPI file |
|Backend modification cost |MCP protocol implementation is required |No modification is required; provide only the OpenAPI file |
|Typical scenarios |Existing self\-built or third\-party MCP Server |Existing ticket, order, approval, CRM, and other REST APIs |

### MCP toolset

An MCP toolset is an entry point for organizing, filtering, and retrieving MCP tools. In the HTTP to MCP scenario:

* A single OpenAPI file typically generates dozens to hundreds of tools. With an MCP toolset, you can select only the tools that truly need to be exposed to agents.

* Multiple backend systems (ticket + approval + CRM) can be aggregated into the same MCP toolset, so the agent connects to only one tool entry point.

* When there are many tools, the semantic retrieval mode can be enabled. In this mode, the model dynamically selects tools from the toolset based on user intent, reducing the tool description footprint in a single prompt.

## Prerequisites

* The AgentKit service has been activated. To enable AgentKit, log in to the[ AgentKit console](https://console.byteplus.com/AgentKit) and follow the system prompts to complete the operations.

* The agent has been built with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) and published to the agent runtime in the AgentKit console. For details, refer to [Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en).

* The corresponding backend service has been created, and the business has been deployed. In this topic, the backend service is deployed on an **ECS** instance. For details, see [Purchasing and using ECS instances](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).

* You have prepared a compliant OpenAPI file. The backend interface must have a Swagger 2.0 or OpenAPI 3.0 description file, which must contain the service address, path, method, parameters, request body, and response body definitions.

   > **tip**

   > Currently, only Swagger 2.0 and OpenAPI 3.0 format API description files are supported. If the backend has only nonstandard API documentation, such as a Word document or wiki page, convert it into an OpenAPI 3.0\-compliant file before integration. For the API file specifications, see [MCP service API file specifications and examples](https://docs.byteplus.com/en/docs/agentkit/MCP_service_API_file_specifications_and_examples).

* An accessible network environment is available where the AgentKit Gateway can access the existing MCP Server address.

   > **tip**

   > The AgentKit Gateway currently does not support private IP addresses as backends. We recommend using the following two methods for network connectivity.

   * **Same VPC**: subnets within the same VPC (Virtual Private Cloud) are, by default, interconnected and can be accessed directly via the private network.

   * **Cross VPC**: For BytePlus cross\-VPC scenarios, PrivateLink can be used to enable network communication between VPCs. For detailed procedures, see [Implementing private access between VPCs across accounts](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03).

   * **Public domain name**: Outbound policy needs to be configured for public domain names. You can configure a NAT Gateway for the VPC where the existing MCP Server resides. For details, see [Accessing public network via SNAT ](https://docs.byteplus.com/en/docs/natgateway/Accessing-the-internet-using-SNAT)and [Providing services to public network via DNAT](https://docs.byteplus.com/en/docs/natgateway/Providing-services-over-the-internet-using-DNAT).

* Outbound credentials are ready. The backend REST API typically requires authentication (for example, `Authorization: Bearer <token>` or a custom header). Credentials must be prepared in advance as outbound credentials during MCP service creation.

* (Optional) A gateway instance has been created. This topic provides an example on how to use **Share mode** to create an MCP service and an MCP toolset. For a production environment, we recommend selecting **Dedicated gateway** mode. You need to create a gateway instance in advance. For details, see [Creating enterprise gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances?lang=en).

## Procedure

In the following section, the example of integrating the recipe‑making REST API as an MCP tool is used to describe the complete workflow. The list of tools/files required for the procedure is as follows:

|List item |Description |
|---|---|
|OpenAPI file |The OpenAPI file used in this topic is `cooking_tools_api.yaml`. |
|Backend service deployment location |The backend service is deployed on an **ECS** instance. |
|Network status |AgentKit and the backend service are in the same VPC. |
|Outbound credential |The outbound credential used in this topic is the API Key `Authorization: Bearer sk-abc123`.<br><br>> **tip**<br><br><br>> In actual operations, use the API Key of your own backend service.<br> |
|Agent build method |An agent built with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en). |

### Step 1: Prepare and validate the OpenAPI file

Obtain the OpenAPI 3.0 description file (.yaml or .json) from the backend team, and validate it locally to ensure that the file format and key fields are complete. For API file specifications, refer to [MCP service API file specifications and examples](https://docs.byteplus.com/en/docs/agentkit/MCP_service_API_file_specifications_and_examples).

* Use Swagger Editor or `openapi-cli` to validate the file to avoid syntax errors.

* Each interface contains clear `operationId`, `summary`, and `description` information.

* Input parameters contain field types, `required `flags, and natural‑language `descriptions`.

The OpenAPI file used in this topic is `cooking_tools.yaml`, a minimal example (fragment):

```JSON
openapi: 3.0.0
info:
  title: Cooking Tools API
  version: 1.0.0
paths:
  /v1/estimate-calories:
    post:
      operationId: estimate_calories
      summary: Estimate dish calories
      description: Estimate the total calories of a dish based on ingredients and quantities
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required: [ingredients]
              properties:
                ingredients:
                  type: array
                  description: List of ingredients
                  items:
                    type: object
                    required: [name, amount_g]
                    properties:
                      name:
                        type: string
                        description: Ingredient name
                      amount_g:
                        type: number
                        description: Amount (grams)
                servings:
                  type: integer
                  description: Number of servings, default is 1
      responses:
        '200':
          description: Estimation successful
          content:
            application/json:
              schema:
                type: object
                properties:
                  total_calories:
                    type: number
                    description: Total calories (kcal)
                  per_serving_calories:
                    type: number
                    description: Calories per serving (kcal)
```

**Parameter configuration descriptions**

|Parameter​ |**Description** |**Sample value** |
|---|---|---|
|`openapi` |The specification version. Currently, Swagger 2.0 and OpenAPI 3.0 are supported. |3.0.0 |
|`paths.<path>.<method>.operationId` |Mapped to the MCP tool name. Lowercase underscore style with business meaning is recommended. |estimate_calories |
|`summary` / `description` |Used in the tool description, directly affecting model tool selection accuracy. We recommend summarizing what the tool does in one sentence and adding a paragraph explaining when it should be called. |Estimate the total calories of a dish based on the ingredients and their quantities. |
|`parameters` /` requestBody` |Input parameter definition. Field name, type, `required`, `enum`, and `description` are all converted into the `Schema` seen by the model. |title, priority |

### Step 2: Create an MCP service and configure inbound authentication and outbound authentication

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Gateway \> MCP integration". On the "MCP Service" tab, click "Create MCP service".

3. Specify related parameters based on the following table.

   > **tip**

   > The following table describes only the parameters required for this procedure. For more parameters and descriptions, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

   * **Basic information**

      |Parameter |Description |
      |---|---|
      |Term |Enter the name of the MCP service. After creation, you cannot change the MCP service name. Here, the name is **syc_cooker**. |
      |Associated gateway |Select the gateway type for the MCP service. Select **Share mode** in this example.<br><br><br>* **Dedicated gateway** (recommended): The MCP service runs on a gateway instance that you independently create. Resources are dedicated and not shared, ensuring stable capacity.<br><br>* **Share mode**: The MCP service runs on shared gateway resources provided uniformly by the platform. You do not need to create a gateway instance.<br><br><br>> **warning**<br><br><br>> **Share mode** is only used for illustration purposes. In actual production environments, use **Dedicated gateway**.<br> |
      |Access method |Select the method for accessing the MCP service. Select **HTTP to MCP** in this example. |
      |Access path |Specify the access path of the MCP service. Here, the path is `/mcp`. |
      |API information |Upload an OpenAPI file in the Swagger 2.0 or OpenAPI 3.0 format. Here, the file used is `cooking_tools.yaml`. |

   * **Network configuration**

      |Parameter​ |Description |
      |---|---|
      |Network configuration |Configure the network access method for the MCP service to specify networks of which types that can access the newly created MCP service. Since the backend service in this guide is deployed on an ECS instance, and the agent that actually calls the MCP service runs on AgentKit, the configured network access method here is **Public network** and **Private network**.<br><br>> **warning**<br><br><br>> Currently, MCP toolsets do not support adding MCP services with only "Private network" enabled. If you need to expose tools within an MCP service from an MCP toolset via a private network, enable public network access at the same time. Select both **Public network** and**Private network**.<br><br><br><br>* **Public network**: Select this option to allow access by external services such as Trae, Codex, and more. Public network is the default access method.<br><br>* **Private network**: Select this option to allow access by agents on AgentKit only. After configuration, the service is not externally accessible and is available only for internal use. Any VPC and subnet within the same region. A maximum of one subnet can be selected per availability zone. |

   * **Authentication information**

      |Parameter​ |Description |
      |---|---|
      |Inbound identity authentication |Configure the identity authentication method for the MCP service. The configuration here is **API Key / apikey_t1k5gdoc** (automatically generated by the system).<br><br>Inbound identity authentication serves as the first security barrier for service access. It ensures that only authorized entities can call MCP services and prevents unauthorized access, data leakage, and malicious attacks.<br><br><br>* **API Key**: After you enter a name, an API Key will be automatically created and associated with the MCP service. After the MCP service is created, you can view the API Key on the MCP service details page.<br><br>* **OAuth JWT**: Use the OAuth authorization mode to apply for an access token and call APIs. This mode enhances security and simplifies configuration. Before configuring this option, ensure that you have [created a user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) and [a client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en).<br><br><br>> **warning**<br><br><br>> Enable inbound authentication for all MCP services in the production environment. An MCP endpoint with inbound authentication disabled is equivalent to exposing internal business APIs to the public network, which may be accessed without authorization, resulting in unauthorized access, privilege escalation, and data leakage risks.<br> |

   * **Backend configuration**

      |Parameter​ |Description |
      |---|---|
      |Service type |Configure the type of backend service to connect to the MCP service. Here, select **ECS**. |
      |Server |Select the ECS instance where the backend service is deployed and configure the port. |
      |Outbound credential |Configure the outbound authorization for the MCP service to allow the agent to use this credential to access downstream resources. Here, the configured credential is **API Key / inspection_api_key**. **This API Key is newly added, and the procedure is as follows**.<br><br><br>* **Add API Key**:<br><br>   1. In the API Key drop\-down list, click the "Add" button at the bottom.<br><br>   2. Refer to the image below to configure the API Key information and create an API Key named **inspection_api_key**. The outbound credential used in this topic is the API Key `Authorization: Bearer sk-abc123`. Enter the corresponding information as follows:<br><br>      * **API Key:**  sk\-abc123<br><br>      * **Location:**  Header<br><br>      * **Parameter Name:**  Authorization<br><br>* **Outbound credential type**<br><br>   * **API Key**: Applicable to external services that use fixed keys for authentication.<br><br>   * **OAuth Client**: Applicable to downstream services that require authentication through the OAuth 2.0 process.<br><br>      * "OAuth Client (M2M)" access credentials are supported only when "Inbound identity authentication" is set to "API Key".<br><br>      * "OAuth Client (M2M)" and "OAuth Client (USER_FEDERATION)" access credentials are supported only when "Inbound identity authentication" is set to "OAuth JWT". |

4. Click the "Create" button to complete MCP service creation. A successful result is shown below.

   * In the "Basic information" tab of the newly created MCP service, you can see the **MCP access endpoint** (the address for agent\-side connection) generated by the Gateway for this service.

   * In the "MCP tool" tab of the newly created MCP service, you can see the tools automatically generated by OpenAPI, and the number of tools matches the number of combinations of `path` × `method` in OpenAPI.

### Step 3: Configure the MCP toolset

> **warning**

* > This step is **optional**. Scenario descriptions are as follows:

   * > **Required**: Create an agent and integrate tools converted from REST API/OpenAPI into the agent in the AgentKit console.

   * > **Optional**: Integrate tools converted from REST API/OpenAPI into the agent via VeADK.

* > **This topic uses VeADK to create an agent and integrate MCP. To cover the entire process, an MCP toolset is configured.**

1. In the left navigation pane, click "Gateway \> MCP integration". On the "MCP Toolset" tab, click "Create MCP toolset".

2. On the Create MCP toolset page, refer to the table below to complete the configuration.

   |Parameter​ |Description |
   |---|---|
   |**Basic information** ||
   |MCP toolset name |Enter the name of the MCP toolset. After creation, you cannot change the MCP toolset name. Here, the name is **mcp_toolset_syc**. |
   |Associated gateway |Select the gateway type for the MCP toolset. Select **Share mode** in this example. |
   |Access path |Configure the access path for the MCP toolset. The default access path is `/mcp`. Here, the default value is retained. |
   |**Network configuration** ||
   |Network configuration |Configure the network access method for the MCP toolset to specify network of which type can access the newly created MCP toolset. Since the backend service in this guide is deployed on an ECS instance, and the agent that actually calls the MCP toolset runs on AgentKit, the configured network access method here is ** Private network**.<br><br><br>* **Public network**: Select this option to allow access by external services such as Trae, Codex, and more. Public network is the default access method.<br><br>* **Private network**: Select this option to allow access by agents on AgentKit only. After configuration, the service is not externally accessible and is available only for internal use. Any VPC and subnet within the same region. A maximum of one subnet can be selected per availability zone. |
   |**Authentication information** ||
   |Inbound identity authentication |Configure the identity authentication method for the MCP toolset. The configuration here is **API Key / apikey_hcrtmlsvdoc** (system\-generated).<br><br>Inbound identity authentication serves as the first security barrier for service access. It ensures that only authorized entities can call MCP services and prevents unauthorized access, data leakage, and malicious attacks. The following configuration methods are supported.<br><br><br>* **API Key**: After you enter a name, an API Key will be automatically created and associated with the MCP service. After the MCP service is created, you can view the API Key on the MCP service details page.<br><br>* **OAuth JWT**: Use the OAuth authorization mode to apply for an access token and call APIs. This mode enhances security and simplifies configuration. Before configuring this option, ensure that you have [created a user pool](https://docs.byteplus.com/en/docs/agentkit/create-user-pool?lang=en) and [a client](https://docs.byteplus.com/en/docs/agentkit/create-client-side?lang=en).<br><br><br>> **warning**<br><br><br><br>* > API Key and OAuth JWT are mutually exclusive authentication methods. You can only enable one method per MCP toolset.<br><br><br>* > Up to 1 inbound identity authentication configuration is supported in API Key mode. Up to 5 clients can be associated in OAuth JWT mode.<br> |
   |**Tool management** ||
   |Calling mode |When an agent calls a toolset, the toolset can return all tools or filter target tools via semantic matching or tag filtering. Here, select **Semantic retrieval**.<br><br><br>* **Full return**: Returns all internal MCP tools directly after connecting to the MCP toolset. We recommend that you select this mode when the number of tools is small, for example, 20 or fewer.<br><br>* **Semantic retrieval**: Performs semantic matching based on the calling intent against tool descriptions and returns the best\-matching tools. We recommend that you select this mode when the number of tools is large and the caller is a general\-purpose agent.<br><br>* **Tag retrieval**: Filters required tools accurately based on tool tags. We recommend that you select this mode when the number of tools is large and the caller is a domain\-specific agent. |
   |Tool |Add tools to the MCP toolset. Click the "Add tool" button and select one or more target tools from the MCP services. You can select and combine tools from multiple MCP services to meet your business needs.<br><br>Here, select the "estimate_calories", "generate_cooking_steps", and "ingredient_substitute" tools of the MCP service created in the previous step (**syc_cooker**), as well as some other tools from other MCP services. |

3. Click the "Create" button to complete MCP toolset creation. A successful result is shown below.

   * In the "MCP tool" tab of the newly created MCP toolset, you can see the tools selected during creation.

   * In the "Test" tab of the newly created MCP toolset, follow the on\-screen instructions to test the toolset.

      * Step 1: Click the "Connect test" button.

      * Step 2: Enter the prompt related to this tool, and the system automatically matches the most suitable tool. For the demo in this topic, the tool converted via REST API/OpenAPI relates to cooking. Enter "cook rice" here.

      * Step 3: The system retrieves available tools based on the prompt. Select a target tool for testing.

      * Step 4: Enter the dish name and click the "Testing tool" button.

### Step 4: Integrate the MCP toolset into the agent code and verify

Here, the MCP toolset is integrated into the agent built with VeADK. This is to connect to the MCP endpoint exposed by the Gateway in the agent code and carry inbound credentials to complete tool discovery and calls.

1. In the "Basic information" tab of the MCP toolset **mcp_toolset_syc**, obtain the MCP toolset URL information and inbound identity authentication API Key.

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
      export BYTEPLUS_ACCESS_KEY=<your_access_key>
      export BYTEPLUS_SECRET_KEY=<your_secret_key>
      ```

   * **Configure environment variables in **  **`.env`**

      In the  **`.env`** file, enter the following content to add MCP toolset configuration.

      ```Bash
      # The URL of the MCP toolset. You can obtain it from the toolset sample call.
      TOOL_MCP_ROUTER_URL=<tool_mcp_router_url>
      # The inbound API Key credential for the MCP toolset.
      TOOL_MCP_ROUTER_API_KEY=<tool_mcp_router_api_key>
      ```

      |Parameter​ |Source |
      |---|---|
      |<your_access_key\> |Information about the platform Access Key ID (AK). |
      |<your_secret_key\> |The Secret Access Key (SK) of the platform. |
      |<tool_mcp_router_url\> |`url` in the MCP toolset sample call. |
      |<tool_mcp_router_api_key\> |`Authorization` in the MCP toolset sample call. |

   **Result**: The agent has successfully recognized the tools in the MCP toolset automatically. The tools in the returned tool list are consistent with those selected in the MCP toolset.

### Step 5: Verify the result

1. **Local test**.

   1. After you send the prompt "Use MCP tool content to tell me the steps for boiling eggs" to the agent locally, the agent can successfully call the tools in the MCP toolset to process the task.

   2. Push the code to the AgentKit console agent runtime.

      1. Execute the `source .venv/bin/activate `command in the local terminal to reactivate the VeADK virtual environment. If you are already in the VeADK virtual environment, skip this step.

      2. Execute the `cd <Project directory>` command to enter the root directory of the agent project.

      3. Execute the` agentkit launch `command to deploy the agent to the AgentKit agent runtime.

2. **Online test**.

   1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).  In the agent list, click the name of the target agent and click the "Online test" button on the agent details page.

   2. After you enter the prompt "What MCP tools do you have?", the agent returns the REST API\-converted tools for creating recipes.

## Troubleshooting

|**Symptoms** |**Possible causes** |**Repair suggestion** |
|---|---|---|
|The tool list is empty when an MCP service is created |`paths` or `operationId` is missing in the OpenAPI file. |Use Swagger Editor to validate the file, add an `operationId` for each API, and upload again. |
|Response‑field mismatch between MCP toolset and OpenAPI definition after creation |The `responses` definition in the OpenAPI file is inaccurate. |Correct the `responses` definition in the OpenAPI file. |
|Incorrect tool selection by model/invalid parameters passed |In the OpenAPI file, the `summary`/`description`/field `description` is too brief. |For each API, add a natural\-language description of "what the tool does and when it should be called". Define key fields as `enum`. |
|Gateway returns `401` (inbound) |Missing or invalid inbound credential. |Confirm the Authorization header format; check whether the API Key or JWT matches the inbound authentication method. |
|Backend returns `401`/`403` (outbound) |Invalid or expired outbound credential. |Update the credential value in the Credential Provider; confirm that Prefix and ParameterName are consistent with the backend. |
|Backend returns a` 400` error for invalid parameters |Field names or types in OpenAPI do not match the actual interface. |Use tools such as Postman to directly connect to the backend and verify the actual contract. After correcting the OpenAPI, upload it again. |
