---
title: "A2A Center overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/A2A_Center_overview"
---

A2A Center offers unified A2A\-protocol\-based agent access and management. With standard protocol communication powered by the underlying gateway, it helps you register, organize, discover, call, and govern agent versions. This topic describes the core concepts, component relationships, and working principles of A2A, providing a basis for your subsequent operations.

<span id="3aPTzdWr"></span>
## What is A2A Center

The A2A Center is a capability center in AgentKit for accessing, managing, and discovering A2A agents, mainly addressing issues such as **scattered agent assets**, **difficult capability search**, and **difficult collaboration maintenance**. The objects it manages are not individual models or tools, but agent services that provide capabilities externally based on the Agent to Agent ([A2A](https://a2a-protocol.org/latest/specification/)) protocol. Through the A2A Center, you can register the agents scattered across different businesses, teams, or systems into one space, and organize, retrieve, and govern them by space.

You can regard the A2A Center as a "directory" used for agent collaboration. Callers check it to see "which agents are available, what they can do, and how to access them", then select the appropriate agents and call them as needed.

<span id="u7NTWwrH"></span>
## Applicable scenarios

The A2A Center is suitable for scenarios where multi\-agent collaboration has become a necessity and no single agent is suitable for taking on all the responsibilities. The most typical case is that business workflows essentially consist of multiple specialized roles. For example, a control agent receives user requests, a retrieval agent collects information, and then the planning agent, execution agent, and domain expert agent respectively complete the subsequent processes. In this case, the A2A Center can turn these role capabilities into agent assets that are discoverable, reusable, and governable.

<span id="Ya0XUlMA"></span>
### **Role\-based collaboration within enterprises**

The customer service control agent needs to call the "Knowledge retrieval agent", "Permission diagnosis agent", and "Fulfillment compensation agent" when troubleshooting based on tickets. The R&D assistant needs to call the "Code analysis agent", "Documentation Q&A agent", and "Release check agent". The A2A Center enables centralized registration of these specialized capabilities, allowing upper\-layer agents to discover and call them as needed.

<span id="UyBTmAfh"></span>
### **Capability sharing across teams or systems**

When different teams maintain their own agent services, if every caller has to manually maintain the connection addresses, fields, and versions, the collaboration cost will rise significantly. Through the A2A Center, callers can first discover agents through the unified space and metadata, and then initiate calls based on standardized agent descriptions, reducing coupling.

<span id="a34xsQKB"></span>
### **Dynamic discovery and semantic matching**

If there are many agents on the platform, callers may not know in advance which agent to search for. In this case, you can leverage agent spaces and the semantic retrieval capability to find a suitable agent based on the task intent, and the upper\-layer orchestration logic then decides whether to call this agent. This capability is especially well suited to plugin marketplaces, enterprise capability platforms, or autonomous multi\-agent systems.

<span id="z5WvyBlo"></span>
### **Canary evolution and version governance**

When an agent's capabilities are continuously upgraded, or multiple versions need to be maintained in parallel, the version management, JSON update, and Agent Card address update capabilities provided by the A2A Center allow users to iterate capabilities without interrupting collaboration.

<span id="Ny3NoL4L"></span>
## Related concepts


|Concept |Description |
|---|---|
|**A2A protocol** |The [Agent to Agent](https://a2a-protocol.org/latest/specification/) protocol refers to the collaboration protocol between agents. Its focus is not on how an agent thinks, but on how different agents complete discovery, capability description, task initiation, message exchange, result returning, and asynchronous status tracking across frameworks, languages, and vendors. |
|**Agent space** |A logical space in AgentKit used for organizing and managing A2A agents. It is used to distinguish environments (dev/staging/prod), business lines, and tenants. Business applications can discover, schedule, and interact with external agents based on A2A agent spaces. |
|**A2A agent** |An agent service that has exposed its capabilities according to the A2A protocol, typically providing discoverable, callable, and describable interface capabilities. |
|**AgentCard** |* AgentCard is a standard JSON agent card defined by the A2A protocol. Any compliant A2A agent must expose it at a fixed path. It is used for automatic discovery of remote agents, communication negotiation, and declaration of authentication rules, and records the agent’s identity, service endpoint, all skills, and access security specifications.<br><br>* When registering an agent in an A2A agent space, you can import a third\-party A2A agent with one click by providing the AgentCard address, supporting autonomous cross\-instance agent collaboration and scheduling. |
|**Agent JSON file** |The agent’s registration record in AgentKit, used to declare agent metadata in a structured way, such as basic information, capability descriptions, service entry point, and versions. |
|**Version** |As A2A agents iterate continuously, protocol declarations, service addresses, capability descriptions, and runtime configurations may change. To avoid directly overwriting online information with every modification, the platform retains configuration information for different versions, helping you track historical changes, confirm the current default version, and clear them when necessary. |


<span id="bW3QBpkb"></span>
## **Core features**


* **Agent registration management**

   * Supports one\-click registration through the console during or after the creation of an AgentKit agent runtime instance. When an agent version is updated, registration and unregistration can be completed automatically.

   * Supports registration of external custom agents by importing a JSON file or configuring an AgentCard address.

* **Agent discovery**

   * Supports fuzzy search for agents by name and version.

   * Supports returning highly matched agents within an A2A agent space based on the entered intent.

   * Supports fuzzy search for A2A agents by skill, skill tag, and agent description.

* **Environment isolation**

   * Different A2A agent spaces are isolated from each other and operate independently. Agent spaces can be used to distinguish different development environments, business lines, or tenants.


<span id="7rVW6Q5H"></span>
## Procedure


1. [Create an A2A agent space](https://docs.byteplus.com/en/docs/agentkit/Creating_A2A_agent_spaces): Create an A2A agent space to centrally manage A2A agents, making it easy to call A2A agent applications.

2. [Register A2A agents](https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents): Register A2A agents to the A2A agent space. You can register A2A agents running in runtime, or register other external agents by importing JSON files or providing AgentCard addresses.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each A2A agent can be registered to multiple A2A agent spaces.   </div>
   

3.  **(Optional) Call A2A agents**: Once registered, A2A agents can be called as A2A agent resources by other agent applications. Take ArkClaw Enterprise as an example. After an AgentKit A2A agent is registered in the Application Center, users can instruct ArkClaw to call the agent via natural language or the `@ `command on the user side. For more information, see [Best practices for resource registration and use in Application Center](https://docs.byteplus.com/en/docs/ArkClaw/Best_practices_for_resource_registration_and_use_in_the_Application_Center?lang=en).

4. **Continuously operate and maintain A2A agents**: As agent capabilities evolve, you can maintain agents registered in the A2A Center by [updating the JSON file](https://docs.byteplus.com/en/docs/agentkit/Updating_A2A_agent_JSON_file), [updating the Agent Card address](https://docs.byteplus.com/en/docs/agentkit/Updating_AgentCard_addresses_of_A2A_agents), and [managing agent versions](https://docs.byteplus.com/en/docs/agentkit/Managing_A2A_agent_versions). You can also [unregister](https://docs.byteplus.com/en/docs/agentkit/Unregistering_A2A_agents) agents that no longer provide services, ensuring that collaboration relationships remain maintainable and traceable during long\-term operation.
