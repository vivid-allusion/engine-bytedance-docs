---
title: "Selecting a dedicated gateway type"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Dedicated_gateway_type_selection"
---

AgentKit Gateway provides a unified entry point for agents to access external tools and model services. It provides features such as authentication, routing, protocol conversion, and access governance. This topic helps you select the appropriate dedicated gateway type based on the resources to be integrated.

## Step 1: Select a gateway type based on your business scenario

**Dedicated gateways** are further classified into **MCP gateways**, **model gateways**, and **agent runtime gateways ** based on the type of associated resources.

|**Gateway type** |**Attachable resources** |Applicable scenarios |
|---|---|---|
|MCP gateway |* MCP service<br><br>* MCP toolset |Expose backend services, existing APIs, or MCP Servers to agents so that agents can discover and call external tools. |
|Model gateway |* Model service |Centrally manages model providers, model IDs, provider API keys, and proxy API keys. |
|Agent runtime gateway |* Agent Runtime |Integrate agent runtime resources. |

> **warning**

> Each gateway instance only supports associating resources of the corresponding type. For example, an MCP gateway can only associate MCP resources, and a model gateway can only associate model services. Select the gateway type based on the resources to be associated, rather than solely based on whether the caller is an agent.

## Step 2: Integrate resources after type selection is complete

|**Selected type** |Next steps for the dedicated gateway |**Next steps for the shared gateway** |
|---|---|---|
|MCP gateway |1. [Creating dedicated gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances)<br><br>2. [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services)<br><br>3. [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset)<br><br>4. [Integrating MCP services in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_MCP_service_in_agent) |1. [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services)<br><br>2. [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset)<br><br>3. [Integrating MCP services in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_MCP_service_in_agent) |
|Model gateway |1. [Creating dedicated gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances)<br><br>2. [Creating model services](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service)<br><br>3. [Integrating model information in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_model_information_in_agents) |1. [Creating model services](https://docs.byteplus.com/en/docs/agentkit/Creating_model_service)<br><br>2. [Integrating model information in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_model_information_in_agents) |
|Agent runtime gateway |1. [Creating dedicated gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances)<br><br>2. [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)<br><br>3. [Calling agents](https://docs.byteplus.com/en/docs/agentkit/Sample_calls_for_text_prompts) |1. [Creating runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)<br><br>2. [Calling agents](https://docs.byteplus.com/en/docs/agentkit/Sample_calls_for_text_prompts) |
