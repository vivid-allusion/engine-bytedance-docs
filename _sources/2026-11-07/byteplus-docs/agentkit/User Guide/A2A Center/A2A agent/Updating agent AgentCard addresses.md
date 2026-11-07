---
title: "Updating agent AgentCard addresses"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_AgentCard_addresses_of_A2A_agents"
---

When an A2A agent registered via AgentCard undergoes a hosted domain migration, path change, or environment switch, you can update the agent's AgentCard address. After the update, the platform will fetch the agent information via the new address. This topic describes how to update the AgentCard address of an A2A agent.

<span id="WhaacFlg"></span>
## Background information

AgentCard is a standardized agent description document in the A2A protocol. It declares an agent's identity, capabilities, service endpoint, and interaction requirements. The AgentCard address is the source address from which the platform obtains this description document. When the AgentCard's hosted domain, file path, gateway entry point, or deployment environment changes, you need to update the registered agent's AgentCard address promptly to prevent the platform from retrieving invalid or unexpected agent information.

<span id="7qMT0BR1"></span>
## Prerequisites

You have registered an A2A agent whose source is **Custom**, and the import method is **AgentCard**. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents)

<span id="AxNM9o1I"></span>
## Operation instructions


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. From the A2A agent space drop\-down list, select the target agent space.

4. Click the target agent name, then click the "Edit" button in the upper\-right corner.

5. Keep the "Import method" as "AgentCard", and enter the new AgentCard address in the "AgentCard address" section.

6. Click "Register now". On the confirmation page, click "Confirm" to complete the operation.
