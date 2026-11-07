---
title: "Deleting MCP toolsets"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Deleting_MCP_toolsets"
---

If an MCP toolset is no longer used by any agent, workflow, or external caller, or if you plan to recreate a toolset of the same type with a new configuration, you can delete it. This topic describes how to delete an MCP toolset.

> **danger**

* > **A deleted MCP toolset cannot be recovered**. Proceed with caution. If any agent or caller still depends on the toolset, deleting it will immediately cause call failures.

* > If you only want to temporarily stop using a toolset, first evaluate whether adjusting the call configuration or removing specific tools can meet your needs. For more information, see [Adding tools to or removing tools from an MCP toolset](https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_MCP_tools). Only delete the toolset when you have confirmed that it is completely no longer needed.

## Prerequisites

You have created an MCP toolset. For details, see [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. In the MCP toolset list, find the target MCP toolset and click "Delete" in the "Actions" column to delete the toolset.
