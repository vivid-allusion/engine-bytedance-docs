---
title: "Building agent teams with one click"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Building_agent_teams_with_one_click_"
---

You can build a dedicated agent team for ArkClaw, allowing multiple intelligent roles to perform their respective duties and independently handle assigned business tasks. In addition, the primary agent can automatically identify and assign tasks to matching sub\-agents to enable multi\-role collaboration.

Main advantages:


* **Flexible identity switching**

   You can switch to the appropriate agent identity with one click based on task requirements. For example, you can switch from "Recruitment specialist" to "Technical review expert", which enables a smooth transition across domains.

* **Lower O&M costs**

   All agents share the same underlying ArkClaw instance resources. You do not need to create or maintain separate ArkClaw instances for different businesses, nor do you need to modify configurations repeatedly. This significantly reduces resource consumption and routine O&M costs.

* **Intelligent task distribution**

   The primary agent can, based on business workflows and actual scenarios, automatically break down and assign tasks to each sub\-agent via conversational commands. This enables multi\-role collaboration and parallel task processing, greatly increasing overall task efficiency.


<span id="RQEi3PBg"></span>
## Prerequisites

You have purchased an ArkClaw instance as the primary agent. For details, refer to [Creating your dedicated ArkClaw with one click](https://docs.byteplus.com/en/docs/ArkClaw/Creating_your_dedicated_ArkClaw_with_one_click_).

<span id="N9uaAyy3"></span>
## Create an agent team

<span id="u5ZTkA4h"></span>
### Specify the primary agent, and then create a team for it

This method is applicable to scenarios where the target ArkClaw (primary agent) is already specified and other agents need to be added to its team.


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Go to the target ArkClaw page.

3. Select "ArkClaw intelligent assistant \> Add agent".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If "ArkClaw intelligent assistant" is grayed out, click "Initiate task" in the left navigation pane. Then, click "ArkClaw intelligent assistant \> Add agent".   </div>
   

4. (Optional) If this is your first time using the agent team feature, click "Upgrade now" to upgrade the agent team plugin. If you have installed the plugin, skip this step.

5. Select the template that fits your business scenario, and click the "Add to agent team" button to add it to the Claw team.

   > Several high\-quality templates are available by default (containing skill plugins, soul settings, standard permission rules, etc.). For a complete list and capability descriptions of the preset templates, see [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_Agent_Gallery_templates_).   
   

6. After the team is built, you can communicate with the primary agent or other agents via ArkClaw to quickly explore their capabilities or handle business tasks.

   * **Chat with the primary agent: ** Enter a message in natural language in its chat box to start a conversation.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When you initiate a conversation via the primary agent, it will automatically determine whether there are sub\-agents in the team matching the task requirements.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If there are matching sub\-agents: The system will automatically assign the task to the most suitable sub\-agent, which will process it and return the result.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If there are no matching sub\-agents: The primary agent will directly undertake and handle the task, and return the result upon completion.      </div>
      

   * **Chat with other agents**

      1. In the left\-side navigation pane, click "Initiate task".

      2. Click "ArkClaw intelligent assistant" in the chat box, then select the target agent.

      3. After the switching, enter a message in natural language in the chat box of the target agent to initiate a conversation.


<span id="rZ1lNktp"></span>
### **Start with another agent, and then add it to ArkClaw**

This applies to scenarios where you first select a target agent (preset template) from Agent Gallery, and then add it to a specified ArkClaw (primary agent).


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/management).

2. In the left navigation pane, click "Agent Gallery".

3. Select the template that fits your business scenario, and click the "Add to agent team" button.

   > The platform provides several templates (containing skill plugins, soul settings, standard permission rules, etc.). For a complete list and capability descriptions of the preset templates, see [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_Agent_Gallery_templates_).   
   

5. (Optional) If the following page appears, click "Upgrade now" to upgrade the plugin. 

6. After the agent team plugin is installed, select the template that fits your business scenario, and click the "Add to agent team" button to add it to the Claw team.

7. After the team is built, you can communicate with the primary agent or other agents via ArkClaw to quickly explore their capabilities or handle business tasks.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you initiate a conversation via the primary agent, it will automatically determine whether there are sub\-agents in the team matching the task requirements.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If there are matching sub\-agents: The system will automatically assign the task to the most suitable sub\-agent, which will process it and return the result.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If there are no matching sub\-agents: The primary agent will directly undertake and handle the task, and return the result upon completion.   </div>
   

   1. In the left\-side navigation pane, click "Initiate task".

   2. Click "ArkClaw intelligent assistant" in the chat box, then select the target agent.

   3. After switching, enter a message in natural language in the chat box of the target agent to initiate a conversation.


<span id="tSEvHmSj"></span>
## Delete an agent

You can only delete an agent added from [Agent Gallery](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_Agent_Gallery_templates_) here, and the associated Claw must be in **Package expired** or **Stopped** status. **Deleting the primary agent is not supported**. For information about how to delete the primary agent, refer to [Deleting ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Deleting_ArkClaw_).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you delete an agent, all conversation records and data of the agent will be <strong>permanently deleted and cannot be restored</strong>. Proceed with caution.</div>



1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page. In the upper\-right corner of the page, click the details icon.

3. On the ArkClaw details page, click the "Agent team" tab.

4. Select the target agent from the agent list on the left.

5. Click “··· \> Delete agent”.

6. Confirm that the agent to be deleted is correct, and then click the "Delete" button to complete the operation.
