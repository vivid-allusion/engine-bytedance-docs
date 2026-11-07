---
title: "Changing agent's public or private network service address"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Changing_Internet_or_private_network_service_address"
---

If your A2A agent is sourced from an **agent runtime** that supports access via both public and private networks, you can change its service address based on your business's network access scope and requirements, adapting to different network environments and security needs. This topic describes how to change your agent's service address.

<span id="apEV703p"></span>
## Prerequisites

An A2A agent whose source is an **agent runtime** has been registered, and the agent runtime supports access via both public and private networks. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents)

<span id="e4vP1YeG"></span>
## Service address selection suggestions


|**Address type** |**Applicable scenario** |
|---|---|
|Private network address |The caller and the target agent are located within the same private network or a controlled network environment, and only intranet connectivity is required. |
|Public network address |The caller is located on the internet side, crosses network boundaries, or cannot directly access the target private network. |


<span id="6NbOFeKw"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. From the A2A agent space drop\-down list, select the target agent space.

4. Click the target agent name and select the "Basic information" tab.

5. Click the edit icon in the "Service address" section.

6. In the "Edit service address" section, select the new service address from the drop\-down list.

7. Click "Confirm" to complete the procedure.


<span id="20poaaSW"></span>
## Subsequent operations

After changing the agent service address, **please promptly update the caller configuration** and initiate a real request to verify that the request can be routed to the new address and the response is as expected. Otherwise, agent calls may be interrupted or fail, or communication errors may occur, affecting normal business operation.
