---
title: "Gateway overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/MCP_Overview"
---

AgentKit Gateway provides a unified entry point for agents to access external capabilities. It provides features such as authentication, routing, protocol conversion, and access governance. As product capabilities extend, gateway\-related objects include gateway instances and model services in addition to Model Context Protocol (MCP) services and MCP toolsets. This topic describes the relationships among gateway objects, applicable scenarios, and onboarding paths to help you select an appropriate access method based on your business requirements.

## What is AgentKit Gateway

Provided by AgentKit, AgentKit Gateway functions as a **unified entry point** for production environments. It centrally manages access addresses, network connectivity, monitoring, billing, and access control for MCP services, MCP toolsets, and model invocation flows. This reduces the cost for business teams to maintain multiple entry points and sets of credentials separately. After integration, agents or business applications can access backend tools or model services through a unified address, with the gateway handling authentication, routing, protocol conversion, and credential injection.

For MCP scenarios, gateways provide unified access to MCP services and MCP toolsets. For model invocation scenarios, model services centrally manage model providers, model IDs, provider API keys, and proxy API keys, and provide a unified access entry point for business applications. A model group combines multiple connected upstream models under a unified invocation name and routes requests based on weights. If your business requires a production\-grade access entry point, dedicated capacity, resource isolation, unified monitoring, or separate billing, we recommend creating a gateway instance first and then integrating MCP services, MCP toolsets, or model services with it. If you only need to verify the integration process for a single tool or model, you can follow the corresponding quickstart guide and later migrate to a gateway instance for production.

## Related concepts

|Concept |Description |
|---|---|
|Gateway instances |A gateway instance (or gateway for short) is a dedicated gateway resource in AgentKit that provides a unified access entry for model services, MCP services, and MCP toolsets. It applies to production environments or business scenarios that require independent capacity, resource isolation, centralized access entry management, and separate billing.<br><br>Gateway instances are available in two product forms: **dedicated** and **shared**. The core difference lies not in whether they provide gateway capabilities, but in resource ownership, performance guarantees, and applicable scenarios. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Gateway_modes_and_MCP_request_counting_rules?lang=en#RtZDC8Cu)<br><br><br>* **Shared gateway**: Shared instances are applicable to POC or development testing, while dedicated instances are intended for production. To quickly validate capabilities or conduct a low\-cost trial, select the shared mode.<br><br>* **Dedicated gateway**: To support production with a clear entry point, isolation, monitoring, and billing boundaries, select the dedicated gateway. Dedicated gateways are further classified into MCP gateways, model gateways, and agent runtime gateways based on the type of associated resources.<br><br>   * **MCP gateway**: Used to access MCP resources (MCP services and MCP toolsets). Select an MCP gateway when you want agents to discover and invoke external tools.<br><br>   * **Model gateway**: Used to access model services. Select a model gateway when you need to centrally manage model providers, model IDs, provider API keys, and proxy API keys.<br><br>   * **Agent runtime gateway**: Used to access runtime resources. If the resource to be mounted to the gateway instance is a runtime resource, select this type. |
|MCP |MCP is an open protocol. Within the AgentKit gateway, MCP is represented as MCP services and MCP toolsets. MCP enables agents to "discover tools (tools/list) and call tools (tools/call)" in a standardized way. It allows tool services with different implementations, languages, and deployment forms to be accessed by agents via a unified protocol, thereby abstracting "tool capability" from agent code into reusable external services.<br><br><br>* **MCP service**: Used to integrate a backend service with an AgentKit gateway. You need to configure the backend address, network connectivity method, protocol mode, and authentication method in the MCP service. After the configuration is complete, the gateway wraps the backend service into tool capabilities that agents can discover and invoke.<br><br>* **MCP toolset**: An MCP tool is a specific capability unit (a specific operation) that can be invoked by an agent. An MCP toolset is an aggregated entry point for tools exposed to IDEs, CLIs, and agents within the AgentKit gateway. Create an MCP toolset when you need an agent to use multiple MCP services simultaneously or to control the scope of visible tools by business domain.<br><br>* **Backend service**: The backend service is the actual service implementation behind the gateway that executes the tool's capabilities. It is the real business system that the gateway ultimately accesses, providing actual business capabilities and data access.<br><br>* **MCP server**/**MCP client**: The MCP server and MCP client separate "providing tools" from "using tools". The server provides tools and implements MCP APIs such as tools/list and tools/call. The client calls tools and is usually integrated with the agent code. The client establishes connections with the MCP server and initiates invocations.<br><br>* **Inbound authentication (Auth)** /**outbound authentication (AuthZ)** : Inbound authentication and outbound authentication decouple the caller's identity from the backend access credentials, preventing sensitive credentials from being scattered across the agent code.<br><br>* **AgentKit Identity**: As one of the identity sources for inbound authentication and permission evaluation, AgentKit Identity provides an auditable and manageable identity system. It is an identity and permission platform that manages the identity information of users, clients, and workloads and supports the coordination of authentication and permissions.<br><br>* **Schema**: Schema is the data structure definition for tool inputs and outputs. It describes field names, field types, whether fields are required, and field meanings. For example, an "order query" tool can define `order_id` as a required string and `status` as an optional enum in its Schema. A clearer Schema makes it easier for the system to validate request formats and for the large model to select parameters correctly and initiate tool calls. |
|Model service |A model service is a model‑scenario resource deployed on the AgentKit gateway. It is used to centrally manage configurations such as model providers, provider API keys, model IDs, proxy API keys, model access scopes, retries, and fallback models. Business applications invoke authorized models through a unified access address and proxy API key, without the need to directly store provider API keys. |
|Model group |* A model group is a logical call unit within a model service. It combines multiple connected upstream models under a single invocation name. The application fills in this invocation name in the `model` field of the request, and the gateway selects an upstream model from the group based on weights.<br><br>* After retries within the group are exhausted, the fallback model can be called at most once. Access to a model group must be granted to a Proxy API Key separately. |

## Gateway instances: dedicated vs shared

|**Dimension** |**Dedicated gateway** |**Shared gateway** |
|---|---|---|
|Resource type |Visible, manageable, and independent resource instances |Platform shared resources |
|Resource isolation |Stronger isolation with exclusive resources |Shares underlying gateway resources with other tenants. |
|SLA |Designed for production scenarios, it delivers higher performance guarantees and more explicit SLA commitments. |No production\-grade SLA commitment |
|Application scenarios |Core production businesses and scenarios with high concurrency, isolation, and stability requirements |POC, development testing, low‑traffic validation, and lightweight trial use |
|Billing method |As an independent billable item, it incurs instance fees and data processing fees based on specification and usage. For detailed billing items and billing methods, see[ Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items). |Shared gateway fees are incurred. For detailed billing items and billing methods, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items). |
|Quantity/performance limit |Operates at the capacity of the selected specification tier. Capacity planning can be done based on the QPS, connection count, and resource quantity. |Platform‑preset quantity, performance, and capability limits. It is more applicable to low\-barrier trials rather than long‑term production workloads. |

## Component relationships

* The **gateway instance** provides a unified access entry point and delivers network, monitoring, billing, and resource isolation features.

   * Within the same gateway instance, resource names of the same type must be unique.

   * Each gateway instance only supports associating resources of the corresponding type. For example, an MCP gateway can only associate MCP resources, and a model gateway can only associate model services.

* **MCP services, MCP toolsets, agent runtimes**, and **model services** are specific resources attached to a gateway instance and are used for backend tool integration, toolset management, and model call management, respectively. A model group is a logical call unit within a model service and cannot be mounted to a gateway instance independently.

|Type |Description |
|---|---|
|Relationship between gateway instance and model service |A **model service** is a "model call scenario" mounted on a **gateway instance**. The gateway instance provides a unified entry point and handles resource isolation, networking, monitoring, and billing.<br><br><br>* The model gateway manages call\-layer configurations, including model providers, hosting of provider API Keys, Proxy API Keys, model access scope, rate limiting, retries, and fallback models.<br><br>* A model group organizes multiple upstream models within a model service and exposes them under a unified invocation name. |
|Relationship between gateway instance and MCP service/MCP toolset |A **gateway instance** is not an **MCP service or toolset**. A gateway instance does not define specific tool semantics. It only provides production‑ready access, isolation, monitoring, and billing. |
|Relationship between MCP service and MCP toolset |* An MCP service can expose multiple tools.<br><br>* An MCP toolset can be associated with multiple MCP services, which can be grouped by business domain, permission boundary, or usage scenario.<br><br>* An MCP service, or an MCP tool within it, can be referenced by multiple MCP toolsets simultaneously. |

## Application scenarios

|**Scenarios** |Recommended |Description |
|---|---|---|
|Unified access to MCP tool capabilities is required |Gateway instance (MCP gateway type) + MCP service/MCP toolset |Applicable to scenarios where you need to expose backend services, existing APIs, or MCP servers for agents to invoke. |
|Centralized management of model providers and model access credentials |Gateway instance (model gateway type) + model service |Applicable to scenarios with multiple models and multiple providers, where you want the platform to centrally manage provider API keys, model IDs, and proxy API keys. |
|A unified model name is required, and traffic must be distributed across multiple upstream models. |Gateway instance (model gateway type) + model service + model group |Applicable to scenarios where the application does not need to be aware of provider differences. The gateway routes requests across multiple upstream models by weight and tries the fallback model if retries within the group fail. |

## MCP invocation details

### MCP implementation principles

**Protocol conversion principle**

When the backend is an existing HTTP API (non\-native MCP), the gateway wraps HTTP endpoints into MCP tool calls. Typical mappings include:

* **Method mapping:**  HTTP methods such as GET and POST are mapped to the MCP tools/call.

* **Parameter mapping:**

   * The HTTP Path, Query, Header, and Body are mapped to the input Schema of the MCP tool.

   * Keep field names stable so that models can learn and reuse them.

* **Result mapping:**

   * The HTTP response body is mapped to the return content of tools/call.

   * Non\-`2xx` results are mapped as structured errors, enabling the agent to retry, fall back, or display a message.

**Tool discovery principle**

The toolset supports three retrieval modes. The essential difference is how many tools are returned to the model:

* **Full return** (AllTools) **:**  Returns all tools in the toolset each time a toolset is connected. Suitable for a small number of tools, for example, fewer than 20.

* **Semantic retrieval** (SemanticSearch): Returns the most relevant tools based on the user's task and tool descriptions. This applies when there are many tools and the agent is general\-purpose, so you cannot pass all tools to the model on every call.

* **Tag retrieval** (TagSearch): Filters target tools based on tool tags. This applies when there are many tools that can be stably classified by business domain, role, and scenario.

The impact on tokens can be understood simply as follows: **The more tool schemas are returned, the more model context they consume**. When the number of tools grows to a certain scale (for example, exceeding N), we recommend using semantic search or tag search.

**Credential injection principle**

The gateway completes credential injection during the outbound request stage. The core process is:

1. Determines the required credential type for outbound requests (for example, API Key, OAuth Client) based on MCP service configuration and the caller.

2. Obtains or refreshes outbound credentials from the Credential Provider.

3. Injects the credentials into the Header or signature of the outbound request and then sends the request to the backend.

4. Outbound credentials are used only for the link from the gateway to the backend and **are not returned to the agent.**

### Runtimes call tools

In the MCP scenario, the agent connects to the gateway via an MCP Client and calls tools. The general workflow is as follows:

1. The runtime loads and runs agent code.

2. Agent code connects to the gateway through an MCP Client.

3. The MCP Client calls tools/list to obtain the list of available tools (or the toolset returns a subset according to the retrieval mode).

4. The large model determines which tool to call based on the current task and tool description.

5. The MCP Client initiates tools/call.

6. The gateway completes inbound authentication, routing, protocol conversion, and outbound credential injection. If authentication or permission verification fails, the gateway directly returns a `40X` error code. Otherwise, it forwards the request to the backend service.

7. After the backend execution is complete, the result is returned to the MCP Client through the gateway and then back to the agent.

### Authentication flow diagram

In the MCP scenario, the authentication flow needs to address three issues at the same time: confirming who can call the gateway, determining whether the caller can access the target tool, and determining which credentials the gateway needs to use when accessing the backend.

1. **Inbound authentication:**  The gateway verifies whether the request comes from an allowed caller (such as verifying the API Key or OAuth JWT).

2. **Identity anchoring:**  The gateway identifies the calling entity (workload, end user, or client) by using the Identity capability.

3. **Permission determination:**  During the routing stage, the gateway requests an authorization decision from the Permission gateway (whether to allow calling a specific tool or accessing a certain type of resource).

4. **Outbound authentication:**  The gateway obtains credentials required by the backend from the Credential Provider and injects them (for example, an API Key or OAuth Client). Credentials are not returned to the agent.

|**Stage** |**Object** |**Common credentials/input** |**Results** |
|---|---|---|---|
|Inbound authentication |Who can access the gateway to invoke MCP resources |API key or OAuth JWT |If the request passes, it proceeds to routing. If it fails, 401 or 403 is returned. |
|Permission determination |Whether tool calls are allowed |Identity, tool/resource identifier, action |If allowed, the request continues. If denied, the request returns 403. |
|Outbound authentication |Gateways accessing backend services |API key, OAuth client, and more (provided by Identity). |Credentials are injected into outbound request headers/signature and not returned to the agent |

## Procedure

1. [Create a gateway instance](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances?lang=en). Select the gateway type, specification, and network access method based on your business scenario. For MCP scenarios, select "MCP gateway". For model invocation, select "Model gateway".

2. **Create the corresponding resources based on your business scenario and integrate them with your agent.**

   * **MCP scenarios**

      1. [Create an MCP service](https://docs.byteplus.com/en/docs/agentkit/MCP_services), and optionally [create an MCP toolset](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

         * **MCP tool**: By creating, deploying, or importing an MCP service, you can connect self\-developed or public services to the platform in a unified manner. You can also upload API definition files to convert existing system APIs to MCP services with one click, without code modification, to quickly enhance secure interaction between large models and existing systems.

         * **MCP toolset (optional)** : Perform it based on your business scenario. If you have a single MCP service, a single agent, or are currently in the testing stage, you do not need to create an MCP toolset. If you need to aggregate multiple MCP services, reuse them across multiple agents, or operate in a production environment, creating an MCP toolset is more convenient **.**

      2. [Integrate the MCP service with agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_MCP_service_in_agent): Call the API capabilities integrated with the MCP service in your agent code. This achieves rapid enhancement of interactions between large models and existing systems without any code modifications.

   * **Model service scenarios**

      3. [Create a model service](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service): Configure the provider, model ID, Proxy API Key, and other information.

      4. Create and manage model groups (optional): Combine multiple upstream models under a unified invocation name, configure weights and fallback models, and grant access to the required Proxy API Keys.

      5. [Integrate model information into an agent](https://docs.byteplus.com/en/docs/agentkit/Integrating_model_information_in_agents): Connect to the API endpoint provided by the model service in your agent code. When using a model group, pass the model group invocation name in the `model` field. The gateway then handles authorization checks and upstream routing.

3. **Validate and observe**: After confirming connectivity, check logs, monitoring, and call results to verify that the configuration has taken effect.

## Common misconceptions

|**Misconceptions** |**Correct understanding** |**Determination method** |
|---|---|---|
|"MCP service equals my backend service." |**The MCP service is a wrapper layer in the gateway instead of a real backend**. The real backend is a function, a domain, ECS, VKE, or an existing MCP server. |Whether an MCP URL assigned by the gateway exists and whether it points to a BackendConfiguration. |
|"After creating an MCP toolset, the agent can definitely see all tools." |When creating an MCP toolset, you need to configure tools (first select an MCP service, then select tools within the MCP service) and the calling mode. **The toolset only exposes tools that have been added**. |Use tools/list or the console to test the toolset and check which tools are actually returned. |
|"Inbound API Key and backend API Key are the same thing." |The inbound API Key is the access gate for calling the gateway, while the backend API Key is the credential the gateway uses to access business systems. |One appears when a client requests the gateway. The other is managed by Identity and injected by the gateway into backend requests. |
|"The agent obtains the backend key before calling the backend." |We recommend that agents do not access backend keys and that the gateway and Identity perform outbound credential injection at the platform layer. |Check whether the agent code contains any third\-party API Key. Ideally, there should be none. |
|"Once the MCP Server is integrated, authentication is no longer required." |You still need to configure gateway inbound authentication and backend outbound authentication. **A unified gateway entry point does not mean the backend is left open**. |Perform negative testing: requests with no inbound credentials, incorrect inbound credentials, or no outbound credentials should all fail. |
