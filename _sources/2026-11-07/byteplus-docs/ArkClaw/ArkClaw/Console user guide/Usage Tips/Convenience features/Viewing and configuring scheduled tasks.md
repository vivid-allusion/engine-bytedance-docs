---
title: "Viewing and configuring scheduled tasks"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks_9"
---

ArkClaw responds to your requests in real time and supports scheduled tasks. It acts as a personal assistant that automatically completes tasks at scheduled times to **remind you**.

<span id="ddCzxxpf"></span>
## Concept


|Concept |Definition |
|---|---|
|Scheduled tasks |Task automatically triggered at the specified time based on the user's preset time and content. |
|Test run |Manual test that can be initiated at any time. This operation does not affect the configured scheduled task and is only used to verify whether the configuration of the newly created task meets expectations. |


<span id="5xV3yEQF"></span>
## Create scheduled tasks

If you have not yet created scheduled tasks or need to add new ones, you can quickly create them via templates or custom configurations to deliver proactive reminders in various scenarios.

<span id="MhOng55L"></span>
### Prerequisites

To push scheduled task information to message channels (Feishu, WeCom, WeChat, and DingTalk), complete the [integration of message channels](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels_1) first.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">By default, ArkClaw receives scheduled task information in the session. You can also choose not to integrate message channels.</div>


<span id="RKvNLP8y"></span>
### Procedure


<Tabs>
<Tab zoneid="KwwWjokv" title="(Recommended) template-based scheduled task creation">
<TabTitle>(Recommended) template-based scheduled task creation</TabTitle>

You can use system preset templates to easily and quickly create scheduled tasks.


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

3. Click the target scheduled task template, for example, "Industry public opinion".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_96aa84054903f2078bce343411106362.png) </span>

4. Confirm whether the content of the selected template fully meets your requirements.

   * If the template meets your requirements, click "Confirm" to complete the operation.

   * If the template does not meet your requirements, adjust the relevant content and then click "Confirm" to complete the operation. For parameter descriptions, refer to **Creating personalized scheduled tasks**.

5. After a scheduled task is created, it **does not run ** by default. The system automatically executes the task based on the specified execution time.

6. (Optional) To ensure that the task configuration is valid, we recommend that you perform a test run after the task is created to verify whether it meets your expectations.

   1. Find the created task in the task list, and click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c608a4a7490d93dbb823f5b842d7d4b5.png) </span> to run a test.

   2. Check the test run result: If "**Last execution succeeded**" appears and ArkClaw returns a message similar to the following, the scheduled task is successfully configured.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In this example, the "Web" channel is used as the push channel.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the push channel of the scheduled task is set to "Feishu", "WeCom", "WeChat", or "DingTalk", check the push message on the corresponding platform.      </div>
      


</Tab>
<Tab zoneid="CrN0u133" title="Personalized scheduled task creation">
<TabTitle>Personalized scheduled task creation</TabTitle>

When the system preset templates cannot cover your business scenario, you can create custom scheduled tasks to meet personalized and customized business requirements.


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

3. Click the "Create scheduled task" button. Then, configure the parameters described in the following table to complete the scheduled task configuration.

   
   |Parameter​ |Description |
   |---|---|
   |Term |Enter the name of the scheduled task. For example, "Weather and Outfit". |
   |Execution agent |Specify the agent to handle the current task and generate corresponding outputs. The default agent is ArkClaw intelligent assistant. If you have created a team, you can also select other in\-team agents based on your needs. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Building_agent_teams_with_one_click_). |
   |Prompt |Provide a prompt that describes the reminder task. The system will send a reminder at the scheduled time based on the provided prompt. Example:<br><br>> Act as my personal assistant and remind me of the weather details in Chengdu and Xi'an.<br><br>> Your tasks include:<br><br>> 1. Identify the weather details of Chengdu and Xi'an separately.<br><br>> 2. Recommend daily outfits for me based on the specific weather. |
   |Execution time |The time when you want to be reminded. For example, every day at 9:00 AM. |
   |Push channel (Optional) |Select the channel (platform) for receiving scheduled task information as needed. Currently supported channels include "Web", "Feishu", "WeCom", "WeChat", and "DingTalk".<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">By default, the "Web" channel is used, which means scheduled task information will be automatically sent to ArkClaw.</div><br> |
   |Push to target group (optional) |When the push channel is set to **Feishu**, and there are available Feishu groups, you can select the corresponding Feishu groups as message recipients. |
   

4. Click the "Confirm" button to complete the operation.

   After the task is created, its initial status is **Not executed**. The system will automatically trigger and run the task at the specified time.

5. (Optional) To ensure that the task configuration is valid, we recommend that you perform a test run after the task is created to verify whether it meets your expectations.

   1. Find the target task in the task list and click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c608a4a7490d93dbb823f5b842d7d4b5.png) </span> to run a test.

   2. Check the test run result: If "**Last execution succeeded**" appears and you have received the corresponding scheduled task information, the scheduled task is successfully configured.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In this example, the "Web" channel is used as the push channel.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the push channel of the scheduled task is set to "Feishu", "WeCom", "WeChat", or "DingTalk", check the push message on the corresponding platform.      </div>
      


</Tab>
</Tabs>


<span id="7vdmMUbS"></span>
## View scheduled tasks

<span id="DjiVZFLz"></span>
### View the scheduled task calendar

Use the calendar view to view scheduled tasks by week or month. The calendar clearly displays task execution windows, helping you plan and manage tasks centrally and quickly identify scheduling conflicts to prevent overlapping execution windows.


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

3. Click the **Calendar** tab to switch to the calendar view.

4. In the upper\-right corner of the page, click the  **"Week"**  or "**Month"**  tab to view all scheduled tasks by week or month.

5. You can also perform the following operations:

   * **View the details of the target scheduled task**: Click the target scheduled task. For more information, see [View scheduled task details](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks_9#9ULtf8zO).

   * **Create a scheduled task:**  Select the target date, and then click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b993a3aa3b61c0b5a7c6d6f51e4e529f.png) </span> icon to create a scheduled task. For more information, see [Create scheduled tasks](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks_9#5xV3yEQF).


&nbsp;

<span id="wgjqnfrb"></span>
### View scheduled task templates

You can view all scheduled task templates at any time and quickly learn about the configuration information of various commonly used tasks. It is convenient for direct reference or selection and helps improve the efficiency of task creation.


1. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

2. View all scheduled task templates.

   * Click a template to view its details. For example, click "Daily summary" to view the complete configuration information for that template.

   * You can also directly select the target template to [create scheduled tasks](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks_9#5xV3yEQF).


<span id="9ULtf8zO"></span>
### View scheduled task details

You can view all created scheduled tasks at any time and clearly check detailed information such as the execution time, status, and execution traces of each task.


1. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

2. In the list of created scheduled tasks, you can view the following information:

   <mark>
   |Feature |Description |
   |---|---|
   |Filter scheduled tasks |The final result of the latest execution of each task is displayed by default. You can click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fb4d503ec2baca273e57d554764ee2c.png) </span> icon, select the target execution statuses, and click the "Confirm" button to quickly locate scheduled tasks with different statuses. |
   |Statistics for the past 7 days |It displays **all scheduled tasks under the current account**, as well as core statistics including total token consumption, execution success rate, and cumulative execution counts in the past 7 days. This helps you quickly learn the overall running health and resource consumption of tasks. |
   |Details |In the "Actions" column of the target task, select " **··· \> ** Details" or click anywhere in the row of the target task to enter the details page of the task and view the following information:<br><br><br>* **Task configuration**: Displays the execution time, next execution time, execution agent, prompt, push channel, and other information of the target task.<br><br>* **Statistics for the past 7 days**: Displays the average token consumption, execution success rate, cumulative execution counts, and average duration for **the target task** over the past 7 days.<br><br>* **Execution history**: Displays all execution records of the target task. You can view the execution time, status, used model, and other information of each record. You can also perform the following operations on a single record:<br><br>   * **Execution trace**: In the "Actions" column of the target execution record, click the "View execution trace" button to track the complete call chain of the scheduled task, including the reasoning chain, tool calls, and full input and output records of this execution. [Learn more about execution trace details](https://docs.byteplus.com/en/docs/ArkClaw/viewing_agent_execution_traces#18cxtrVZ).<br><br>   * **In\-depth diagnosis**: If the basic diagnosis indicates an exception, you can select "Execution trace  **\>**  In\-depth diagnosis" for a comprehensive diagnosis. For details, refer to [Execution trace diagnosis](https://docs.byteplus.com/en/docs/ArkClaw/viewing_agent_execution_traces#tUYm1rcw). |
   |Actions |In the "Actions" column of the target scheduled task, you can enable/disable, edit, copy, or delete the scheduled task. For details, refer to [Managing scheduled tasks](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks_9#LdJh3cTb). |
   </mark>


<span id="LdJh3cTb"></span>
## Manage scheduled tasks


<Tabs>
<Tab zoneid="NkKzmWyQ" title="Edit scheduled tasks">
<TabTitle>Edit scheduled tasks</TabTitle>

You can use the "Edit" feature to modify a scheduled task, such as its keyword, execution time, and notification channel, to meet your varying needs.


1. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

2. In the task list, select " **··· \> ** Edit".

3. After the modification, click "Confirm" to complete the operation. For parameter descriptions, refer to [Creating scheduled tasks](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks_9#5xV3yEQF).


</Tab>
<Tab zoneid="yWcJBVmL" title="Copy scheduled tasks">
<TabTitle>Copy scheduled tasks</TabTitle>

To create multiple scheduled tasks with similar configurations, you can use the "Copy" feature to quickly generate duplicates. This eliminates the need to repeatedly configure task settings (such as the keyword, execution time, and notification channel), enabling you to complete scheduled task configuration efficiently.


1. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

2. In the task list, select " **··· \> ** Copy".

3. Confirm whether the copied content fully meets your requirements.

   * If it meets your requirements: Click "Confirm" to complete the operation.

   * If it does not meet your requirements: Adjust the parameters as needed, and then click "Confirm" to complete the operation. For parameter descriptions, refer to [Creating scheduled tasks](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_and_configuring_scheduled_tasks_9#5xV3yEQF).


</Tab>
<Tab zoneid="vL8AG5Pz" title="Enable or disable scheduled tasks">
<TabTitle>Enable or disable scheduled tasks</TabTitle>

By default, a scheduled task is ** enabled** after it is created. You can manually disable it as needed and enable it again at any time.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">After you disable a scheduled task, the system no longer automatically executes the target task at the preset time. The configured task content and parameters will not be lost, and the task will resume normal execution once it is enabled again.</div>


1. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

2. Choose to enable or disable a scheduled task as needed.


</Tab>
<Tab zoneid="ixNdrFeY" title="Delete scheduled tasks">
<TabTitle>Delete scheduled tasks</TabTitle>

After a scheduled task is deleted, the system no longer automatically executes the target task at the preset time. This operation cannot be undone. Proceed with caution.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">If you delete a scheduled task, the system does not delete the corresponding chat history. You can still view it in the chat history list.</div>


1. Switch to the target ArkClaw page, and select "Scheduled tasks" in the directory tree on the left.

2. In the task list, select " **··· \> ** Delete".

3. After you confirm the information of the scheduled task you want to delete, click the "Delete" button to complete the operation.





</Tab>
</Tabs>
