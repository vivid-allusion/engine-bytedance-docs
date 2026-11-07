---
title: "Employee-side console usage overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Employee-side_console_usage_overview"
---

This topic describes the employee\-side console of ArkClaw to help **enterprise employees** quickly understand how to use the console and provides document entries for common features.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The login, application, and session pages visible to enterprise employees, as well as optional model sources, models, seat editions, and available features, are all specified by the enterprise administrator. The actual pages shall prevail. To use a certain capability, please contact your enterprise administrator for configuration.</div>


<span id="ptdgqGku"></span>
## Overview

ArkClaw Enterprise provides a console centered on **tasks** and **agents**: You can initiate tasks on a single page, select appropriate professional agents for execution, and view and download output after task completion.

**What will you do:** 


1. Apply for your first ArkClaw instance.

2. Enter the console and initiate your first task.

3. (Optional) Select an expert agent which is better suited to your scenario from the Agent Gallery or create a custom agent. Then, initiate a task.

4. View task progress and obtain output.


<span id="PXU9zomX"></span>
## Concept

We recommend that you learn the basic concepts below prior to use:


|Term |Description |
|---|---|
|Task |A work unit with a clear objective, for example, "Generate a weekly report", "Sort meeting minutes", or "Compare two proposals and provide a suggestion". |
|Agent |An assistant with specific capabilities and knowledge structure. Different agents are suitable for different task types. |
|Skill |Capability components that agents can call (such as document processing and data analysis components). |
|Quick commands |Trigger fixed processes or capabilities by entering shorter texts (such as `/`). |
|Console |The main entrance for initiating tasks, interacting with the agents, and viewing the task process and outputs. |
|Agent Gallery |An entrance for centralized browsing and selection of preset and recommended agents. |
|My agents |View the custom agents you recruited or created, and perform configuration, debugging, sharing and other management operations. |


<span id="jrIxHuGM"></span>
## Quick start


1. [Apply for an ArkClaw instance](https://docs.byteplus.com/en/docs/ArkClaw/Applying_for_ArkClaw_instances_?lang=en).

   If you are using ArkClaw for the first time, you need to apply for an instance first.

2. Enter the console.

   After the instance is ready, enter the console to get started.

3. Initiate a task.

   * [Direct initiation](https://docs.byteplus.com/en/docs/ArkClaw/Initiating_tasks): Input your objectives and constraints in the console and instruct the default agent to execute the task.

   * [Specify an agent for execution](https://docs.byteplus.com/en/docs/ArkClaw/Adding_agents_and_managing_my_agents?lang=en): In the task, use `@` to select a specific agent (such as finance specialist, legal specialist, developer, data analyst or any other role) to focus more on completing the task.

   * Use [quick commands](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_quick_commands_?lang=en)/[skills](https://docs.byteplus.com/en/docs/ArkClaw/Learning_and_using_skills_?lang=en): Use `/` to invoke common capabilities or commands (such as certain fixed processes or templated tasks).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During task execution, do not switch agents to avoid interruption or failure of the task.   </div>
   

4. View progress and download output.

   In the task list of the console, you can view the real\-time progress of the current task and download the generated files or reports after the task is completed.


<span id="9V2xiA14"></span>
## Manage agents


|Feature |Description |
|---|---|
|[Adding and managing my agents](https://docs.byteplus.com/en/docs/ArkClaw/Adding_agents_and_managing_my_agents?lang=en) |A larger agent list can cover more business scenarios and help assign a more suitable expert role for each task. You can add agents from Agent Gallery and create custom agents. |
|[Publish as an enterprise template](https://docs.byteplus.com/en/docs/ArkClaw/Adding_agents_and_managing_my_agents#BkjHP8CY) |ArkClaw supports publishing custom agents as enterprise templates. This allows employees to create ArkClaw instances quickly based on the templates assigned to them. |
|[Configuring independent message channels for my agents](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_independent_message_channels_for_my_agents) |After adding sub\-agents from Agent Gallery or custom sub\-agents to ArkClaw, in addition to configuring messaging channels (such as Feishu and DingTalk) for the primary agent, you can also configure message channels for each sub\-agent. Additionally, you can enable or disable the message synchronization feature to choose whether to sync and display the chat history from third\-party message channels to ArkClaw (web). This allows you to centrally manage all conversations on the web interface. |
|[Configure models for my agents](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_models_for_my_agents?lang=en) |After adding sub\-agents from Agent Gallery or custom sub\-agents to ArkClaw, you can specify an inference model for each sub\-agent. This allows you to flexibly select the most suitable model based on agent roles and task characteristics to configure differentiated inference capabilities. |
|[Configuring skills for my agents](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_skills_for_my_agents) |After adding sub\-agents from Agent Gallery or custom sub\-agents to ArkClaw, you can add skills to or remove preset skills from each sub\-agent. Each sub\-agent will only retain capabilities that match its responsibilities. |
|[Configuring tools for my agents](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_tools_for_my_agents) |After adding sub\-agents to ArkClaw (from the Agent Gallery or by custom creation), you can enable or disable tools for each sub\-agent independently and retain only the capabilities the sub\-agent actually needs for greater security and efficiency. |
|[Setting sub-agent scheduling priority](https://docs.byteplus.com/en/docs/ArkClaw/Setting_sub-agent_scheduling_priority) |You can control whether sessions initiated by the **primary agent** prioritize sub\-agent scheduling. By default, prioritized sub\-agent processing is disabled. If your business has strict requirements for task distribution chains, we recommend that you enable this feature to improve the stability of sub\-agent calls. |
|[Viewing and upgrading agent versions](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_upgrading_agent_versions?lang=en) |The ArkClaw platform continuously iterates on agent templates to expand and refine the business functions and improve runtime stability. You can check the current version of a template at any time and upgrade it as needed to access the latest capabilities. |
|[Viewing and adding preset scheduled tasks](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_adding_scheduled_tasks_preset_in_agent_templates_01?lang=en) |Some agent templates are preset with exclusive scheduled tasks to fit recurring business scenarios. After you add such a template to an agent team, the system will automatically generate the scheduled tasks of the template, without manual configuration of scheduling rules. |
|[Setting agent team collaboration mode](https://docs.volcengine.com/docs/87732/2598366?lang=zh) |You can enable the team collaboration scheduling mode as needed, which enables intelligent matching of professional sub\-agents for cross\-domain collaboration and improves task processing efficiency. |
|[Delete an agent](https://docs.byteplus.com/en/docs/ArkClaw/Adding_agents_and_managing_my_agents#BkjHP8CY) |You can delete **custom agents ** and agents **added from Agent Gallery** only. **You cannot delete the primary agent**. |


<span id="PFbJdKI2"></span>
## Convenience features


|Feature |Description |
|---|---|
|[Initiating tasks](https://docs.byteplus.com/en/docs/ArkClaw/Initiating_tasks) |By default, purchased ArkClaw has only one conversation task. If you want to start a new task unrelated to the current conversation while keeping your existing conversation for parallel task processing, you can create a new conversation. |
|[Viewing and managing task outputs](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_managing_task_outputs) |ArkClaw supports viewing all outputs generated by the current session and uploaded reference files, previewing their content, downloading them to local devices, transferring them to the cloud disk, and sharing with department employees. |
|[Adjusting ArkClaw inference models](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__?lang=en) |After the administrator configures multiple models, you can change the inference model as needed. |
|[Learning and using skills](https://docs.byteplus.com/en/docs/ArkClaw/Learning_and_using_skills_?lang=en) |ArkClaw includes some commonly used built\-in skills that can be automatically matched and called based on task requirements. ArkClaw also supports integration with community plug\-ins from channels such as ClawHub. You can expand new skills for ArkClaw in multiple fields such as programming, browser operations, office work, and expert roles as needed. |
|[Viewing and configuring scheduled tasks](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks__?lang=en) |ArkClaw can not only passively answer and address your questions in real time, but also execute the scheduled tasks you set and **proactively send you reminders**. |
|[Conversation retrieval](https://docs.byteplus.com/en/docs/ArkClaw/Conversation_retrieval) |This feature allows you to quickly search historical task content by keyword and jump to the corresponding conversation with one click. Whether you need to review previous communication details or continue a conversation in a previous conversation, this feature helps you locate information efficiently. This feature covers various retrieval scenarios, including titles, body text, phrases, multiple keywords, entities, and code. |
|[File space](https://docs.byteplus.com/en/docs/ArkClaw/File_space?lang=en) |During daily use, ArkClaw generates a large number of files (such as presentations, documents, images, videos, and code) in its workspace (.openclaw/) based on your task requirements. The **file space** feature allows you to perform complete file management operations such as uploading, downloading, browsing, and deleting files in this directory while ensuring system security. |
|* [Claw cloud disk](https://docs.byteplus.com/en/docs/ArkClaw/Claw_cloud_disk?lang=en)<br><br>* [Personal cloud disk](https://docs.byteplus.com/en/docs/ArkClaw/Personal_cloud_disks?lang=en) |You can use a TOS bucket from [Torch Object Storage (TOS)](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos) as a cloud disk to quickly upload or download files between your local environment and the cloud. ArkClaw can use files from the cloud disk as task materials, and can also place files generated after task execution (such as documents, images, and videos) into the cloud disk. This makes the files available for you to download locally. |
|[Uploading and processing files](https://docs.byteplus.com/en/docs/ArkClaw/Uploading_and_processing_files?lang=en) |ArkClaw provides convenient features such as local file upload, selection of cloud disk files, file preview, intelligent processing, and zoom preview. You can quickly complete intelligent identification and in\-depth analysis of files by selecting files from cloud disks, uploading local files, copying and pasting files, or other methods, enriching chat scenarios and improving processing efficiency. |
|[Using Codex Programming](https://docs.byteplus.com/en/docs/ArkClaw/Using_Codex_Programming) |Codex Programming is a coding agent running in the ArkClaw terminal. It can be used to write code, execute scripts, and modify files via natural language commands. |
|[Using Hermes](https://docs.byteplus.com/en/docs/ArkClaw/Using_Hermes_Agent__) |Hermes can run directly within ArkClaw, sharing its conversation context and memory data. This enables precise understanding of user needs and ensures consistent logic and content throughout multi\-turn conversations. You can use Hermes directly on the platform for related operations. |
|[Switch thinking mode](https://docs.byteplus.com/en/docs/ArkClaw/Switching_thinking_mode_?lang=en) |You can flexibly switch among Fast, Standard, and Expert thinking modes based on task complexity and response time requirements. This helps match scenarios on demand, reduce redundant thinking time, and improve conversation efficiency. |
|[Taking over cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_?lang=en) |A cloud PC is a fully functional cloud\-based virtual computer hosted in the ArkClaw environment. It provides a complete desktop operating environment, allowing you to browse the web pages and run or manage various applications just like on a local computer. |
|[Take over a cloud browser](https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_browsers__?lang=en) |ArkClaw may execute browser automation tasks or encounter graphical interface interactions that it cannot handle independently. These include complex graphic captchas, QR code login, high\-risk permission confirmation, and other similar scenarios. You can then manually take over the cloud browser and enter split\-screen mode to complete verification and processing. |
|[Switching execution mode of cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Switching_execution_mode_of_cloud_PC_?lang=en) |Supports flexible switching among the auto mode, browser mode, cloud desktop mode, and OpenCli mode to match task complexity. |
|[Automated office capabilities of cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Automated_office_capabilities_of_cloud_PC_?lang=en) |Supports directly calling and running Office components in the cloud to automate the creation and processing of documents, spreadsheets, slides, and other files. |
|[Desktop operation recording and prompt generation](https://docs.byteplus.com/en/docs/ArkClaw/Desktop_operation_recording_and_prompt_generation_?lang=en) |Supports the generation of structured prompts via cloud PC operation recording. The prompts can be executed automatically in real time or saved as dedicated task templates for reuse. |
|[Evaluating and providing feedback on ArkClaw responses](https://docs.byteplus.com/en/docs/ArkClaw/Evaluating_and_providing_feedback_on_ArkClaw_responses_?lang=en) |Conversation messages support message\-level feedback. You can like or dislike individual responses from ArkClaw, and specify detailed reasons when submitting dislikes. The platform leverages your feedback to identify flaws in ArkClaw responses, so as to continuously optimize response performance, interaction experience, and stability. |
|[Managing system notifications](https://docs.volcengine.com/docs/87732/2431037) |To ensure you stay updated with the latest developments of ArkClaw in real time, BytePlus provides a system notification mechanism. When ArkClaw releases version updates and new features, the platform will push relevant information to you in a timely manner. |
|[Feedback](https://docs.byteplus.com/en/docs/ArkClaw/Feedback_?lang=en) |If you encounter issues that you cannot resolve while using ArkClaw, or have new suggestions for ArkClaw, you may inform us via the feedback feature. |
|[Exiting ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Exiting_ArkClaw_?lang=en) |You can exit the ArkClaw conversation page when you no longer need to use ArkClaw. |


<span id="B70gWEDj"></span>
## Advanced features


|Feature |Description |
|---|---|
|[Configure message channels](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__?lang=en) |ArkClaw supports integration with message channels such as Lark and Slack. After the integration, you can chat with ArkClaw through the corresponding message channel. ArkClaw can also use bot capabilities to help you perform operations such as creating documents and scheduling calendar events. |
|[Access OpenClaw console](https://docs.byteplus.com/en/docs/ArkClaw/Accessing_OpenClaw_console__?lang=en) |ArkClaw is a cloud edition built on OpenClaw. It supports one\-click access to the **OpenClaw console**, providing a visual operation and management experience. |
|[Operating local browser](https://docs.byteplus.com/en/docs/ArkClaw/Operating_local_browser?lang=en) |Supports connecting the local browser and the cloud runtime environment (AgentKit Runtime / OpenClaw) via the ArkClaw Janus plugin. No code is required. Simply record your web operations, and the system will automatically generate standardized automation skills, quickly enabling automation of web tasks. |
|[Downloading conversations](https://docs.byteplus.com/en/docs/ArkClaw/Downloading_conversations?lang=en) |You can download the full history of the current chat locally for retention, archiving, sharing, and further sorting. |
|[Upgrading ArkClaw version](https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_version_?lang=en) |You can update your ArkClaw system and component versions with one click to unlock the latest capabilities and ensure stable system operation. |
|[Restarting ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Restarting_ArkClaw__?lang=en) |You can manually restart ArkClaw when you need to load new ArkClaw configuration, when ArkClaw responds slowly, or in other situations. |
|[AI diagnosis](https://docs.volcengine.com/docs/87732/2485345?lang=zh) |When ArkClaw exceptions occur, such as no response or startup failure, you can manually trigger AI diagnosis, and the system will automatically perform troubleshooting and repair. |
|[Auto healing of ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Auto_healing_of_ArkClaw__?lang=en) |When your ArkClaw becomes unavailable due to tasks, setting adjustments, or more, you can use the auto healing feature to attempt to restore it to the latest available state. The healing process takes approximately 1–2 minutes. Wait patiently. |
|[Restoring ArkClaw to factory settings](https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings__?lang=en) |If the service crashes due to corrupted configuration, or if system failures, abnormal status, and other unrecoverable issues occur, you can restore the ArkClaw service with one click to its original available state. The process takes about 1–2 minutes. Wait patiently. |
|[Accessing ArkClaw from terminals](https://docs.byteplus.com/en/docs/ArkClaw/Accessing_ArkClaw_from_terminals_?lang=en) |You can access ArkClaw from a terminal and use Shell commands to perform various operations (such as viewing directories and files in the current path, creating tasks, and so on). **This is suitable for technical developers who need in\-depth usage.**  |
|[Managing my images](https://docs.byteplus.com/en/docs/ArkClaw/Managing_my_images) |Supports image management. Employees can create reusable custom images configured with souls, built‑in plugins, and built\-in skills. |
|[Migrate OpenClaw to ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Migrating_OpenClaw_to_ArkClaw__) |With the migration feature, you can quickly migrate existing OpenClaw data to ArkClaw. After migration, ArkClaw will use the memories, skills, and other data accumulated in OpenClaw to maintain consistency with your original usage habits and operation logic. This enables a smooth transition with zero learning cost and no service interruption. |
|[Insufficient memory alert](https://docs.byteplus.com/en/docs/ArkClaw/Troubleshooting_and_handling_methods_for_insufficient_ArkClaw_memory?lang=en) |When the memory of an ArkClaw instance is insufficient, an alert notification is triggered for this issue. You can quickly resolve the memory shortage issue by closing the browser, checking for updates, and other methods. |
|[Insufficient storage capacity alert](https://docs.byteplus.com/en/docs/ArkClaw/Troubleshooting_and_handling_methods_for_insufficient_ArkClaw_storage_space?lang=en) |When the storage capacity of an ArkClaw instance is insufficient, an alert notification is triggered for this issue. You can quickly resolve the insufficient storage capacity issue by clearing redundant files, releasing system cache, and other methods. |


<span id="mKDblxky"></span>
## Manage ArkClaw instances


|Feature |Description |
|---|---|
|[Viewing ArkClaw status and usage](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_status_and_usage?lang=en) |You can view the current ArkClaw health status, token usage statistics, usage trend, and resource allocation for the instance. |
|[Viewing ArkClaw security logs](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_security_logs__?lang=en) |ArkClaw comes with the built\-in AI security assistant enabled by default. You can view information about ArkClaw\-related risk events monitored and defended by this feature. |
|[Enabling/Disabling ArkClaw plugins](https://docs.byteplus.com/en/docs/ArkClaw/Enabling_and_Disabling_ArkClaw_plugins) |You can manually enable or disable ArkClaw feature extension components to flexibly control their functional scope. |
|[Clearing ArkClaw storage cache data](https://docs.byteplus.com/en/docs/ArkClaw/Clearing_ArkClaw_storage_cache_data__?lang=en) |You can use the one\-click cleanup feature to safely and quickly free up storage capacity on your ArkClaw. This feature only clears temporary cache data generated during ArkClaw runtime. It does not affect your personal data, installed skills, or plugins. |
|[Back up and restore ArkClaw data](https://docs.byteplus.com/en/docs/ArkClaw/Backing_up_and_restoring_ArkClaw_data__?lang=en) |This feature can fully restore the **entire ArkClaw system and all data** to the state at the time corresponding to your selected backup. After restoration, the system will be the same as its state when the backup was created. |
|[ArkClaw Enterprise memory management](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Enterprise_memory_management__?lang=en) |ArkClaw supports the visualized memory management feature that enables more precise memory storage, retrieval, and application solutions based on LanceDB. ArkClaw also offers the AutoDream feature for intelligent memory governance, resolving memory confusion and inaccurate recall issues. |
|[Setting Webhook](https://docs.byteplus.com/en/docs/ArkClaw/Setting_Webhook) |You can configure Webhook to autonomously control A2A\-protocol\-based external access to your ArkClaw, establishing a linked call channel between ArkClaw and the internal business system of your enterprise. |


<span id="howBMFo2"></span>
## Manage shared Claw


|Feature |Description |
|---|---|
|[Use shared Claw](https://docs.byteplus.com/en/docs/ArkClaw/Initializing_shared_Claw?lang=en) |Shared Claw refers to permission\-governed Claw instances for team sharing. It fits collaborative workflows that require centralized agent configurations, shared knowledge bases, and standardized execution environments. |
|[Configuring shared Claw message channels](https://docs.volcengine.com/docs/87732/2597087) |Shared Claw administrators can integrate bot message channels for shared Claw and grant relevant personnel permissions to use the message channel applications. After authorization, enterprise employees without administrative permissions can directly use the shared Claw via the configured message channels. |
|[Configuring agents for shared Claw](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_agents_for_shared_Claw) |Shared Claw administrators can edit the visibility scope of agents, update agent configurations (skills, tools, .MD files, etc.), and manage agents based on versions. |
|[Viewing shared Claw data details and session review](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_shared_Claw_data_details_and_session_review) |On the "Status and usage" page of the target shared ArkClaw, administrators of the shared Claw can view its basic information, operating status, usage scale, token consumption trend, storage resource usage, and session review information. Based on this information, they can quickly assess whether the shared ArkClaw instance runs stably, whether employees are consistently using it, and which optimizations are required. |
