---
title: "Registering agents"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents"
---

A2A agents are services that comply with the A2A protocol and can be discovered and called by other agents. You can register them in an agent space for calling by other agents. In the space, you can manage your A2A agents centrally. This topic describes the preparations before registering an A2A agent and the registration method.

<span id="6N9wjYCf"></span>
## Background information

In single\-agent applications, an agent typically only needs to call tools, knowledge bases, or models to complete tasks. However, in real business scenarios, many tasks are inherently cross\-system, cross\-role, and cross\-team. For example, "Read the sales data, generate an analysis report, submit it for approval, and notify group members". If all capabilities are built into a single agent, that agent will be overloaded with responsibilities, difficult to maintain, and hard for teams to reuse.

Our A2A objective is to enable different agents to collaborate like services. Each agent can provide only one stable capability, such as data analysis, spreadsheet processing, document generation, approval submission, or message notification. After an A2A agent is registered, other agents can discover it through the A2A Center and then initiate calls based on the capabilities, address, and interaction method stated in the AgentCard.

<span id="z6utSKb4"></span>
## Core concepts


|**Concept** |**Description** |
|---|---|
|A2A agent |An agent service that can be discovered and called by other agents through the A2A protocol. |
|AgentCard |An externally exposed agent capability description file that describes information such as the agent name, capabilities, service address, authentication method, and inputs and outputs. |
|JSON file |An agent description file maintained in JSON format. This file can serve as a configuration source when you register an agent. |
|AgentCard address |The URL for accessing the AgentCard. The platform can fetch or update the agent description via this address. |


<span id="EEoi2sQz"></span>
## Prerequisites


*  **(** **Optional)**  You have [created an agent space](https://docs.byteplus.com/en/docs/agentkit/Creating_A2A_agent_spaces).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you have not created an agent space, the agent will be registered to the <code>Default</code> space.   </div>
   

* You have prepared the corresponding resources based on the source of the agent to be registered.

   * **Agent runtime**: Create an agent runtime that complies with the A2A protocol. For example: Use the `a2a` protocol template that comes with the AgentKit CLI to quickly create an agent project and deploy it as an agent runtime. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool)

   * **Custom**:

      * **JSON file**: Prepare a JSON file that complies with the A2A protocol.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">For a sample JSON file, see <a href="https://docs.byteplus.com/en/docs/agentkit/Sample_A2A_agent_JSON_file">Sample JSON file for A2A agent</a>. For the specific definitions, value ranges, and validation rules of all fields in the file, as well as other requirements, see <a href="https://a2a-protocol.org/latest/specification/#441-agentcard">the official A2A protocol documentation</a>.         </div>
         

      * **AgentCard address**: Get the AgentCard address of the A2A agent.


<span id="pAoQOnX9"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. From the A2A agent space drop\-down list, select the target space and click the "Register agent" button.

4. Set the corresponding registration parameters based on the source of the agent to be registered.

   
   <Tabs>
   <Tab zoneid="CAKdGSO4kO" title="Agent Runtime">
   <TabTitle>Agent Runtime</TabTitle>
   
   If you have already created an A2A agent runtime in AgentKit, you can quickly register it to an agent space.
   
   
   |Parameter​ |Description |
   |---|---|
   |Agent Runtime |Select the target A2A agent runtime. |
   |Service endpoint |After an agent runtime is selected, its service address is automatically populated. You can select either a public or private network address based on your needs.<br><br><br>* **Private network:**  Suitable for internal access via VPC. Private network connectivity is free of charge.<br><br>* **Public network:**  Suitable for accessing cloud resources via the Internet. |
   |AgentCard |After the agent is registered, the platform will automatically display the AgentCard details for the agent, including its ID, name, protocol version, communication mode, and other core attributes, as well as the associated A2A agent space. |
   
   
   
   
   
   </Tab>
   <Tab zoneid="dCiOWLSv2p" title="Custom">
   <TabTitle>Custom</TabTitle>
   
   You can register your own or third\-party A2A agents to an agent space, manage them centrally, and provide services externally.
   
   
   |Parameter​ |Description |
   |---|---|
   |Import method |Select the method to import agent information. Supported:<br><br><br>* **JSON file**: Enter JSON information that complies with the A2A requirements to import the agent. Please paste the JSON information into the AgentCard section.<br><br>* **AgentCard address**: Enter the AgentCard address of the A2A agent to import agent information. |
   |AgentCard address |If you select the **AgentCard address** method, enter the AgentCard address of the target A2A agent here and click the "Parse" button. |
   |AgentCard |AgentCard details for the A2A agent.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can edit the agent configuration online as needed, and click the "Parse JSON" button to visually view information such as the agent version, capabilities, and skills.</div><br> |
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Click "Register now" to complete the operation.


<span id="spvgbHM2"></span>
## Related operation

Afterward, you can update the agent's [service address](https://docs.byteplus.com/en/docs/agentkit/Changing_Internet_or_private_network_service_address), [JSON file](https://docs.byteplus.com/en/docs/agentkit/Updating_A2A_agent_JSON_file), [AgentCard address](https://docs.byteplus.com/en/docs/agentkit/Updating_AgentCard_addresses_of_A2A_agents), and [version](https://docs.byteplus.com/en/docs/agentkit/Managing_A2A_agent_versions) as needed based on security, network environment, and other requirements for different business scenarios.
