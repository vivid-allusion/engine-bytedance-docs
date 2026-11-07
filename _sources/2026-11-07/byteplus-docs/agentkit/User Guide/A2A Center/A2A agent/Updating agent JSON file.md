---
title: "Updating agent JSON file"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_A2A_agent_JSON_file"
---

When the business capabilities, description, externally exposed skills, or version definitions of a **custom**\-source A2A agent change, you can update the agent configuration by editing its JSON file. This topic describes how to update the JSON file of an A2A agent.

<span id="Loe77IrW"></span>
## Background information

When you register an A2A agent using a JSON file or AgentCard, the platform saves the agent's configuration information based on the imported content and uses it for subsequent discovery, version management, and calling. Updating the JSON file is not just maintaining document fields. This operation adjusts the agent's basic metadata that defines how the agent is recognized by the platform, how it is discovered by other agents, and what configuration is used when it is called.

When the business capabilities, description, externally exposed skills, or version definitions change, you need to update the JSON file accordingly to avoid affecting normal use by callers.

<span id="aEZr49XB"></span>
## Prerequisites

An A2A agent from a **Custom** source has been registered. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents)

<span id="zYzL46YJ"></span>
## Operation instructions


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. From the A2A agent space drop\-down list, select the target agent space.

4. Click the target agent name, then click the "Edit" button in the upper\-right corner.

5. In the "AgentCard" section, adjust the JSON configuration as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For a sample JSON file, see <a href="https://docs.byteplus.com/en/docs/agentkit/Sample_A2A_agent_JSON_file">Sample JSON file for A2A agent</a>. For the specific definitions, value ranges, and validation rules of all fields in the file, as well as other requirements, see <a href="https://a2a-protocol.org/latest/specification/#441-agentcard">the official A2A protocol documentation</a>.   </div>
   

6. After completing the update, click "Register now". On the confirmation page, click "Confirm" to complete the operation.

   * If this update involves the `version` parameter, the platform will generate a new A2A agent version and automatically set it as the default version for agent calling.

   * If this update does not involve the `version` parameter, the platform will overwrite the parameter settings of the current version.
