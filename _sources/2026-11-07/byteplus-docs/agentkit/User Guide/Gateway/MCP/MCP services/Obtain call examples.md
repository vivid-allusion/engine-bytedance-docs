---
title: "Obtain call examples"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Obtaining_sample_calls_svc"
---

After an MCP service is created, you can call it by using an IDE or CLI tool. The platform automatically generates sample code snippets that include the domain name, call examples, and Access Token for the MCP service, helping you quickly complete integration. This topic describes how to obtain sample calls.

## Background information

* **Sample call**

   * **Gemini CLI call example**: This applies to CLI tools such as Gemini CLI. For information about how to call the MCP service in Gemini CLI, see [Server-specific configuration](https://geminicli.com/docs/tools/mcp-server/#server-specific-configuration-mcpservers).

   * **Trae call example**: This applies to IDE tools such as Trae and Cursor. For information about how to call the MCP service in Trae, see [Manually configure the MCP server](https://docs.trae.cn/ide/add-mcp-servers#47a33ec0).

* **Access** ** token**

   An MCP service that uses **OAuth JWT** for inbound identity authentication requires an Access Token as the authentication credential.

## Prerequisites

An MCP service has been created. For more information, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

## Procedure

### Obtain call examples

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. Find the target MCP service and click "Sample call" in the "Actions" column.

4. View and copy the sample code. Click "Confirm" to close the window.

### Obtain an Access Token

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. Click the name of the target MCP service. On the "Basic information" tab, click "How to obtain Access Token" in the "Sample call" section.

4. View and copy the sample code. Replace the arguments in the example with your actual information.
