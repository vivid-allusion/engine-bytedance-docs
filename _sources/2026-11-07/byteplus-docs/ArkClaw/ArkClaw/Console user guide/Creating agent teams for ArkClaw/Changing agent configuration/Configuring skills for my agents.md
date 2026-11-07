---
title: "Configuring skills for my agents"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_skills_for_my_agents_0"
---

Skills are scenario\-based business capability packages for ArkClaw agents. They consist of instruction sets, knowledge bases, business workflows, and Q&A rules, and can be directly reused as complete business capability modules.

You can configure **primary agent skills** and **independent skills for the other agents**. Skills for the primary agent are global default skills and are inherited by all the other agents by default. After **building an agent team ** for your ArkClaw, you can add independent skills or enable/disable preset skills for **each agent ** (the primary agent or the other agents). This enables each agent to possess only the capabilities relevant to its role.


* **Enable a skill**

   Once a skill is enabled, the agent can automatically identify and match the business scenarios covered by this skill during conversations. It then invokes the built\-in skill instructions, knowledge bases, and business workflows to respond to and process tasks.

* **Disable a skill**

   After a skill is disabled, the agent no longer loads or matches this skill during conversations. Q&A for the corresponding business scenarios will be handled by general ArkClaw capabilities as a fallback, instead of invoking the specialized capabilities encapsulated in the skill.

   > * Enabling or disabling a skill takes effect only for **new conversations**. Historical conversations are not affected.

   > * Disabling a skill does not delete the skill itself. It can be re\-enabled at any time.

   <span id="NT7bnKTa"></span>
   ## Operation instructions

   If the other agents have independently configured skills, those skills take precedence when the target agent handles tasks, and the global skills of the primary agent do not apply to that agent. If no independent skill configuration is set, the agent automatically inherits and uses the skills of the primary agent.

<span id="aKIIR5jZ"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Go to the target ArkClaw page.

3. In the left\-side navigation pane, click "Agent  Center".

4. Click the "My agents" tab.

5. Select the target agent and click the "View details" button.


In the "Skills" module, perform the following operations:


   * **Add a skill**

      1. Click "Add".

      2. In the pop\-up window, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a0064985c8e364acea59c02f11022a3c.png) </span> icon of the target skill to add it.

   * **Delete a skill**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Only custom\-added skills can be deleted. System preset skills cannot be deleted.      </div>
      

      1. Click the "Edit all" button.

      2. In the pop\-up window, choose to delete skills individually or in batches:

         * Delete individually: On the right side of the target skill, click the "Delete" button. Confirm that the skill to be deleted is correct. Then, click "Delete" to complete the operation.

         * Delete in batches: Select multiple skills to be deleted, and click the "Batch delete" button. Confirm that the selected skills are correct, and click the "Delete" button to complete the operation.
