---
title: "Viewing shared Claw data details and session review"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_shared_Claw_data_details_and_session_review"
---

On the "Status and usage" page of the target shared ArkClaw, administrators of the shared Claw can view its basic information, operating status, usage scale, token consumption trend, storage resource usage. Based on this information, you can quickly assess whether the shared ArkClaw instance runs stably, whether employees are consistently using it, and which optimizations are required.

<span id="dkQuu6sh"></span>
## Go to the Claw status and usage page


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target shared Claw with an administrator identifier.

3. Hover over the target shared Claw instance, and click the "View Claw details" button.

4. Select the "Status and usage" tab to view the shared ArkClaw basic information and perform management operations. You can also view the token usage, and usage trends about your shared Claw.


<span id="tylmEkwx"></span>
## Basic information

View the basic information of the target shared Claw and perform management operations.


|Metric |Description |
|---|---|
|Basic information |Current shared ArkClaw version, model source, configuration, and other related information. |
|Related operation |In this module, you can change the shared ArkClaw avatar and name, and perform the following management operations:<br><br><br>* **Edit the shared ArkClaw name**: Click the edit button next to the shared ArkClaw name. Enter the name in the pop\-up dialog box, and click the "Confirm" button to complete the operation.<br><br>* **Check for updates:**  Upgrade versions of the shared ArkClaw system and core components, such as "Message channel" and "Memory management", to ensure stable running of your shared ArkClaw. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_version_?lang=en).<br><br>* **AI diagnosis**: When shared ArkClaw exceptions occur, such as no response or startup failure, you can manually trigger AI diagnosis, and the system will automatically perform troubleshooting and repair. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/One-click_diagnosis_of_ArkClaw__?lang=en).<br><br>* **Auto healing: ** When your shared ArkClaw becomes unavailable due to tasks, setting adjustments, or other reasons, you can use the auto healing feature to attempt to restore it to the latest available state.<br><br>* **More configurations:** <br><br>   * **Restart:**  You can manually restart shared ArkClaw when you need to load new shared ArkClaw configuration, when shared ArkClaw responds slowly, or in other situations. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Restarting_ArkClaw__?lang=en).<br><br>   * **View terminal: ** You can access shared ArkClaw from terminals and use Shell commands to perform various operations (such as viewing directories and files in the current path, creating tasks, and so on). **This is suitable for technical developers who require advanced usage of ArkClaw.**  [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Accessing_ArkClaw_from_terminals_?lang=en).<br><br>   * **Restore factory settings: ** You can reinitialize the shared ArkClaw service and reset it to the initial available state when your ArkClaw configuration is corrupted and causes a service crash, or when system failures or abnormal states occur and cannot be recovered. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings__?lang=en).<br><br>* **Adjust model configuration: ** After the administrator configures multiple models, you can change the inference model used by shared ArkClaw based on actual business scenarios **.**  [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__?lang=en).<br><br>* **Administrator**: You can assign administrators to a specified shared Claw. Employees assigned as administrators can use and manage the shared Claw. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Initializing_shared_Claw#5PQcqYm4). |


<span id="DLl6CAp0"></span>
## **Basic statistics**

View the running time, number of members, and activity of the shared ArkClaw to quickly assess its basic running status.


|Metric |Description |
|---|---|
|Running time |The current duration of continuous operation of the shared ArkClaw. |
|Agents |The number of agents in the current shared ArkClaw instance, including the primary agent and added members (agents). |
|Number of shared members |The total number of members who have been added or are authorized to use the shared ArkClaw. |
|The number of active members in the last 7 days |The number of members who actually used the shared ArkClaw in the last 7 days. |


<span id="56mjvmX3"></span>
## **Usage trend**

View the number of tasks, resolution effectiveness, message processing volume, token consumption, and storage usage to assess the shared Claw's actual usage volume, problem resolution effectiveness, and overall cost changes.


|Metric |Description |
|---|---|
|Number of processed messages |The total number of messages processed by the shared ArkClaw during the selected period. |
|Token |The total number of tokens consumed by the current shared ArkClaw during the selected period, which is measured in thousands (K). |
|Storage usage (GB) |The used storage capacity and total storage capacity of the current shared ArkClaw. Supported operations:<br><br><br>* Viewing of the storage breakdown of used space by file category, including system files, cached data, plugins, skills, and more.<br><br>* [One-click cache data cleanup](https://docs.byteplus.com/en/docs/ArkClaw/Clearing_ArkClaw_storage_cache_data__?lang=en) |
|Message processing trend |The count trend of messages processed by shared ArkClaw during the selected period. |
|Token usage trend |Token usage trend of the shared ArkClaw during the selected period. |
|Number of effective tasks |The total number of resolved tasks, unresolved tasks, and tasks with an indeterminate status during the selected period, excluding invalid conversations such as "hi". |
|Number of resolved tasks |The number of effective tasks determined to be resolved during the selected period.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Tasks that receive a like, are explicitly confirmed as resolved, or have a completed agent workflow are all considered resolved tasks.</div><br> |
|Number of unresolved tasks |The number of effective tasks determined to be unresolved during the selected period.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Tasks are considered unresolved if they receive a dislike or negative feedback, are explicitly marked as unresolved, or involve an interrupted agent workflow, insufficient permissions, or missing content.</div><br> |
|Effective resolution rate |The ratio of resolved tasks to effective tasks during the selected period, which can be used to measure the overall efficiency of the shared ArkClaw when processing effective tasks. |
