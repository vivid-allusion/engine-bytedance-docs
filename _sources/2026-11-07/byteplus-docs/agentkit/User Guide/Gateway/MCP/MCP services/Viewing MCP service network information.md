---
title: "Viewing MCP service network information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_service_network_information"
---

When the network configuration mode of an MCP service is set to "Private network" (that is, the MCP service is accessible over a private network), you can view its associated VPC and subnet IDs on the details page. You can go to the subnet details page to obtain network parameters such as the subnet CIDR block (IPv4 CIDR) and add these network parameters to the allowlist of the database or other target services. After you configure the allowlist, the target service can accept access requests from the MCP service's private network environment.

### Scenarios

* The MCP service needs to access target services, such as databases, caches, or internal APIs, over a private network.

* The target service requires an allowlist of source CIDR blocks.

* You need to troubleshoot issues such as private network access failures, connection timeouts, or allowlist misconfigurations.

## Prerequisites

You have created an MCP service and configured it with "Private network" during creation. For details, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. In the MCP service list, click the name of the target MCP service. On the "Basic information" tab of the details page, view the VPC or subnet ID.

4. Click the target VPC or subnet ID to go to the corresponding details page for more information, such as the IPv4 CIDR block.
