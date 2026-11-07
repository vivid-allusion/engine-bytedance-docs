---
title: "Updating associated components"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_configuration"
---

This topic describes how to associate new components or update existing associated components.

<span id="zn1d6xSV"></span>
## Usage notes


* **Version requirement**: In preview mode, you can update the configuration only for the Latest version. In non\-preview mode, you do not need to specify a version and can update directly.

* **Effective conditions**: After updating associated components, **republish** the agent runtime. The new configuration then takes effect, and a new version is created. Once published, the latest version is automatically used for subsequent agent runtime calls. [View release history](https://docs.byteplus.com/en/docs/agentkit/Viewing_release_history).


<span id="10osqA9Y"></span>
## Association limits


* The network access method of the associated component must be the same as that of the agent runtime. Otherwise, the association fails.

* Before you associate a component, make sure that the agent deployed in the agent runtime has been integrated with the target component. Otherwise, the system cannot inject the required environment variables, and the agent cannot call the component features.

   For information about how to integrate different components, see the following topics:

   * [Integrating sandbox templates in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_tools_in_agent): enables the agent to call an isolated environment to complete code execution, browser tasks, and other complex tasks.

   * [Integrating session resources in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_session_resources_in_agents): provides the agent with short\-term memory management capabilities and is responsible for persistent session connection and context management.

   * [Integrating memories in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_memories_in_agent): provides the agent with enterprise\-grade long\-term memory management capabilities. This enables cross\-session context awareness, personalized interaction, and continuous learning and evolution for the agent.

   * [Integrating knowledge bases in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_knowledge_base_in_agent): calls APIs to integrate knowledge base capabilities, enabling maintainable, updatable, traceable, and low\-cost agents.

   * [Integrating MCP services in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_MCP_service_in_agent): enables rapid enhancement of interaction capabilities between large models and existing systems without code changes.


<span id="xApEhgpf"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. Click the "Associated components" tab, and then perform the following operations as needed in the target component area:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In preview mode, configuration updates are supported only for the Latest version. Switch the version to Latest before you perform the operation.   </div>
   

   * Click "Associate now" to add a component.

   * Click "Edit" to update an associated component.

5. In the dialog box, select the target component and click "Confirm".

6. Publish the agent runtime to apply the configuration.

   * Preview mode: Click "Save" to save the configuration. After you save the configuration, you can test the Latest version or[ publish it as an official version](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes).

   * Non\-preview mode: After updating the configuration, click "Release" in the upper\-right corner of the page. The new configuration takes effect only after republishing.
