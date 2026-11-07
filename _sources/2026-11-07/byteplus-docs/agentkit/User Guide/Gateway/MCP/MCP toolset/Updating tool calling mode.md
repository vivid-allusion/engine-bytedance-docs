---
title: "Updating tool calling mode"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_tool_calling_mode"
---

The tools in an MCP toolset support multiple calling modes to accommodate different application scenarios. When the toolset grows in size, the caller type changes, or you want to improve tool selection efficiency, you can adjust the calling mode of the MCP toolset. For example, when the number of tools is small, returning all tools directly is appropriate. When the number of tools is large, switching to semantic or tag\-based retrieval is more suitable to reduce the number of irrelevant tools exposed to the model. This topic describes how to update the calling mode of a tool.

> **warning**

> After you update the calling mode of a tool, the tool information returned by the MCP toolset will change. Proceed with caution.

## Background information

Currently, the following calling modes are supported.

|**Calling mode** |Description |**Application scenarios** |
|---|---|---|
|Full return |Returns all tools within the MCP toolset. |This mode is suitable for scenarios with a small number of tools, such as fewer than 20. |
|Semantic retrieval |Performs semantic matching based on the task request and tool descriptions, returning the most relevant tool. |This mode is suitable for scenarios with a large number of tools called by general\-purpose agents. |
|Tag retrieval |Filters tools by specified tags, returning tools that meet the criteria. |This mode is suitable for scenarios with a large number of tools where the caller is a domain\-specific agent. |

## Prerequisites

You have created an MCP toolset. For details, see [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. In the MCP toolset list, click the target toolset name. On the "Basic information" tab, click "Edit" next to "Calling mode".

4. Select the desired calling mode and click "✓" to complete the operation.
