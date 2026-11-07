---
title: "Adding tools to or removing tools from an MCP toolset"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_MCP_tools"
---

Tools in an MCP toolset are grouped by MCP service. To expand the capabilities that an agent can invoke, add new tools to an existing MCP toolset. If a tool is deprecated, duplicated, or no longer suitable for your scenario, remove it from the toolset. This topic describes how to add tools to or remove tools from an MCP toolset.

## Background information

An MCP tool is a standardized capability unit that an MCP service exposes externally. A model or agent accesses external resources, such as files, databases, APIs, and system commands, through these tools. Adding or removing tools in a toolset changes the capabilities that the toolset exposes externally.

## Prerequisites

* You have created an MCP toolset. For details, see [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

* Before you add a tool, confirm that the target MCP service is available and provides the tool that you need.

## Procedure

### Add MCP tools

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. Click the name of the target toolset. On the "MCP tool" tab, click "Add tool".

4. On the "Add tool" page, select the target MCP service. Then select the tool that you want to add and click "Confirm".

5. After the tool is added, you can view it on the "MCP tool" tab.

### Remove MCP tools

> **warning**

* > Keep at least one MCP tool in the toolset. You cannot remove all tools at once.

* > After a tool is removed, agents or callers that depend on it may experience missing capabilities, failed calls, or changes in retrieval results.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. Click the name of the target toolset. On the "MCP tool" tab, select the tools to remove.

   * **Remove a single tool**: In the "Actions" column for the target tool, click "Remove".

   * **Batch\-remove tools**: Select one or more tools and click "Batch remove" at the bottom of the page.

4. On the confirmation page, click "Remove" to complete the operation. The removed tool no longer appears on the "MCP tool" tab.
