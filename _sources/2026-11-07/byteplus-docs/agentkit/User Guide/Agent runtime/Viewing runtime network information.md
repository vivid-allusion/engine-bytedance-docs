---
title: "Viewing runtime network information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_runtime_network_information"
---

When the network configuration of a runtime is set to "Private network" (meaning the runtime is accessible only over a private network), you can view the information of the VPC and subnet IDs associated with the runtime on the details page. You can also navigate to the subnet details page to obtain network parameters such as the subnet CIDR block (IPv4 CIDR), and use them to configure an allowlist in target services such as databases to allow access requests from that private network environment.

<span id="NqCMj2uB"></span>
## Prerequisites

A runtime has been created with the network configuration set to "Private network". For more information, see [Creating runtimes (console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

<span id="DlSi31ab"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the target runtime name to go to the details page.

4. On the "Basic information" tab on the details page, view the subnet ID information.

5. Click the target subnet to navigate to its details page and obtain more detailed subnet information (such as IPv4 CIDR).
