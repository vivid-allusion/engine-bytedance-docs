---
title: "Configuring skills for my agents"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_skills_for_my_agents"
---

After adding sub\-agents from Agent Gallery or custom sub\-agents to ArkClaw, you can add skills to each sub\-agent or enable/disable preset skills. This enables each sub\-agent to retain only the capabilities that match its responsibilities.

<span id="BpTimF7x"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page, and select "Agent Center" in the left\-side navigation pane.

3. On the My agents page, click "View details" on the target agent card.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent whose Agent ID is <strong>main</strong> is the <strong>primary agent</strong>.   </div>
   

4. In the "Skills" module, perform the following operations:

   
   <Tabs>
   <Tab zoneid="A2pzn7DiuK" title="Add/delete agent skills">
   <TabTitle>Add/delete agent skills</TabTitle>
   
   * **Add a skill**
   
      Click the "+ Add" button and add skills in the following ways:
   
      * Intelligent creation: In the dialog box that appears, describe the required skill (for example, "Help me create a capability for searching North American media news across the entire web"). Then, click the "Create" button. The system will automatically draft, verify, and associate the skill with the agent.
   
      * Add from SkillHub: In the dialog box that appears, use the category tabs at the top (such as Data analysis or IT O&M) or the search box to find and add an existing mature skill.
   
      * Upload a skill: In the dialog box that appears, drag and drop a local `.zip `file that meets the specifications (within 10 MB) to upload and apply it.
   
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
         
   
         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the name of the uploaded skill compressed package (.zip) is exactly the same as an existing skill name in the current skill list, the system will perform overwriting by default. The newly uploaded content will directly replace the original skill data. Confirm whether you need to keep the old configurations before you perform the operation.      </div>
         
   
         > File specifications:
   
         > After decompression, the root directory must contain exactly **one folder**, and its name must exactly match the skill name in the SKILL.md file.
   
         > The SKILL.md file must be placed in the **root directory** of this folder and meet the following requirements:
   
         > Skill name:
   
         > * Required. The length cannot exceed 64 characters.
   
         > * Only lowercase letters, numbers, and hyphens (\-) are supported.
   
         > * XML tags or platform\-reserved fields (such as agentkit) cannot be contained.
   
         > Skill description:
   
         > * Required. The length cannot exceed 10,000 characters.
   
         > * XML tags cannot be contained.
   
   * **Delete a skill**
   
      1. Click the "Edit all" button.
   
      2. In the pop\-up window, click the "Agent skills" button and choose to delete skills individually or in batches.
   
         * Delete individually: On the right side of the target skill, click the "Delete" button. Confirm that the skill to be deleted is correct. Then, click "Delete" to complete the operation.
   
         * Delete in batches: Select multiple skills to be deleted, and click the "Batch delete" button. Confirm that the selected skills are correct, and click the "Delete" button to complete the operation.
   
   
   </Tab>
   <Tab zoneid="fIX5D56f0e" title="Enable/disable built-in skills">
   <TabTitle>Enable/disable built-in skills</TabTitle>
   
   1. Click the "Edit all" button.
   
   2. In the pop\-up window, click the "Built\-in skills" button to enable or disable preset skills.
   
      * **Enable a skill:**  On the right side of the target skill, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80263f2034bf5eb1084acf51c94570d1.png) </span> to enable the skill. Once a skill is enabled, the agent can automatically identify and match the business scenarios covered by this skill during conversations. It then invokes the built\-in skill instructions, knowledge bases, and business workflows to respond to and process tasks.
   
      * **Disable a skill:**  On the right side of the target skill, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c4cedcd29808406ea914facb69ebf63.png) </span> to disable the skill. After a skill is disabled, the agent no longer loads or matches this skill during conversations. Q&A for the corresponding business scenarios will be handled by general ArkClaw capabilities as a fallback, instead of invoking the specialized capabilities encapsulated in the skill.
   
      >    * Enabling or disabling a skill takes effect only for **new conversations**. Historical conversations are not affected.
   
      >    * Disabling a skill does not delete the skill itself. It can be re\-enabled at any time.
   
   
   </Tab>
   </Tabs>
   

5. After the configuration, click the "Update" button for the configuration to take effect.
