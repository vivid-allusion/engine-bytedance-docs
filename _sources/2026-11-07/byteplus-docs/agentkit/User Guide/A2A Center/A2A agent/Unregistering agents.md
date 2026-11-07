---
title: "Unregistering agents"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Unregistering_A2A_agents"
---

If you no longer want agents registered in the A2A space to be discoverable or callable, you can unregister them from the agent space.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After an A2A agent is unregistered, external agents will no longer be able to call the corresponding agent in that space, which may cause existing call requests to fail. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Unregistering an A2A agent <strong>does not delete its source</strong>, such as the agent runtime. The agent’s service or code still exists, but it can no longer be discovered or called through the current A2A agent space.</div>



<span id="7YNTVeJn"></span>
## Prerequisites

An A2A agent has been registered. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents)

<span id="PfUh4UO0"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. From the A2A agent space drop\-down list, select the target agent space.

4. Click the "Unregister" button in the "Actions" column of the target agent.

5. On the confirmation page, click "Unregister" to complete the operation.
