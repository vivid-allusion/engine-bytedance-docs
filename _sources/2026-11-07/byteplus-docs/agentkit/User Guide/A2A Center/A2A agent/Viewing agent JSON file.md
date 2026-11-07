---
title: "Viewing agent JSON file"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_A2A_agent_JSON_file"
---

After registering an A2A agent, you can view the agent's registration, verify the protocol declarations, externally exposed capabilities, and other information through the agent JSON file. This topic describes how to view the JSON file of an A2A agent.

<span id="Jnx5OvpY"></span>
## Background information

The JSON file of an A2A agent describes the agent's basic information, communication protocol, and service entry point, and declares some of its capabilities. It is a structured description that enables external systems to understand "who the agent is, what it can do, and how to access it".

In A2A collaboration scenarios, callers typically need to first obtain and parse this description, and then decide whether to proceed with capability discovery, task calling, or compatibility validation. Therefore, when encountering issues such as "The agent is visible but unavailable", "Field declaration does not match actual service", or "Cross\-system access failed", you usually need to start troubleshooting by checking the JSON file.

<span id="0PCu7nwd"></span>
## Prerequisites

An A2A agent has been registered. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents)

<span id="SpwOjSGi"></span>
## Operation instructions


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. From the A2A agent space drop\-down list, select the target agent space.

4. Click the target agent name, then click the "JSON file" button in the upper\-right corner.

5. On the JSON file display page, you can view and copy the code information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For the specific definitions, value ranges, and validation rules of all fields in the JSON file, as well as other requirements, see <a href="https://a2a-protocol.org/latest/specification/#441-agentcard">the official A2A protocol documentation</a>.   </div>
