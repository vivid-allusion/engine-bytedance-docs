---
title: "Using collaboration mode"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Using_collaboration_mode_"
---

ArkClaw collaboration mode is designed to break through the limitations of the single\-agent mode in handling complex, cross\-field tasks. With this mode, you can quickly build a temporary collaborative team composed of AI agents with expertise in different fields within an ArkClaw instance, enabling them to communicate and jointly complete comprehensive projects.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The collaboration mode is an experimental feature currently <strong>in Beta. </strong>Your participation and experience are welcome. If you experience any problems, exceptions or have any suggestions during use, submit feedback by clicking "Settings \> Feedback".</div>


* <div data-tips="true" data-tips-type="warning">The workflow in collaboration mode is planned and controlled by the large model and consumes a large number of tokens. If the model produces hallucinations during project execution and the project cannot proceed as expected, you may suspend or delete the project.</div>



<span id="r59OYigW"></span>
## **Core features**


* **Multi\-role collaboration**: Collaborative members perform respective duties and collaborate efficiently under the unified scheduling of the **project manager agent** to complete complex tasks and deliver final outputs.

* **Independent workspace**: Each member agent in the collaborative team has an independent session and workspace. This ensures that tasks in different fields are processed in parallel without interference.

* **Unified lifecycle management**: Each member agent is deeply associated with a project. When you create a project, the platform automatically initializes all required member agents in the ArkClaw instance. When you delete the collaborative project, the associated multiple agents are securely released and deleted synchronously.


<span id="vDeCP98R"></span>
## Mode comparison


|Mode |Description |
|---|---|
|Collaboration mode |Designed specifically for complex projects. After you switch to this mode, the system guides you through the project creation process. At the same time, the session list on the left is automatically switched to the project view, allowing you to manage all collaborative projects easily. |
|Assistant mode |Maintains the original single\-point dialog mode, which is suitable for quick Q&A and executing a single task. |


<span id="UKtRiNKX"></span>
## Usage notes


* **Starter** ArkClaw instances support the creation of only 3 collaborative projects, while **Standard** and **Premium** ArkClaw instances have no such limit.

* Collaboration mode is only available for the **primary agent**, namely the ArkClaw intelligent assistant.

* Currently, collaboration mode does not support visual interface takeover and manual operations of cloud PC (CUA) and cloud browser (BUA). If a step requiring manual operations (such as login authentication or slider verification) is triggered during task execution, the task will be interrupted. We recommend that you complete operations that require login authentication in a separate session in advance, or reuse an established login state in the task.


<span id="VWUBtPWQ"></span>
## Procedure

<span id="6Zu5vjwd"></span>
### Step 1: Enter collaboration mode


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/welcome).

2. Switch to the target ArkClaw page.

3. In the ArkClaw chat box, click the "+" button, and then click the "Enable" button next to **Collaboration mode** to enter collaboration mode.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you use the collaboration mode, if the "Install plugin" dialog box pops up, click "Confirm" to install the plugin. After the installation is complete, you can access the collaboration mode chat page.   </div>
   

<span id="DwaPCMNE"></span>
### Step 2 (optional): Configure custom experts

ArkClaw provides preset experts. If they do not meet your scenario requirements, you can configure custom experts when creating a new project. For detailed operations, refer to [Add a custom expert](https://docs.byteplus.com/en/docs/ArkClaw/Managing_custom_experts_).

<span id="q3VQe0ts"></span>
### Step 3: Create and initialize a project

After entering the collaboration mode, you can start a new project by using either of the following methods.


<Tabs>
<Tab zoneid="HwCcQyO3hS" title="Method 1: Custom creation">
<TabTitle>Method 1: Custom creation</TabTitle>

1. Enter the name and goals of the project that requires collaboration in the dialog box.

   > **Suggestions:** 

   > Specify the task scope, outputs, and timeline clearly. The more specific the goals, the better the collaborative task completion.

   > * **Recommended example**: Complete the e\-commerce mini\-program MVP within 1 week, including product browsing, ordering, and payment features.

   > * **Not recommended**: Create a project.

2. Configure team members.

   * Intelligent member matching (recommended): Click the "+ Custom member \> Intelligent member matching" button.

      Based on the project name and goals you entered, the system automatically matches and recommends the most suitable team from the pool of available members (typically consisting of one project manager and multiple execution members).

      > This feature applies to the following scenarios:

      > * You are using the collaboration mode for the first time and are unsure which roles to use.

      > * You want to quickly get a system\-recommended team plan to reduce the time spent on project setup.

   * Manual configuration of team members: Click the "+ Custom member" button, then select "**Preset expert**" or "**Custom expert**" as needed.

3. After the configuration is complete, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39b89ce07c7770e5404464958549b31a.png) </span> button. After submission, ArkClaw starts the project initialization process.

4. (Optional) View recommended members or adjust the team.

   * View recommended members: After initialization, the system displays a list of members to join the team on the page. We recommend that you pay more attention to the following content:

      * **Role coverage**: Whether the member responsibilities cover the core tasks required for the project.

      * **Matching reason**: Hover over a member's avatar to view the specific reason behind the system recommendation. This helps you determine if they fit the project requirements.

   * Adjust the team: Before the project officially starts, if the recommended members do not meet your expectations, click "Configure members". On the **project members ** page in the **project details** panel, you can add, remove, or replace specific members (for example, adding a custom expert you created).


</Tab>
<Tab zoneid="QC0huLVwKb" title="Method 2: Template-based creation">
<TabTitle>Method 2: Template-based creation</TabTitle>

The system provides a series of preset project templates covering common application scenarios. After you select a template, its preset project name, goals, and collaborative member configurations are automatically populated into the chat box. You can use the template directly or modify the template information as needed.

**Procedure**


1. Click the target template, such as **Short story writing**.

   > You can also place the mouse in the dialog box and press the **Tab** key to switch tasks.   
   

2. In the dialog box, the platform automatically populates the preset team roles, project goals, and other information from the template into the dialog box.

   You can also modify the preset project name, project goals, custom members, and other information.

3. After you confirm that the project content is correct, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e847bf60d719160cfdb2ff04c8c86592.png) </span> button to create a new project.


</Tab>
</Tabs>


<span id="WL4agRZe"></span>
### Step 4 (optional): Configure startup options

After project initialization is completed, the project manager agent will send a confirmation card, prompting you to confirm whether to start the project immediately. Before clicking the **Start task** button, you can configure the following boot options.

<span id="Q0xA8STy"></span>
#### Synchronously create a Lark project group

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once a project is started, you can no longer create a Lark project group for it. To use this feature, create a new project and enable "Synchronously create a Lark group" before starting the task.</div>


To sync the project execution process and results to Lark in real time and interact directly with ArkClaw in a group chat, you can follow the steps below to configure and create your dedicated Lark project group.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can integrate a dedicated Lark bot only by using <strong>Quick pairing</strong>. The <strong>Associate existing bot</strong> option is currently not supported.</div>


   <div data-tips="true" data-tips-type="default"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_48c37134babf9bbf743de0cdfab78468.png" width="333px" />   </div>
   

* <div data-tips="true" data-tips-type="default">After configuration completes, you can directly reuse this bot to synchronously create a project group for a new collaborative project.</div>


* <div data-tips="true" data-tips-type="default">As ArkClaw is designed as a personal AI assistant, using it in group chats may pose risks such as credential leakage. Use it with caution.</div>


1. Create and integrate a dedicated bot.

   > If you have associated the Feishu channel with the primary agent (ArkClaw intelligent assistant) but have not enabled the group creation permission, you can skip this step and proceed to enable the group creation permission.   
   

   1. In the main chat interface of the project, turn on the "Synchronously create a Feishu group" toggle and click the "Start project" button. The system will prompt you to associate the Feishu channel. Click the "Associate Feishu channel" button to go to the ArkClaw intelligent assistant page.

   2. Click the "Connect Feishu" button to complete the operation. For detailed steps, refer to [Quickly create and integrate a bot](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels_1).

      > After successful pairing, your ArkClaw instance automatically restarts to apply the configuration. Please wait patiently.      
      

2. Grant the bot the **Create group** permission.

   > The permission to create a group does not require review. The setting takes effect immediately, and **you do not need to publish the application**.   
   

   You can grant the permission to create a group in the following two ways:

   
   <Tabs>
   <Tab zoneid="606HPowF" title="Method 1: In the project">
   <TabTitle>Method 1: In the project</TabTitle>
   
   1. After the instance restarts, select "My tasks \> Target collaborative project" in the left navigation pane.
   
   2. In the main chat interface of the project, turn on the "Synchronously create a Lark group" toggle and click the "Start project" button. The system will display an insufficient permissions message. Click "Lark permissions" to navigate to the authorization page.
   
   3.  Select the "im:chat:create" permission and click the "Confirm authorization" button.
   
   
   </Tab>
   <Tab zoneid="Og0xJp1X" title="Method 2: In the Feishu Open Platform">
   <TabTitle>Method 2: In the Feishu Open Platform</TabTitle>
   
   1.  Log in to[ the Lark Open Platform](https://open.larksuite.com/app). Select the "Custom Apps" tab, and click the Lark open application you created.
   
   2.  In the left directory tree, select "Development Configuration \> Permissions & Scopes", and click the "Add permission scopes to app" button.
   
   3.  In the Add permission scopes to app pane, select the "tenant_access_token" tab, check the "im:chat:create" permission, and click the "Add Scopes" button.
   
   
   </Tab>
   </Tabs>
   

   3. Enable synchronization in the project.

   1. After the instance permission takes effect, return to the ArkClaw instance page. In the left navigation pane, select "Collaborative projects \> Target project".

   2. In the main chat interface of the project, make sure to enable "Synchronously create a Lark group".


After the configuration, click the "Start project" button to officially start the project.

<span id="0Yb9SIsc"></span>
### Step 5: Dialogue interaction and collaboration

After starting the project, you can converse directly with the **AI project manager**, issue instructions, provide additional materials, or track project progress.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Running multiple projects concurrently in a Starter ArkClaw instance may consume excessive instance resources, which causes slow or no system responses. To ensure the best experience, we recommend that you keep only 1 project running at a time in a Starter instance.</div>


The main interaction rules are as follows:


* **Centralized communication**

   You only need to communicate with the project manager. The project manager is responsible for understanding your requirements, breaking them down into specific tasks, and assigning them to other AI experts in the team.

* **View task progress and output**

   Although you cannot directly communicate with other team members, you can check each member's work progress and output in the following ways:

   1. At the top of the chat box, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6afd22a6f52c1231dac41b97117c5134.png) </span> button to enter the task list and view task progress.

   2. Click the "Open" button next to the output file to preview the detailed content of the output file. You can also download the file to your local device.

* **Reference output files**

   During collaboration, you can use the **reference** feature to import output files as context into the current chat. The system displays referenced items as visual cards and uses the full context to better understand your commands for further analysis, processing, and task optimization.

   **Procedure**

   1. At the top of the chat box, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6afd22a6f52c1231dac41b97117c5134.png) </span> button to enter the task list.

   2. In the expanded task list, click the "Open" button next to the target output file.

   3. Select the file or folder you want to reference as needed.

   4. After selection, the referenced output file/folder will appear in the input box as an **icon\-based text link highlighted in blue**.

      > Before you send a message, confirm whether the referenced task or file information is correct.      
      

   5. In the text box, specify a command for the team (for example, "Optimize the layout of this task output" ) and send the message. After you send the message, the referenced content and your command are saved in the conversation history.

   6. The system automatically parses the referenced context and initiates follow\-up actions based on your latest command. You can view the progress and final results directly in the execution process or task list.


&nbsp;

&nbsp;
