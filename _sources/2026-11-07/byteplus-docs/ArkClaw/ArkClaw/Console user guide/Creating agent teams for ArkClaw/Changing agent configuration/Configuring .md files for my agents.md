---
title: "Configuring .md files for my agents"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_md_files_for_my_agents_0"
---

By configuring Markdown (.md) files, you can define independent codes of conduct, workflow, profile, and user profile for each agent in ArkClaw and your team. This transforms every ArkClaw agent into a customized intelligent assistant with a distinct identity, strict operational boundaries, structured processes, and a deep understanding of its users.

<span id="Ldwn5YcS"></span>
## Descriptions of Markdown file configurations and usage scenarios

<span id="ApXLvmXn"></span>
### Code of conduct (SOUL.md)

This file defines the baseline rules, security constraints, and core values that the agent must strictly follow. It covers value principles, prohibited actions, decision\-making logic, and communication guidelines. Its purpose is to explicitly state what the agent must not do, as well as the criteria for judgment and trade\-offs when encountering conflicts.

ArkClaw provides a default set of **general code of conduct** for each agent, which covers most business scenarios. ** We recommend keeping the default configuration**. If the default content does not meet your business needs, you can adjust it as required.

<span id="Njj1RMYt"></span>
### Workflow (AGENTS.md)

This file defines the agent's **business processes, collaboration standards, and task orchestration logic**, including session start/stop conditions, task breakdown, delivery requirements, and collaboration agreements. The file defines how agents perform tasks and clarifies rules for ** starting, processing, and concluding** individual sessions and tasks. You can choose whether to configure this based on your actual business needs.


* **Configuration not required**: Lightweight Q&A agents, such as FAQ assistants or terminology translation tools, do not require a workflow.

* **Configuration required:**  When the agent needs to handle multi\-step processes, clear sequences, or task decomposition scenarios, you can set up a workflow to ensure orderly and traceable execution. For example, a ticket assistant can operate following a 6\-step workflow: "**Receive ticket → Categorize → Assign → Track → Resolve → Satisfaction survey**". This enables standardized management of the entire ticket lifecycle.


<span id="EcfSQsxg"></span>
### Agent profile (IDENTITY.md)

This file defines the core identity and soul of the agent, including its name, personality, and identity definition. It is used to clearly define "who I am" and maintain a consistent communication style and role identity. ArkClaw provides a preconfigured agent profile for each agent, covering most business scenarios. We recommend keeping the default configuration. If the default content does not meet your business needs, you can adjust it as required.

<span id="0HY5SdfI"></span>
### User profile (USER.md)

This file records basic user information and communication preferences, such as preferred forms of address, interaction habits, context memory, and privacy boundaries (for example, explicitly setting rules like "Do not discuss salary or politics in work contexts", which prompts the agent to proactively avoid these topics). This allows the agent to adapt to personalized needs and provide customized services in a more tailored manner.


* **Configuration not required**: You do not need to configure a user profile if the agent serves a general audience and does not require personalization or long\-term interaction, for example, disposable or short\-term agents such as event Q&A bots, temporary launch\-event assistants, or time\-limited support helpers.

* **Configuration required**: When personalized interaction or custom usage preferences are needed, configure a user profile to allow the agent to precisely adapt to your communication style, usage habits, and specific rules.


<span id="P67kUoQT"></span>
## Procedure

<span id="OK4JSsjy"></span>
### Step 1: Enter the Markdown configuration page


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page.

3. In the left\-side navigation pane, click "Agent Center".

4. Click the "My agents" tab.

5. Select the target agent and click the "View details" button.


<span id="wRZRFqRQ"></span>
### Step 2: **Configure agent Markdown files**

By configuring a set of standardized Markdown (.md) files, you can define the agent's code of conduct, workflow, profile, and user profile. This enables fine\-grained management of the agent without writing code.


1. In the MD configuration section, click the  **"Code of conduct"/"Workflow"/"Agent profile"/"User profile"**  tab to switch to the corresponding configuration page.

2. Click the text editing area and edit the content directly.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can write the content using your preferred format, such as plain text, bulleted lists, tables, or Markdown. The agent will parse it correctly.   </div>
   

3. After you complete editing, click the "Save" button to complete the operation.

5. (Optional) If you need to discard your current modifications, click the "Cancel" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After canceling, unsaved content will be lost and cannot be recovered.   </div>
