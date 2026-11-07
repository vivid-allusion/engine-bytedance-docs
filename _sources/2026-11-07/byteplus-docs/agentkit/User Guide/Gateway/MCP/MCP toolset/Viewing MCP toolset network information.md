---
title: "Viewing MCP toolset network information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_toolset_network_information"
---

When the network configuration of an MCP toolset is set to "Private network" (that is, the MCP toolset is accessible over a private network), you can view the VPC and subnet IDs associated with the toolset on the details page. You can add this information to the allowlist of a database or other target services. After the allowlist is configured, the target services can allow inbound access requests from the MCP toolset's private network environment.

## Prerequisites

You have created an MCP toolset with **private network access** configured for it. For details, see [Creating MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Toolset" tab.

3. In the MCP toolset list, click the name of the target MCP toolset. On the "Basic information" tab of the details page, view the VPC/Subnet ID.

4. Click the target private gateway/subnet to open its details page to view details (for example, IPv4 CIDR).
