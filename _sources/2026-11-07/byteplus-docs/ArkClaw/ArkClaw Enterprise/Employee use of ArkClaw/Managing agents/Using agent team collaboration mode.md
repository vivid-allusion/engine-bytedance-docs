---
title: "Using agent team collaboration mode"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_agent_team_collaboration_mode"
---

In agent team collaboration mode, the primary agent serves as the orchestrator: It delegates work to sub\-agents as needed, automatically links the entire workflow, and quickly starts a standardized orchestration task. This mode is suitable for scenarios with unclear boundaries that require comprehensive judgment, cross\-checking, multi\-perspective summary output, and parallel handling of subtasks by multiple specialized roles.

You can enable or disable this capability as needed.


* **Enable agent team collaboration mode (default)** 

   After the agent team collaboration mode is enabled, you can trigger a team workflow in either of the following ways:

   * **Automatically triggered**: The primary agent determines whether collaboration is required based on the task content and complexity from the user input. It then prioritizes assigning suitable sub\-agents to collaborate on tasks.

   * **Triggered manually**: You can manually start a team workflow during the conversation and specify the sub\-agents to participate in the collaboration. This method is suitable for scenarios where the task boundaries are clear and you want precise control over the collaboration scope.

* **Disable agent team collaboration mode**

   After the team collaboration mode is disabled, requests no longer automatically trigger team workflow orchestration. Tasks are handled independently by the primary agent based on its own configuration, and sub\-agents are not automatically matched or called.


<span id="m323iVFT"></span>
## Limits


|Limit item |Description |
|---|---|
|Agent |This feature can only be configured on the **primary agent**. Sub\-agents do not support this configuration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The agent whose ID is <strong>main</strong> is the <strong>primary agent</strong>. For details about how to view the agent ID, see the procedure below<strong>.</strong></div><br> |
|ArkClaw specifications and versions |* **Instance type**: Only **Standard, Premium, and Ultimate ** ArkClaw instances support this feature.<br><br>* **Version requirements**: This feature is only available for ArkClaw instances running version **`1.3.6`** ** or later**. You can check your ArkClaw version and perform upgrades on the "Status and usage" tab of the ArkClaw details page. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_status_and_usage) |
|Collaboration mode usage constraints |After you enable ** collaboration mode**, the Hermes capability is automatically disabled. The Hermes capability is not supported in collaboration mode. |
|Agent template usage constraints |Agent templates marked with the **Featured** label are featured templates. These templates incorporate prompts, workflows, dedicated Skills, and other components that have been refined by the platform over time. As core digital assets of the platform, they are available for direct use only. Viewing detailed configurations and making edits or modifications are not supported. |


<span id="EqbojuPt"></span>
## Prerequisites


* The agent team has been created and includes at least **2 sub\-agents**. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Adding_agents_and_managing_my_agents?lang=en)

* If the team has a [custom agent](https://docs.byteplus.com/en/docs/ArkClaw/Adding_agents_and_managing_my_agents?lang=en#ijV7GfgB), manually enable the `Agent Workflow Status`, `Update Agent Workflow`, and `exec` tools for the agent. For configuration details, refer to [Configuring tools for my agents](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_tools_for_my_agents?lang=en).


<span id="QXx3bISD"></span>
## Enable/disable agent team collaboration mode


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page, and select "Agent Center" in the left\-side navigation pane.

3. On the "My agents" page, click the "Edit" or "View details" button on the primary agent card.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent with the agent ID <strong>main</strong> is the <strong>primary agent</strong>.   </div>
   

4. Enable or disable agent team collaboration mode as needed.

   * Enable: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5869d3ec8479cc9febe3f8ed0956f0e.png) </span> icon to enable agent team collaboration mode.

   * Disable: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c199d7a6a52f26f11191723206a41ae2.png) </span> icon to disable agent team collaboration mode.


<span id="wTgb5ZAD"></span>
## Use collaboration mode

After the **agent team collaboration mode is enabled**, you can start a team workflow through **automatic ** or **manual ** triggering. The following describes the procedures for each method:


<Tabs>
<Tab zoneid="jK6KeC7ko1" title="Triggered automatically">
<TabTitle>Triggered automatically</TabTitle>

1. In the chat input box, enter a natural language task command or select content suitable for the current scenario from the platform preset prompts. After confirming that the command is correct, send it.

2. (Optional) Follow the on\-screen instructions to provide supplementary information.

3. When a workflow planning\-related prompt appears, click "Start in team mode" to initiate an agent team collaboration task. The primary agent coordinates sub\-agents to collaborate through a division of labor, automatically handling task decomposition, handoff, and end\-to\-end processing.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Start in single\-agent mode</strong>: Tasks are handled independently by the primary agent, and only the primary agent is used for executing tasks. Alternatively, tasks are handled in the original way, where the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring_md_files__?lang=en">Agent.md</a> and <a href="https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Enterprise_memory_management__?lang=en">memory management</a> configurations of the primary agent determine whether the primary agent or a sub\-agent handles a task.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Cancel task</strong>: Cancel the task, do not start any execution mode, and end the current task flow directly.   </div>
   

   4. (Optional) After the task starts, you can also click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d62ca4a51c6bfc9cd68b46f3aa4c57d4.png) </span> icon at any time to view its progress, generated outputs, and uploaded files in the current orchestration stage on the right. For more details, refer to [Viewing and managing task outputs](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_managing_task_outputs?lang=en).


</Tab>
<Tab zoneid="rFNNclm8NU" title="Triggered manually">
<TabTitle>Triggered manually</TabTitle>

1. In the ArkClaw chat box, click the "+" button, and then click the "Enable" button next to **Collaboration mode** to enter collaboration mode.

2. (Optional) If agents have not yet been recruited, the system prompts you to recruit first. You can click "Go to recruit" to go to the Agent Gallery page to recruit Agents. At least 2 agents are required. After configuration, switch to the primary agent in the dialog box and enable collaboration mode.

3. In the chat input box, enter a natural\-language task command or select a preset prompt provided by the platform that matches the current scenario. Then select the sub\-agents for collaboration. After you confirm that the configuration is correct, send the command.

4. (Optional) Follow the on\-screen instructions to provide supplementary information.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the sub\-agents in the current ArkClaw do not meet the requirements for a collaboration workflow, the collaboration mode cannot be initiated.   </div>
   

5. When a workflow planning\-related prompt appears, click "Start in team mode" to initiate an agent team collaboration task. The primary agent coordinates sub\-agents to collaborate through a division of labor, automatically handling task decomposition, handoff, and end\-to\-end processing.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Start in single\-agent mode</strong>: Tasks are handled independently by the primary agent, and only the primary agent is used for executing tasks. Alternatively, tasks are handled in the original way, where the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring_md_files__?lang=en">Agent.md</a> and <a href="https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Enterprise_memory_management__?lang=en">memory management</a> configurations of the primary agent determine whether the primary agent or a sub\-agent handles a task.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Cancel task</strong>: Cancel the task, do not start any execution mode, and end the current task flow directly.   </div>
   

   6. (Optional) After the task starts, you can also click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d62ca4a51c6bfc9cd68b46f3aa4c57d4.png) </span> icon at any time to view its progress, generated outputs, and uploaded files in the current orchestration stage on the right. For more details, refer to [Viewing and managing task outputs](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_managing_task_outputs?lang=en).


</Tab>
</Tabs>


<span id="kpNeolOZ"></span>
## View agent execution traces

Agent execution traces display the execution process of sub\-agents in the current task. Through the execution trace, you can see how the primary agent dispatches tasks, what state each sub\-agent is currently in, which stages have been completed, and what results were returned.

During task execution, click the avatar of the target agent in the task panel on the right to view agent execution details.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The <strong>Task progress</strong> panel on the right only shows agents that are actually involved in the current task. It does not inherit sub\-agents from the previous task or from the entire session. When no sub\-agent is invoked in the current task, no sub\-agent avatars are displayed.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Once the entire agent workflow has finished and all sub\-agent results have been aggregated, the "Task progress" panel is automatically hidden, and the page displays only the final output.</div>



<span id="7Uw7AQgx"></span>
## FAQ


* **Why do I receive an error message indicating sub\-agents do not support the current team task after enabling the team collaboration mode?** 

   Possible causes and solutions:

   * **Missing workflow tool permissions required for sub\-agents**

      You need to grant the following tool permissions to sub\-agents: `Agent Workflow Status`, `Update Agent Workflow`, and `exec`. For instructions, refer to [Configuring tools for my agents](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_tools_for_my_agents?lang=en).

   * **Agent team workflow orchestration cache**

      Go to the configuration page of the primary agent (ID: main), disable the team collaboration mode switch, and then enable it again to refresh the status. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_agent_team_collaboration_mode?lang=en)

* **Why can't I find the team collaboration mode switch?** 

   This feature has both specification and version limits. If the requirements are not met, the switch entry is hidden.

   * **Instance type**: Only Standard, Premium, and Ultimate ArkClaw instances support this feature.

   * **Version requirements**: This feature is only available for ArkClaw instances running version `1.3.6` ** or later**. You can check your current ArkClaw version and perform upgrades on the "Status and usage" tab of the ArkClaw details page. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_status_and_usage)

* **Can I use agent team collaboration mode over IM channels?** 

   Yes, you can. After enabling [agent team collaboration mode](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_agent_team_collaboration_mode?lang=en), you can initiate collaboration mode tasks when you chat with the primary agent (ID: main) through an IM channel.
