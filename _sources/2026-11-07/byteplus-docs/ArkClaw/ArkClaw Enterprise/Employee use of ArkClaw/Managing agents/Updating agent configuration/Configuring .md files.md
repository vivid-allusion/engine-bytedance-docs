---
title: "Configuring .md files"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_md_files__"
---

By configuring Markdown (.md) files, you can define independent codes of conduct, workflow, profile, and user profile for ArkClaw and "My agents". This transforms every ArkClaw agent into a customized intelligent assistant with a distinct identity, strict operational boundaries, structured processes, and a deep understanding of its users.

<span id="C7zB1mEs"></span>
## Descriptions of Markdown file configurations and usage scenarios

<span id="4KurpnsU"></span>
### Code of conduct (SOUL.md)

This file defines the baseline rules, security constraints, and core values that the agent must strictly follow. It covers value principles, prohibited actions, decision\-making logic, and communication guidelines. Its purpose is to explicitly state what the agent must not do, as well as the criteria for judgment and trade\-offs when encountering conflicts.

ArkClaw provides a default set of **general code of conduct** for each agent, which covers most business scenarios. **We recommend keeping the default configuration**. If the default content does not meet your business needs, you can adjust it as required.

<span id="3CJVG08z"></span>
### Workflow (AGENTS.md)

This file defines the agent's **business processes, collaboration standards, and task orchestration logic**, including session start/stop conditions, task breakdown, delivery requirements, and collaboration agreements. The file defines how agents perform tasks and clarifies rules for ** starting, processing, and concluding** individual sessions and tasks. You can choose whether to configure this based on your actual business needs.


* **Configuration not required**: Lightweight Q&A agents, such as FAQ assistants or terminology translation tools, do not require a workflow.

* **Configuration required:**  When the agent needs to handle multi\-step processes, clear sequences, or task decomposition scenarios, you can set up a workflow to ensure orderly and traceable execution. For example, a ticket assistant can operate following a 6\-step workflow: "**Receive ticket → Categorize → Assign → Track → Resolve → Satisfaction survey**". This enables standardized management of the entire ticket lifecycle.


<span id="HKq3LdLm"></span>
### Agent profile (IDENTITY.md)

This file defines the core identity and soul of the agent, including its name, personality, and identity definition. It is used to clearly define "who I am" and maintain a consistent communication style and role identity. ArkClaw provides a preconfigured agent profile for each agent, covering most business scenarios. We recommend keeping the default configuration. If the default content does not meet your business needs, you can adjust it as required.

<span id="oWQ0U59O"></span>
### User profile (USER.md)

This file records basic user information and communication preferences, such as preferred forms of address, interaction habits, context memory, and privacy boundaries (for example, explicitly setting rules like "Do not discuss salary or politics in work contexts", which prompts the agent to proactively avoid these topics). This allows the agent to adapt to personalized needs and provide customized services in a more tailored manner.


* **Configuration not required**: You do not need to configure a user profile if the agent serves a general audience and does not require personalization or long\-term interaction, for example, disposable or short\-term agents such as event Q&A bots, temporary launch\-event assistants, or time\-limited support helpers.

* **Configuration required**: When personalized interaction or custom usage preferences are needed, configure a user profile to allow the agent to precisely adapt to your communication style, usage habits, and specific rules.


<span id="0dLYaiz5"></span>
## Procedure

By configuring a set of standardized Markdown (.md) files, you can define the agent's code of conduct, workflow, profile, and user profile. This enables fine\-grained management of the agent without writing code.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw, and select "Agent Center" in the left\-side navigation pane.

3. On the "My agents" page, click "View details" on the target agent card.

4. In the MD configuration section, click the  **"Code of conduct"/"Workflow"/"Agent profile"/"User profile"**  tab to switch to the corresponding configuration page.

5. Hover over the text area and click to modify the content.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can write in any format you prefer, such as plain text, bulleted lists, tables, or Markdown. The agent will parse it correctly.   </div>
   

6. Save the changes.

   * Primary agent (the agent whose agent ID is "main"): After editing, click the "Save" button to make the new settings take effect.

   * Sub\-agent (added from Agent Gallery or custom sub\-agents): After editing, click the "Update" button in the upper\-right corner of the page to make the new settings take effect.
