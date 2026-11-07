---
title: "Scheduled Task"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Scheduled_Task"
---

This operation document is used to explain how to create, manage, and view the results of iDA scheduled tasks, and to help you configure repetitive tasks such as daily newspaper generation, data query, and industry briefing into automated tasks. You can run tasks by day, week, month, or at a specified time, and view the execution results through an iDA session or Lark push.

<span id="ad520bc6"></span>
# Prerequisite


* The scheduled task function is only available for iDA agents.


<span id="ab36440e"></span>
# Create a new scheduled task


1. Log in to the BytePlus iDA console, enter the agent list, and select the agent to enter the Q & A interface.

2. Select the scheduled task at the top of the left navigation bar to enter the task list, click the New Scheduled Task button at the top right of the list, and fill in the task\-related configuration items to confirm. The following are relevant instructions for configuration items:


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you have not created a task, you can click the New Scheduled Task button in the center of the interface to create a new task.</div>



|Configuration item name |Is it required? |Explain |
|---|---|---|
|Agent |Yes |Select the agent that executes the scheduled task, and the currently available agent is displayed by default, which can be switched through the drop\-down box. |
|State |Yes |Controls whether scheduled tasks are enabled and turned on by default; when turned off, tasks do not execute automatically as planned. |
|Task name |Yes |Fill in the task name to identify the task in the task list and runtime. |
|User command |Yes |Fill in the specific requirements that the agent needs to perform after the task is triggered, such as querying data, generating reports, or summarizing information.<br><br>For example, you could type: Help me summarize today's news about the artificial intelligence industry and generate a newsletter.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The user command text box provides access to resources (DataWind datasets) and upload local file entries, while specifying relevant skills and enabling online search.</div><br> |
|Running time |Yes |Set the task execution cycle, including a specified time, daily, weekly, and monthly. Depending on the specified time type selected, select a different specific time. |
|Set expiration time |Yes |After checking, you can select the task expiration time, and the task will stop automatically executing after expiration. |
|Lark push |No |After opening, the completion of the task execution will push the result to the bound Lark account. Click Authorize Now to jump to the authorization page to authorize. For authorization, please refer to the [Operation Processes of Lark Binding and Authorization](https://docs.byteplus.com/docs/dataagent/Operation_Processes_of_Lark_Binding_and_Authorization). |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ac8b0690c584d79bf840ba86f67d4db~tplv-goo7wpa0wc-image.image) </span>

<span id="6c78aee6"></span>
# Task list

The completed tasks created are displayed in the task list, and tasks can be turned on or off. At the same time, you can switch the view (card view/table view) above the list to view the task list, and the search box can search by the task name. The actions that can be performed on a single task are:


* Immediate execution: Manually triggered tasks are executed once, regardless of the current scheduled execution time limit.

* Edit: Enter the task editing page and modify the configuration of task name, execution rules, user instructions, push method, etc.;

* Delete: Delete the current scheduled task, which no longer appears in the task list after deletion, and no longer runs the task. Attention: Deleted tasks cannot be restored, please proceed with caution.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb81dc62bde48ae8094644e3c087cd6~tplv-goo7wpa0wc-image.image) </span>

<span id="1ebf2bc1"></span>
# Run record

Run records are used to centrally view the historical execution of scheduled tasks, helping you track which agent executed each task, at what time, and whether the execution and push were successful. You can quickly locate the target record by task name or account filter, and enter the corresponding conversation task through "View Session" to verify the complete execution process and output content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cf00413002f433e8435aab8b7814f0b~tplv-goo7wpa0wc-image.image) </span>

<span id="05c21a02"></span>
# Use templates to quickly create scheduled tasks

Pre\-made templates are used to help you quickly create common types of scheduled tasks. You can first select a task scenario from the template list, view the template's built\-in instructions and execution rules, and then enter the new task pop\-up window to supplement the personalized configuration, and finally generate a scheduled task that can be automatically run. Here are the steps to create a scheduled task using a template:


1. After entering the scheduled task page, the prefabricated template area is displayed at the top of the page. You can choose the appropriate template according to the task objective.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9739f64f12c44cb2b4d7ff77ba81c04e~tplv-goo7wpa0wc-image.image) </span>

   
   |Prefabricated template type |Scene description |
   |---|---|
   |**Daily briefing** |Automatically read the specified data source every day, generate a complete structure, direct forwarding of daily/weekly/newsletter, and continuously update to the same document or directly output the broadcast body. |
   |**AI Weekly Industry News Brief** |Automatically summarize the most recent week's important developments, representative events, key data changes, and key points of view in a given industry on a weekly basis to generate a well\-structured industry briefing that is easy to read and forward. |
   |**Brand public opinion monitoring** |Automatically generate weekly trending topics, sentiment distributions, and volume trends in major media for brands to identify risks and provide early warnings. |
   |**Daily class A share quotes** |Automatically summarize the latest changes in the three major indices of class A shares every day, important market news and capital flows. |
   

2. After selecting the corresponding template card, the system will open the template details pop\-up window, displaying the name, purpose description and preset command content of the current template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1454da76385f4d2f8c68440e53242e55~tplv-goo7wpa0wc-image.image) </span>

3. After clicking the "+ Create Scheduled Task" button, the system will open the New Scheduled Task pop\-up window and automatically fill in the template name and user instructions. You can adjust the task information based on this.

4. After confirming that the configuration is correct, click the **Save** button to complete the creation; to abandon the configuration, click the **Cancel** button or the Close button in the upper right corner.
