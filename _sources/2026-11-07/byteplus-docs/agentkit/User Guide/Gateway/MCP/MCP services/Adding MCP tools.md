---
title: "Adding MCP tools"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Adding_MCP_tools"
---

For an MCP service created using the **HTTP\-to\-MCP** method, you can upload API files at any time to add or update tools. The console converts each API in the file into an MCP tool that agents can call. This topic describes how to add MCP tools to an existing HTTP\-to\-MCP service.

> **warning**

> This topic applies only to MCP services of the **HTTP\-to\-MCP** integration type.

## Background information

An MCP tool is an executable unit exposed externally by an MCP server under the Model Context Protocol (MCP). It encapsulates external capabilities such as files, databases, APIs, or system commands into a standardized interface that models can call.

## Prerequisites

* An MCP service has been created using the **HTTP\-to\-MCP** method. For more information, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

* You have prepared a compliant API file. For the API file specifications, see [MCP service API file specifications and examples](https://docs.byteplus.com/en/docs/agentkit/MCP_service_API_file_specifications_and_examples).

* Confirm that the tool names in the API file do not conflict unintentionally with existing tools. If the newly uploaded API file contains a tool with the same name as an existing tool, selecting "Overwrite existing tool" will replace the existing tool configuration, which may affect agents currently calling that tool.

   ## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. In the service list, click the name of the target service. On the "MCP tool" tab, click "Upload API information".

4. Select how to handle tools with the same name for "If a tool with the same name exists when uploading".

   * **Proceed and overwrite the original tool**: Tools in the API file with the same name as existing tools will overwrite the corresponding tools in the MCP service. Use this option when you have confirmed that the new tool definition is the target version and have assessed the impact on existing callers.

   * **Skip and do not overwrite the original tool**: Existing tools in the MCP service are retained, and tools in the API file with the same name are skipped. Use this option when you are unsure whether the duplicate tools can be replaced, or when you only want to add tools with different names.

5. Click or drag the prepared API file to the console to upload it, and then click "Confirm".

6. After the upload is complete, you can view uploaded tools on the "MCP tool" page.

7. (Optional) Manage uploaded tools. You can click "..." \> "Edit description" or "..." \> "Delete" in the upper\-right corner of the target tool card to edit the tool description or delete the tool.
