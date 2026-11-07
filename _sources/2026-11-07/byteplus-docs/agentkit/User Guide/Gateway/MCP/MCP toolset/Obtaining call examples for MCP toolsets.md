---
title: "Obtaining call examples for MCP toolsets"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Obtaining_sample_calls"
---

After you create an MCP toolset, you can view system\-generated code examples in the console. The examples include the toolset domain name, call examples, and access token, helping you invoke the toolset quickly and avoid failures caused by incorrect domain names, authentication headers, or parameter formats. This topic describes how to obtain call examples.

## Background information

* **Call examples**: The system automatically generates code or configuration examples based on the target toolset. You can copy these examples directly to an IDE, CLI, or other client for use.

   * **Gemini CLI call example**: This applies to CLI tools such as Gemini CLI. For information about how to call an MCP toolset in Gemini CLI, see [Server-specific configuration](https://geminicli.com/docs/tools/mcp-server/#server-specific-configuration-mcpservers).

   * **Trae call example**: This applies to IDE tools such as Trae and Cursor. For information about how to call the MCP toolset in Trae, see [Manually configure the MCP server](https://docs.trae.cn/ide/add-mcp-servers#47a33ec0).

* **Access ** **token:**  An MCP toolset that uses **OAuth JWT** for inbound identity authentication requires an access token as the authentication credential.

## Prerequisites

* You have created an MCP toolset. For details, see [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

* If the toolset uses OAuth JWT for inbound identity authentication, ensure you have obtained an access token before calling the toolset.

## Procedure

### Obtain call examples

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. In the MCP toolset list, find the target toolset and click "Sample call" in the "Actions" column to view call examples.

### Obtain an Access Token

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Gateway" \> "MCP" and click the "MCP Toolset" tab.

3. Click "Sample call" in the "Actions" column of the target MCP toolset.

4. In the "Sample call" section, click "How to obtain Access Token" to view the sample code for generating an Access Token.
