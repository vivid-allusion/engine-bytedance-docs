---
title: "Managing dedicated gateway instances"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Managing_gateway_instances"
---

After you create a dedicated gateway instance, you can manage it routinely. You can view the instance details and running status, manage the model services and MCP resources associated with the instance, and delete the instance when you no longer need it. This topic applies to scenarios where you have created a gateway instance and need to operate and maintain it.

## Prerequisites

You have created a dedicated gateway instance. For details, see [Creating dedicated gateway instances](https://docs.byteplus.com/en/docs/agentkit/Managing_gateway_instances).

## Procedure

### Manage gateway instances

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, in the gateway instance list, click the name of the target gateway to open the instance details page.

   **View the configuration information of gateway instances**

**Scenarios**: Confirm the basic configuration and network access information of a gateway instance.

   **Procedure**: Click the "Configuration information" tab to view the basic information and network configurations of the gateway instance. The basic information includes the instance name, ID, running status, specifications, and billing method. The network configurations include the inbound access address, access mode, VPC, and subnet.

   **Manage the associated resources of gateway instances**

**Scenarios**: View and manage the resources associated with the current gateway instance.

   **Procedure**:

   * **Model gateway**: Click the "Model service" tab to view information about the models associated with the model service for the current gateway instance. The information includes the model name, ID, status, model provider, and Proxy API Key.

   * **MCP gateway**: Click the "MCP" tab to view information about the MCP services and MCP toolsets associated with the current gateway instance.

      * On the "MCP Service" tab, you can click the "Create MCP service" button to create an MCP service in the current gateway instance. For the detailed procedure and parameter descriptions, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

      * On the "MCP Toolset" tab, you can click the "Create MCP toolset" button to create an MCP toolset in the current gateway instance. For the detailed procedure and parameter descriptions, see [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

### Delete gateway instances

> **warning**

* > **Deletion prerequisite**: If a gateway instance has associated model services, agent runtimes, or MCP resources, you cannot delete it directly. Delete all associated resources first, and then delete the instance. Take an MCP gateway as an example: Click the name of the target gateway instance, delete all associated resources on the MCP tab, and delete the instance after the "Delete" button becomes available.

* > **Irreversible operation**: After you delete a gateway instance, you cannot restore it. Proceed with caution.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, in the gateway instance list, click "Delete" in the "Action" column for the target gateway.

3. In the dialog box that appears, enter "Confirm delete", and then click "Delete" to complete the deletion.

4. After you delete the instance, refresh the page. If the instance no longer appears in the gateway instance list, the deletion is complete.
