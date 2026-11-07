---
title: "Testing MCP toolsets"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Testing_MCP_toolset"
---

You can test an MCP toolset in the console to verify domain connectivity, identity authentication, and tool parameters before integrating it. This helps you identify tool selection errors, parameter configuration errors, or authentication anomalies in advance, preventing task interruptions caused by unavailable tools during actual agent calls. This topic describes how to test an MCP toolset.

> **warning**

* > **Network information**: Public network domain name testing is available to all users. Private network domain name testing is currently in **Beta**and can be used only after it is enabled. To request access, contact your account manager.

* > **Billing note**: Operations on the Test tab, such as connection tests, tool retrieval, and tool calls, follow the same logic as calling an MCP service or MCP toolset through code. **All of these operations go through the gateway and count toward the usage of the corresponding billing items**. Control the testing frequency to avoid unexpected charges. For more information about billing rules, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).

* > **Call description**: After an MCP toolset is created, when a request is sent to the MCP toolset, the MCP toolset accesses the associated MCP service to call tools. The number of generated requests is counted toward the usage statistics of**both the MCP toolset and the MCP service**. For more information, see[Instructions on MCP request count](https://docs.byteplus.com/en/docs/agentkit/MCP_request_counting_rules).

## Background information

MCP toolsets support different calling modes. Before testing a toolset, we recommend confirming which mode the toolset uses. The mode determines how you select a test tool.

|**Calling mode** |Method for selecting a testing tool |
|---|---|
|Full return |The system directly returns all tools in the MCP toolset. Select the target tool from the list to start testing. |
|Semantic retrieval |You need to enter a natural language description that matches the tool's purpose. The system returns candidate tools based on the description. This mode is suitable for scenarios with a large number of tools called by general\-purpose agents. |
|Tag retrieval |Filter for tools by tag, and then select the target tool. This mode is suitable for scenarios with a large number of tools that have already been categorized by domain or purpose using tags. |

## Prerequisites

* You have created an MCP toolset. For details, see [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

* (Optional) If you use a private network domain name for MCP testing, ensure that your local machine is connected to the target VPC through Direct Connect, VPN, or another method and can resolve the private network domain name. Otherwise, the connection test will fail. If your local machine is not configured to forward DNS requests to the BytePlus private DNS, you can enable public network resolution for the private network domain name.

   * **For private network connection configuration, see** [Direct Connect - Best practices](https://docs.byteplus.com/en/docs/directconnect/best-practices-overview?lang=en).

   * **Enable public network resolution for private domain names**: Configure based on the gateway mode to which the MCP service belongs. For more information, see [Enabling or disabling public network resolution for private domains](https://docs.byteplus.com/en/docs/agentkit/Enabling_or_disabling_public_network_resolution_for_private_domains).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. In the list, click the name of the target toolset. On the "Test" tab, follow the on\-screen instructions to verify the tools in the MCP toolset.

   * **Step 1**: In the "Select a domain name and then access it for testing" step, click "Connection test". The system automatically populates the public domain name of the toolset and the API Key or Access Token required for inbound identity authentication. You do not need to provide them manually.

      * **Domain name**: The domain name for accessing the MCP toolset over the public network.

      * **API Key or Access Token**: The credential used to authenticate inbound requests to the MCP toolset.

   * **Step 2**: (Optional) For toolsets whose call method is "Tag retrieval" or "Semantic retrieval", you need to filter for the target tools by tag or natural language.

      * **Tag retrieval**: Select the tag of the tools to test.

      * **Semantic retrieval**: Enter natural language text to filter for the target tools, and then click "Search tool".

   * **Step 3**: In the "Select the tool to be tested" step, select the tools to test.

   * **Step 4**: In the "Enter parameters for testing" step, enter the testing parameters as needed and click "Testing tool" to complete the operation.

4. If the **Test succeeded** message is returned, the MCP toolset's connectivity is normal.
