---
title: "Enabling or disabling public network resolution for private domains"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Enabling_or_disabling_public_network_resolution_for_private_domains"
---

When you need to **test** resources (such as MCP services) through a private domain on the AgentKit platform, but your local machine is not configured to forward DNS requests to the BytePlus private DNS, you can enable public network resolution for the private domain so that public recursive DNS can also resolve it. This makes it easier to complete domain name resolution verification in a public network environment. This topic describes how to enable or disable public network resolution for private domains for resources under a ** dedicated gateway** or ** a shared gateway**.

## Instructions

* Public network environments are complex and cannot guarantee the accuracy or timeliness of domain name resolution, so we recommend using this feature ** only in non\-production environments**. For production environments, we recommend that you use DNS Forward to forward local DNS requests to the BytePlus private DNS for more stable resolution.

* After public network resolution, the result is still a private IP address (the PrivateLink Endpoint address), which is not publicly accessible. In other words, the ** resolution result remains unchanged**.

* After you enable or disable public network resolution, resolution may not take effect or may fail for a short period. Wait for the DNS cache to refresh.

## Prerequisites

* Your client network already has network connectivity to the target VPC (for example, established through a VPN or Direct Connect). For related configuration, see [Direct Connect - Best practices](https://docs.byteplus.com/en/docs/directconnect/best-practices-overview?lang=en).

* **Dedicated gateway**: You have created a dedicated gateway instance whose network access mode includes private network access. You can view the gateway network access mode in the configuration information of the dedicated gateway instance. For details, see[ Creating gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances?lang=en).

* **Shared gateway**: Based on your actual testing needs, create the required resource (such as an MCP service) and make sure its network access mode includes private network access. You can view the network access mode in the resource's configuration information.

   * MCP service: [Create an MCP service](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

   * MCP toolset: [Create an MCP toolset](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset).

   * Agent runtime: [Create a runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

## Procedure

### Dedicated gateway

If the gateway mode of the resource to be tested is **dedicated gateway**, you need to enable or disable public network resolution for private domains in the dedicated gateway instance.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, click the name of the target gateway instance.

3. In the "**Network configuration**" section of the "**Configuration information**" tab, under "Private domain name public network resolution", click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7bc931226e49ac6c47615e764762697c.png).

4. Enable or disable the public network resolution for private domains feature.

   * **Enable**: In the dialog box that appears, click "Enable" to enable the public network resolution for private domains feature.

   * **Disable**: In the dialog box that appears, click "Disable" to disable the public network resolution for private domains feature.

### Shared gateway

If the gateway mode of the resource to be tested is ** shared gateway**, you need to go to the corresponding resource to enable or disable public network resolution for private domains.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. Go to the details page of the target resource.

   * **MCP service**: In the left\-side navigation pane, select "Gateway \> MCP". On the "MCP Service" tab, click the name of the target MCP service.

   * **MCP toolset**: In the left\-side navigation pane, select "Gateway \> MCP". On the "MCP Toolset" tab, click the name of the target MCP toolset.

   * **Agent runtime**: In the left\-side navigation pane, select "Agent Runtime" and click the name of the target agent runtime.

3. In the "**Network configuration**" section of the "**Configuration information**" tab, under "Private domain name public network resolution", click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7bc931226e49ac6c47615e764762697c.png).

4. Enable or disable the public network resolution for private domains feature.

   * **Enable**: In the dialog box that appears, click "Enable" to enable the public network resolution for private domains feature.

   * **Disable**: In the dialog box that appears, click "Disable" to disable the public network resolution for private domains feature.
