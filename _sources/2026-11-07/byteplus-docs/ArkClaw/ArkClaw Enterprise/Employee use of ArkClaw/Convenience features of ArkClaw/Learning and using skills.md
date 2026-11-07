---
title: "Learning and using skills"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Learning_and_using_skills_"
---

ArkClaw includes some commonly used built\-in skills that can be automatically matched and called based on task requirements. In addition, ArkClaw supports integrating community plugins from channels such as ClawHub, allowing you to extend ArkClaw with new skills as needed across a wide range of domains, such as programming, browser operations, office work, and expert roles.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Skills are essentially capability units with encapsulated logic for executing specific tasks (for example, your Python language capability, addition operations, English language, or other skills). When performing tasks, ArkClaw automatically selects the appropriate skills from its skill list to complete operations (for example, during programming, you might select skills such as Python or English).</div>


<span id="uQNknUt0"></span>
## View the existing skills of an agent

You can view the currently available skills, including preset skills and skills you have added.


1. Open the browser, enter the ArkClaw login URL in the address bar, and then press Enter.

2. Switch to the target Claw.

3. You can view all added skills by using the following methods.

   
   <Tabs>
   <Tab zoneid="yRlQkNZIUn" title="View via shortcut">
   <TabTitle>View via shortcut</TabTitle>
   
   Enter the / symbol in the task initiation chat box and select the "Skills" tab in the pop\-up window to check information of all added skills.
   
   
   </Tab>
   <Tab zoneid="dLY267DXj4" title="View in the "Add skill" module">
   <TabTitle>View in the "Add skill" module</TabTitle>
   
   At the bottom of the task input box, click "+ \> Add skill" to view all currently added skills.
   
   
   </Tab>
   </Tabs>
   


<span id="md7LpPtZ"></span>
## Use skills from the SkillHub

If the existing skills do not meet your business requirements, the "SkillHub" on the "Skill Center" page provides a variety of skills that you can try out or add to your agent.

The skills view in the SkillHub is divided into two categories:


|Category |Content |
|---|---|
|Visibility scope |All skills, enterprise\-uploaded skills, public skills, and personal\-uploaded skills.<br><br><br>* Enterprise\-uploaded skills: Skills uploaded by administrators in the ArkClaw Enterprise console. After an administrator configures permissions, they become visible to employees with the corresponding permissions.<br><br>* Personal\-uploaded skills: Skills uploaded by employees in the ArkClaw Enterprise employee\-side console. They are visible only to the uploaders and administrators. After an administrator configures permissions, they become visible to employees with the corresponding permissions.<br><br>* Public skills: Native ArkClaw skills, visible to all users. |
|Applicable scenarios |All scenarios, BytePlus recommendations, enterprise picks, design, multimedia, document processing, and more. |


<span id="Mod4Gd1k"></span>
### Try out a skill


* If you are not sure whether to add a skill, click "Try" on the skill card to open a chat box and try it out.

* If you want to add a skill to a specific agent, click "Add to more agents" and select the target agent.


<span id="0CR7IjVz"></span>
### Add skills to agents

In any skill view, you can add skills to specified agents in ArkClaw, either individually or in batches (if there are multiple skills). Specific steps are as follows:


<Tabs>
<Tab zoneid="xQ9xW89P" title="Add a skill to multiple agents">
<TabTitle>Add a skill to multiple agents</TabTitle>

This is suitable for scenarios where you have an employee ArkClaw instance, have created multiple agents, and want to batch\-add a single skill to those agents.


1. Open the browser, enter the ArkClaw login URL in the address bar, and then press Enter.

2. Switch to the target Claw, and select "Skill Center" in the left directory tree.

3. On the "SkillHub" page, find the skill to add to the agents, and click "+ Add" on the skill card.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If a pop\-up window appears with the message "You can add skills after upgrading the plugin", it means your ArkClaw skill plugin is outdated. Click "Upgrade now" as prompted, and add the skill after the upgrade completes.   </div>
   

4. In the pop\-up window, select the agents in the current ArkClaw to which you want to add the skill, and click the "Add" button to complete the operation.


</Tab>
<Tab zoneid="KdQGLQhCAL" title="Add multiple skills to multiple agents">
<TabTitle>Add multiple skills to multiple agents</TabTitle>

This is suitable for scenarios where you have an employee ArkClaw instance, have created multiple agents, and want to batch\-add multiple skills to those agents.


1. Open the browser, enter the ArkClaw login URL in the address bar, and then press Enter.

2. Switch to the target Claw, and select "Skill Center" in the left directory tree.

3. On the target skill view tab, click "Batch add" at the bottom, select the cards of new skills that you want ArkClaw to learn, and click "Add to agent".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your ArkClaw skill plugin version is outdated, click "Upgrade now" as prompted, and add the skills after the plugin is upgraded.   </div>
   

4. In the pop\-up window, select the agents in the current ArkClaw to which you want to add the skills, and click the "Add" button to complete the operation.


</Tab>
</Tabs>


<span id="aTmPqzR7"></span>
## Create or upload skills

If the existing skills do not meet your business requirements, you can create custom skills or upload your own skills.


* If you **do not have** a skill package to upload, you can create and upload a skill by clicking "Create with agent".

* If you **already have** a skill package to upload, you can upload the skill through "Agent Center".



<Tabs>
<Tab zoneid="H0muwEL1gN" title="Create skills with an agent">
<TabTitle>Create skills with an agent</TabTitle>

You can create a skill with an agent on the "Skill Center" tab by entering natural language and then upload the skill to the SkillHub. To manage skills for an agent, see [Configuring skills for my agent](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_skills_for_my_agents).


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target Claw, and click "Skill Center" in the left navigation tree.

3. In the upper\-right corner of the page, select "Create skill \> Create with agent" to open the skill creation task dialog box.

4. In the chat box, enter the description of the skill to create and wait for the system to create the skill.

   **Examples:** 

   > **Task objective**

   > Create a document review skill.

   > **Execution requirements**

   > * Execute the task only based on the draft content provided by the user. Do not add any unspecified skill attributes, feature details, or technical implementations.

   > * Ensure that the generated skill definition is complete but not over\-expanded, and retain "document review" as the core purpose.

   > **Output requirements**

   > Output the complete definition or configuration structure of the document review skill. Any clear, executable format is acceptable.   
   

5. After the skill is created, you can perform the following operations.

   * **View files**

      Click "View file" to quickly view the related definitions and file content of the skill, so that you can understand the capability boundaries and applicable scenarios of the skill.

   * **Save**

        If you do not need to add the skill to an agent or publish it to the SkillHub at the current stage, you can click "Save" to persist the current editing progress. The saved version will be retained in the "Created by me" list and can be added to an agent or published later, as needed.

   * **Add to an agent**

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If a skill with the same name already exists in the target skills space, the existing skill version will be directly overwritten by the submitted content during registration. After the overwrite, the original capability configuration will be replaced and cannot be automatically rolled back. Confirm that the name is correct, or back up important versions in advance to avoid exceptions in business capabilities.      </div>
      

      To put the configured skill into actual use, click "Add to agent" and select the agent that needs to use the skill. The current skill is then added to the corresponding agent. After the skill is added, the system associates the current skill with the target agent. The agent can call the capabilities defined by the skill in subsequent conversations.

   * **Publish to the SkillHub**

      After the skill is published, it is visible on the "SkillHub \> Created by me" tab, and only to the uploader. The skill can also be viewed from the management console.

      * Publishing a skill does not automatically add it to an agent. To add it to your agent, select the "SkillHub \> Created by me" tab, click "+ Add" on the skill card you created, and select the specified agent. If the created skill is updated, you can click "Upload update" on the skill card, and the agent will synchronously update the skill.

      * To allow other employees to view and use the skill, an enterprise administrator can add it to the skill library and configure permissions. Authorized employees can then view it in the SkillHub.


</Tab>
<Tab zoneid="k3YXy93333" title="Upload skills via Agent Center">
<TabTitle>Upload skills via Agent Center</TabTitle>

Custom skills can be uploaded for agents on the "My agents" tab. Prepare the skill ZIP package in advance. To manage skills for an agent, see [Configuring skills for my agent](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_skills_for_my_agents).


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target Claw and select "Agent Center \> My agents".

3. Click the "View details" button on the agent card (using the primary agent whose **ID** is main as an example).

4. On the agent details page, select the "Skills" section and then click "Add \> Upload skill".

5. In the dialog box that appears, drag and drop a local `.zip` file that meets the specifications (within 25 MB) to upload and apply it.

   Installing skills that involve sensitive operations, such as reading from or writing to arbitrary files or executing system commands, is not recommended for shared Claws.

   > File specifications:

   > After decompression, the root directory must contain exactly **one folder**, and its name must exactly match the skill name in the SKILL.md file.

   > The SKILL.md file must be placed in the **root directory** of this folder and meet the following requirements:

   > * Skill name:

   >    * Required. The length cannot exceed 64 characters.

   >    * Only lowercase letters, numbers, and hyphens (\-) are supported.

   >    * XML tags or platform\-reserved fields (such as agentkit) cannot be contained.

   > * Skill description:

   >    * Required. The length cannot exceed 10,000 characters.

   >    * XML tags cannot be contained.


</Tab>
</Tabs>


<span id="3ikypEXv"></span>
## Manage skills

You can manage ArkClaw preset skills or manually added skills on the "Skill Center" and "My agents" tabs.

<span id="qhBk1JYd"></span>
### Disable or enable preset skills


<Tabs>
<Tab zoneid="pgGPCogA73" title="Manage preset skills in the Skill Center">
<TabTitle>Manage preset skills in the Skill Center</TabTitle>

1. Open the browser, enter the ArkClaw login URL in the address bar, and then press Enter.

2. Switch to the target ArkClaw page.

3. Click "Skill Center" in the left navigation tree and go to the "Added" tab.

&nbsp;

4. On the left, select the corresponding agent and click "Preset skills". In the preset skill list, you can enable or disable preset skills either individually or in batches.


</Tab>
<Tab zoneid="RugJzVYx6V" title="Manage preset skills in the Agent Center">
<TabTitle>Manage preset skills in the Agent Center</TabTitle>

1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw page and select "Agent Center \> My agents".

3. Click "View details" on the corresponding agent card.

4. On the details page of the agent, click "Edit all" in the "Skills" section.

5. In the "All skills" pop\-up window, click "Built\-in skills". In the "Actions" column of each skill, you can enable or disable individual built\-in skills, or select multiple skills and click "Batch disable" or "Batch enable".


</Tab>
</Tabs>


<span id="83qXerl5"></span>
### Delete added skills


<Tabs>
<Tab zoneid="S71q5Ued5I" title="Delete skills in the Skill Center">
<TabTitle>Delete skills in the Skill Center</TabTitle>

1. Open the browser, enter the ArkClaw login URL in the address bar, and then press Enter.

2. Switch to the target ArkClaw page.

3. Click "Skill Center" in the left navigation tree and go to the "Added" tab.

4. On the left, select the corresponding agent and click "Agent skills". In the agent skill list, you can remove skills either individually or in batches.


</Tab>
<Tab zoneid="Vp4mXyRbTl" title="Delete skills in the Agent Center">
<TabTitle>Delete skills in the Agent Center</TabTitle>

1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw page and select "Agent Center \> My agents".

3. Click "View details" on the corresponding agent card.

4. On the details page of the agent, click "Edit all" in the "Skills" section.

5. In the "All skills" pop\-up window, click "Agent skills". In the "Actions" column of each skill, you can delete individual skills, or select multiple skills and click "Batch delete".


</Tab>
</Tabs>


<span id="yU9ptIYE"></span>
### Transfer skills to other agents

You can transfer skills of the current agent to other agents within the current instance.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw page and select "Agent Center \> My agents".

3. Click "View details" on the corresponding agent card.

4. On the details page of the agent, click "Edit all" in the "Skills" section.

5. On the default "Agent skills" page in the "All skills" dialog box, select the target skill or skills, click "Batch transfer", and select the target agent.


<span id="Bmy5pCdC"></span>
### Update a skill version

You can upload an updated version of a skill to your agent. Specific steps are as follows:


<Tabs>
<Tab zoneid="XwIDnF01GI" title="Upload from "Created by me"">
<TabTitle>Upload from "Created by me"</TabTitle>

If you manually update a skill you created, you can upload the updated skill to an agent from the "Created by me" tab.


1. Open the browser, enter the ArkClaw login URL in the address bar, and then press Enter.

2. Switch to the target Claw.

3. Click "Skill Center" in the left navigation tree and go to the "Created by me" tab.

4. Find the skill to update, click "Upload update" on the card, and upload the new skill ZIP package.


</Tab>
<Tab zoneid="dBRHFjvKaL" title="Upload from "Added"">
<TabTitle>Upload from "Added"</TabTitle>

If you have not manually updated any skills, you can also check whether the current agent has other skills available for update and upload the updated skills.


1. Open the browser, enter the ArkClaw login URL in the address bar, and then press Enter.

2. Switch to the target Claw.

3. Click "Skill Center" in the left navigation tree and go to the "Added" tab.

4. If any skills are available for update, the page displays the message "X skills are available for update". Click "View update" in the message.

5. In the pop\-up window, select the skills to update, click "Update", and upload the new skill ZIP package.


</Tab>
</Tabs>


<span id="rhwNjZGE"></span>
### Discard skill version changes

After you [update a skill version](https://docs.byteplus.com/en/docs/ArkClaw/Learning_and_using_skills_#Bmy5pCdC), if you have not published the skill to the SkillHub, none of the changes in the current update have officially taken effect. You can discard the current changes as needed to restore the skill to the published version and discard all unpublished changes in this update.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Discarding changes will discard all unpublished changes in the current update, and the skill will be reverted to the published version. This operation does not affect the live version that is currently running. <strong>This operation cannot be undone. Proceed with caution</strong>.</div>



1. Select "... \> Discard change".

2. After confirming that you want to revert to the published version, click "**Discard**" to complete the operation.


<span id="pjmDLhAS"></span>
## Use skills on a shared Claw as an employee

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The shared Claw feature is currently in Beta. To use this feature, contact your account manager.</div>


Shared Claws are managed centrally from the enterprise management console. Employee permissions when using a shared Claw differ from those when using a personal Claw.


* Employees can use the skills configured on a shared Claw to complete tasks as usual. They can also enter "/" in the chat box to view the list of currently available skills. To adjust skill configurations, contact an enterprise administrator.

* Employees cannot perform operations that require administrative permissions, such as adding skills, enabling or disabling preset skills, creating or uploading skills, or deleting existing skills from a shared Claw.
