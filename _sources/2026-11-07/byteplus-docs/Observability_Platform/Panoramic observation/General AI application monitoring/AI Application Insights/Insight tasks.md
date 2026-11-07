---
title: "Insight tasks"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/renwu"
---

An insight task can be used for batch analysis on historical sessions within a specified range based on the specified insight rule. For each session, the task generates a tag and an evaluation rationale. By creating an insight task, you can filter a large number of sessions to identify the data that requires attention. You can also view the overall distribution of results and locate issues based on the original sessions. The analysis results provide a basis for optimizing system prompts, tool calls, or product workflows. This topic describes how to manage insight tasks.

<span id="M4VsZINd"></span>
## Limits


* You have view permissions on the target workspace. For details, see[ Workspace-level IAM permission control](https://docs.byteplus.com/en/docs/apmplus/Workspace-level_IAM_permission_control).

* The target workspace contains historical session data of AI applications. For details about how to integrate and query session data, see[ LLM session analysis](https://docs.byteplus.com/en/docs/Observability_Platform/LLM_session_analysis#nLKPmro0).


<span id="OMYw9UaJ"></span>
## Create an insight task


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation pane, select **AI Application Insights** \> **Insight task**.

3. In the upper\-right corner of the page, select the target workspace. An insight task can only be used to analyze the session data in the selected workspace.

4. Click "**Create insight task**" and then configure the parameters.

   
   |Parameters |Description |
   |---|---|
   |Task name |Enter a custom name for the insight task. Duplicate names are not allowed within the same workspace. |
   |Associated insight rules |Select the insight rule used by the current task. For details, see[ Insight rules](https://docs.byteplus.com/en/docs/Observability_Platform/guize). |
   |Analysis time range |Select the time range in which the sessions were generated. The system analyzes only the sessions within the specified time range. You can select "Last 1 day", "Last 7 days", "Last 14 days", "Last 30 days", or a custom time range. |
   |Agent Service |Select the agent services that you want the current task to analyze. If you do not specify a service, the task analyzes all agent services within the workspace by default. |
   |Data filtering |Click **Add Filter** to further narrow down the data to be analyzed within the analysis time range and the Agent service scope. You can configure fields such as session ID, user ID, session duration, and trace count.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If you do not add any filter criteria, the system analyzes all eligible sessions within the analysis time range.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you add multiple filter criteria, the criteria are combined with a logical AND. That is, only the sessions that meet all the specified criteria are included in the analysis.</div><br> |
   


<span id="2UinskVH"></span>
## View an insight task


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation pane, select **AI Application Insights** \> **Insight task**.

3. In the upper\-right corner of the page, select the target workspace. The system displays all insight tasks in the workspace.

4. In the task list, click the name of the target task, or click **Details** in the Actions column to view the basic information about the task.

5. The task result overview page displays the number and percentage of each tag in the current task. Click **View Rule Configuration** to view the insight rule associated with the task. For details, see[ Insight rules](https://docs.byteplus.com/en/docs/Observability_Platform/guize?lang=en).

   
   <Tabs>
   <Tab zoneid="sSBa6zFCgJ" title="Task result details">
   <TabTitle>Task result details</TabTitle>
   
   Click the **Task result details** tab to view the analysis results of the task. This tab consists of a filter section and a result details section.
   
   
   * In the filter section, you can filter sessions based on the following criteria:
   
      * Status: Filter sessions by the analysis status.
   
      * Rule name: Filter sessions by the insight rule associated with the current task.
   
      * Filter by Session ID: Enter the complete session ID to locate the analysis result of a specific session.
   
   * The result details section displays the analysis records for each session:
   
      * Creation time: The time when the insight result was generated. This information helps you confirm whether the result comes from the target analysis period. It also helps you distinguish between results that are generated for the same session by different tasks or at different times.
   
      * Session ID: The ID of the session. Click the session ID to go to the **LLM session analysis** page, where you can view the complete conversation, trace, and related context. For details, see [LLM session analysis](https://docs.byteplus.com/en/docs/Observability_Platform/LLM_session_analysis?lang=en).
   
      * Tag attribute: The classification result output by the rule. Use this result to determine the extent to which user needs are met in a complete session.
   
      * Evaluation rationale: The explanation that the large language model provides for the current tag. This explanation describes which parts of the conversation affected the satisfaction assessment.
   
   
   </Tab>
   <Tab zoneid="opQsCiHUZY" title="Associated insight rules">
   <TabTitle>Associated insight rules</TabTitle>
   
   Click the **Associated insight rules** tab to view information about the insight rule used by the current task, including the rule name, rule ID, version, output type, and description. On this tab, you can check the evaluation criteria on which the current analysis is based.
   
   
   
   
   </Tab>
   <Tab zoneid="FTRjLDB4Ho" title="Execution details">
   <TabTitle>Execution details</TabTitle>
   
   Click the **Execution details** tab to view the execution records of the task, including the execution round, the number of records, the start time, the end time, and the status.
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="gxeM1LPP"></span>
## Delete an insight task

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleted tasks cannot be recovered. Proceed with caution.</div>



1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation pane, select **AI Application Insights** \> **Insight task**.

3. In the upper\-right corner of the page, select the target workspace. The system displays all insight tasks in the workspace.

4. Click **Delete** in the Actions column of the target insight task to delete the task.
