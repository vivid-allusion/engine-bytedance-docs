---
title: "Enabling or disabling semantic retrieval"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Enabling_or_disabling_semantic_retrieval"
---

To reduce the usage cost for callers caused by forgetting agent names or manual route maintenance, agent spaces provide the semantic search capability. This topic describes how to enable and disable the semantic retrieval feature for an A2A agent space.

<span id="lZy23tXr"></span>
## Background information

When there are only a few agents in an agent space, callers can typically specify the target agent by using a fixed name, fixed ID, or explicit routing logic. However, in scenarios involving multi\-team collaboration or finer capability granularity, or more natural\-language task descriptions, callers often do not know which agents are suitable. In this case, the semantic retrieval feature enables automatically matching a more suitable agent within the space based on the user's task intent, agent name, description, and capability boundaries.

<span id="papyI0Nd"></span>
## Applicable scenario

<span id="lJBwkZpe"></span>
### Enable semantic retrieval


* **Cross\-team agent reuse**

   When data, operations, documentation, approval, and other capabilities are maintained by different teams, you can register approved agents into the same space. Callers only need to retrieve and call agents within the space, without having to learn each agent's external service address individually.

* **Automatic breakdown and routing of complex tasks**

   When the user's input is a near\-natural\-language task, such as "Analyze last week's sales changes and generate a review", the primary agent needs to first match a data analysis agent in the space, and then call a document generation agent or a message notification agent.


<span id="lgTSxCBv"></span>
### Disable semantic retrieval


* **Fixed orchestration of production chains**

   If a production chain must always call a specific target agent, such as in risk control review, order fulfillment, or rule calculation scenarios, it is usually safer to disable semantic retrieval. This way, callers can select the target based on a fixed identifier or business logic, reducing the risk of mismatching.

* **Testing and verification**

   If an agent is in the joint testing, acceptance review, or troubleshooting stage, you can disable semantic retrieval first to eliminate uncertainties from the matching chain, making it easier to identify issues in capabilities, configurations, or returned results.


<span id="zMkgQ4sv"></span>
## How it works

When semantic retrieval is enabled for the first time, the platform constructs an index based on the key descriptive information of agents in the space (to understand "what tasks this agent is suitable for"), and then retrieves relevant agents based on the caller’s natural\-language task input. When an agent is newly registered or updated, automatic synchronization will be triggered to construct or refresh the index.

After semantic retrieval is disabled, the platform does not immediately clear the existing index but only stops constructing new indexes. The discovery method for agents within the space changes from "intent\-based matching" to "fixed target selection". When semantic retrieval is re\-enabled, only the indexes for agents added or updated during the period are refreshed, and existing data can be reused directly.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When an agent is unregistered, the platform automatically clears the corresponding index. The platform monitors and manages frequent registration and deregistration to avoid additional costs caused by abnormal operations.</div>


<span id="WdwzCP19"></span>
## Prerequisites

You have created an agent space. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Creating_A2A_agent_spaces)

<span id="R7l5uMMt"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. In the A2A agent space drop\-down list, find the target A2A agent space, then click "... \> Edit" on the right.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e57aae1c33c6b3df21817f86824092dd.png) </span>

4. In the "Agent semantic retrieval" section, click the toggle to enable or disable the agent semantic retrieval feature.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before enabling the semantic retrieval feature, make sure that the agent name, description, and capability boundaries of agents registered to the space are clear. Otherwise, multiple similar candidates may be returned, or a wrong agent may be matched.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you disable the semantic retrieval feature, when agents call the A2A agent space, returning best\-matching agents based on call intent is no longer supported. This operation may affect the dynamic discovery of agents. Proceed with caution.   </div>
   

5. Click "Confirm" to complete the procedure.


<span id="sMDUTJOc"></span>
## Verify results

After enabling semantic retrieval, you can call the [SearchAgentCards](https://docs.byteplus.com/en/docs/agentkit/SearchAgentCards_-_Queries_agents_via_intent_recognition?lang=en) API and pass a natural\-language task in the `Prompt` that closely reflects the real business scenario. If the API returns the `TopK` best\-matching agents, it indicates that agents have been successfully discovered and queried dynamically based on the call intent.
