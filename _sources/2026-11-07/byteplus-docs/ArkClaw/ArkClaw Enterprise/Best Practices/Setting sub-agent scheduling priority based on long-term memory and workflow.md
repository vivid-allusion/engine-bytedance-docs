---
title: "Setting sub-agent scheduling priority based on long-term memory and workflow"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Best_practices_for_multi-agent_scheduling"
---

This topic describes how to configure long\-term memory (LTM) and a workflow for the ArkClaw intelligent assistant (the primary agent). This enables it to reliably identify which tasks should be prioritized for processing by sub\-agents when orchestrating multi\-agent team tasks, and automatically distribute such tasks in accordance with the rules you predefined.

<span id="dbN3k4Xk"></span>
## Scenarios

This practice applies to scenarios where multiple agents collaborate to complete complex tasks. Typical scenarios are as follows:


* **Team collaboration scenarios with fixed task allocation**

   The one\-task\-per\-role model is adopted, where dedicated sub\-agents independently handle product analysis, competitor research, data sorting, page generation, and other tasks.

* **High\-frequency standardized task scenarios**

   Repetitive business workflows can be standardized. For example, a market research task involves a complete sequential workflow covering information collection, conclusion collation and page output, which can be taken on and handled separately by multiple agents.

* **Scenarios requiring context\-specific professional capabilities**

   For specialized tasks such as coding, document drafting, data analysis, and design tasks, you may assign dedicated professional sub\-agents to take priority in handling them to ensure professional outputs.

* **Scenarios requiring high efficiency in completing parallel tasks**

   Complex tasks can be broken down into multiple independent sub\-tasks that run concurrently, significantly reducing total processing time and boosting task efficiency.


<span id="c5vuwqqU"></span>
## Step 1: Configure LTM

Save team task scheduling principles as LTM to the memory. The ArkClaw intelligent assistant (the primary agent) can access this memory information in subsequent sessions and assist with task scheduling based on the configured scheduling principles. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Enterprise_memory_management__?lang=en).


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page. In the upper\-right corner of the page, click the details icon.

3. Click the "Memory management" tab.

4. After selecting "ArkClaw intelligent assistant", click the "Add memory" button.

5. In the "Memory content" text box, enter the following content, and click "Confirm" to add LTM for the ArkClaw intelligent assistant (the primary agent).

   > Prior to execution, all tasks must strictly follow the team task scheduling principles and first be evaluated to determine whether professional team members need to be scheduled. Tasks that meet the scheduling conditions must be split and dispatched before proceeding, and the primary agent must not handle tasks that should be scheduled.   
   

<span id="fnCgMP0J"></span>
## Step 2: Adjust the workflow

Configure baseline standards, security constraints, and core values that the ArkClaw intelligent assistant (the primary agent) must follow in the team task scheduling, establishing a unified execution standard that the assistant must adhere to when automatically assigning tasks.


1. In the left\-side navigation pane, click "Agent Center".

2. Click the "My agents" tab.

3. Select the "ArkClaw intelligent assistant" card and click the "View details" button.

4. Switch to the "Workflow" tab, and perform operations in two scenarios based on whether the specified comment markers exist in the `AGENTS.md` file:

   * If the page already contains the `<!-- arkclaw-agent--team-mode-start -->` and `<!-- arkclaw-agent-team-mode-end -->` comment markers and their content: Copy the configuration content below and paste it between the two sets of comment markers to replace the original content in that section.

   * If the `<!-- arkclaw-agent--team-mode-start -->` and `<!-- arkclaw-agent--team-mode-end -->` comment markers and their content are not found on the page: Copy and paste the configuration content below into the `AGENTS.md` file.

   ```Markdown
   <!-- arkclaw-agent--team-mode-start -->
   ## Team Mode
   
   Your role is main agent. You have full working capabilities, and are also responsible for evaluating whether each task should be delegated to a more suitable specialist on the team. Don't default to handling things yourself — first assess whether a team member is a better fit.
   
   ### Team Workspace
   
   Team files are located a `~/.openclaw/.arkclaw-team/`：
   
   - `TEAM.md` — Team description, including mission, goals, member list, and task routing reference. This file must be read first; no scheduling decisions or self-execution is allowed until it has been read.
   
   ### Task Scheduling Decisions
   
   1.Read TEAM.md — Check the "Task Routing Reference" and "Members" sections to confirm which specialists are available.
   Enforce match-based routing — Whenever a task type or keyword matches an existing member's area of expertise, it must be routed to that member. It is prohibited to handle it yourself on the grounds that "I can already do this."
   2.Fallback execution — Only when no matching member exists may the main agent handle the task directly, and must explicitly state: "No matching specialist available; handled by main agent as fallback."
   3.Retroactive reporting required — If you have already completed an analysis without routing, you must inform the user which member the task actually matched (e.g., "This task actually matches the expertise of xxx"), and ask whether they'd like it handed off to the specialist for secondary processing.
   
   ### Task Scheduling Principles
   
   The following rules must be followed before scheduling:
   
   1. Read config before acting — Upon receiving any new task, the first step must always be to read TEAM.md and confirm which specialists are available. Do not self-execute or skip the scheduling process before reading it.
   2. Route first, fall back last — If there is a clear matching member, assign the task directly; only handle it yourself if there is no match or if splitting is not appropriate.
   3. Show task list before assigning — Before routing, you must present the user with a list of tasks to be dispatched, in the following format:
   
      • Data Collection Agent: Gather publicly available information on the target AI tool (pricing, version, feature descriptions) and compile a baseline dataset.
      • Capability Analysis Agent: Extract core capabilities and differentiators, generate comparison dimensions and recommendation conclusions.
      • Page Generation Agent: Render the data and content as a single-file HTML page with interactive charts, ready to share.
   4. Tasks must be self-contained — Assigned members have no access to your conversation history with the user. The task description must include:
      - What to do (the specific task)
      - What the background is (context / dependencies)
      - What the output requirements are (deliverable format and standards)
   5. Parallelize when possible — Spawn multiple independent tasks simultaneously; do not wait on them serially.
   6. Synthesize before replying — After receiving all members' results, integrate them into a complete, ready-to-use response for the user — do not simply concatenate outputs.
   7. Explain when not routing — Whenever you decide to handle something yourself without routing, briefly explain why (e.g., no matching member, task granularity not suitable for splitting, or routing overhead exceeds self-completion cost).
   <!-- arkclaw-agent-team-mode-end -->
   ```
   

5. Click the "Save" button. Then, click the "Confirm" button to complete the configuration.


<span id="zNvTnwEl"></span>
## Step 3: Automatically allocate tasks to each sub\-agent

Enter task instructions in the chat box of the ArkClaw intelligent assistant (the primary agent). The system will automatically parse task requirements and accurately assign the split subtasks to the most suitable sub\-agents for concurrent processing. This improves task efficiency and result accuracy.


1. On the "My agents" page, select the "ArkClaw intelligent assistant" card and click the "Initiate task" button.

2. Enter content in natural language in the chat box to initiate a conversation. Based on the business workflow and actual scenarios, the Agent will automatically identify a suitable sub\-agent within the team, distribute the task to the best\-matched sub\-agent for processing, and return the execution results.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Agent scheduling relies on a model to identify the task requirements and the capabilities of each sub\-agent so as to assign tasks. If no suitable sub\-agent is found, the ArkClaw assistant (the primary agent) will undertake and handle the task. Currently, the following situations are normal in multi\-agent scheduling.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>The desired agent is not found</strong>: The system cannot determine the target agent. This may be caused by missing capability requirements, recognizable invocation intent, or other necessary information in the task instructions.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>The target agent is identified but scheduling fails</strong>: The target agent fails to undertake the task. This may be because the target agent is currently unavailable, its capabilities do not match, the scheduling requirements are not met, or there is an exception in the execution chain.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Tasks are ultimately handled by the ArkClaw intelligent assistant (the primary agent)</strong>: No matching agent is found, so the ArkClaw intelligent assistant undertakes the task to avoid interruptions.   </div>
   

3. (Optional) To specify a sub\-agent to execute the task, or if the sub\-agent automatically allocated by the primary agent does not meet your requirements, you can adjust in the following two ways:

   * Precisely specify the executor via "@the target agent".

      **Sample prompt:**  @Product expert agent is prioritized for handling this task.

   * Add your requirement of "execution by a sub\-agent is prioritized" in the task description.

      **Sample prompt:**  Do not have ArkClaw intelligent assistant (the primary agent) handle this task directly. Assign this task preferentially to a sub\-agent with expertise in this domain.
