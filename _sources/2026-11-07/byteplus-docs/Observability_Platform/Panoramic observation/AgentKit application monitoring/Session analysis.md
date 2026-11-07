---
title: "Session analysis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Session_analysis"
---

AI application monitoring provides a dedicated session analysis page for AgentKit and its deployed agents. This page tracks the complete interaction between a user and a deployed agent within a specified time period to facilitate troubleshooting. This topic describes how to view session information about AgentKit applications and manage session data.

<span id="lsSnaeZ4"></span>
## Prerequisites

Resources such as runtime have been created on the AgentKit platform, and observability has been enabled. Learn more about creating a [runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

<span id="mgVHnUcJ"></span>
## View session data


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Click **Session analysis**, and select a time range. You can then view the list of all sessions and basic session information within the specified time period.

   Sessions can be filtered by Runtime name, session ID, user ID, duration, and other conditions. From the session list, you can view basic session information, such as Session ID, Duration, Total Tokens, Input Tokens, Output Tokens, Trace Count, User ID, and Start Time.

4. Click the name of the target session or the **Details** button in the Actions column on the right of the target session for details, such as the start time and Input/Output details of each trace, as well as total token count, trace count, trace ID, user ID, and model name.

5. To view the complete request trace and full trace log, click **Trace ID** in the session details to go to the single trace details page.

   On the Single trace details page, after switching to the **LLM data** column in the Details tab in the lower right corner, you can view basic data of the model called in the current trace. For example, input/output data, request operating system, model, type, response model, input cache hit tokens, input tokens, output tokens, and total tokens.

   Select the **LLM** section in the metrics tab at the lower right corner of the single trace details page. Then, view the service related to the specified trace and large language model data. For example, large language model call QPS, large language model call count, token usage, large language model response duration, TTFT, and TPOT monitoring dashboards.


<span id="dcW0fubS"></span>
## Export session data

Session analysis supports exporting both the session list data and the detailed trace data of a specific session.


<Tabs>
<Tab zoneid="Yk5QHdc7pR" title="Export session list data">
<TabTitle>Export session list data</TabTitle>

Go to the session management page. Select the sessions you wish to export, click the **Export ** button in the upper\-right corner of the page, and the basic information data related to the sessions will be exported to a CSV file based on the session list.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">You can export at most 100 records at a time.</div>



</Tab>
<Tab zoneid="qqnH6EKaS8" title="Export session details data">
<TabTitle>Export session details data</TabTitle>

On the session management page, click the target session ID to go to the session details page. Click the **Export** button in the upper\-right corner of the page to export the detailed trace data related to the selected session to a CSV file.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">You can export up to 1000 trace data records at a time.</div>



</Tab>
</Tabs>


<span id="5tqQwHx7"></span>
## Diagnose a session


1. Go to the Session analysis list, click **Session diagnostics** in the Actions column of the target session, and confirm the prompt. You are redirected to the **Observational diagnostics** page, and a session diagnosis task starts automatically.

2. When the task status is "Completed", the diagnosis is complete, and the report is generated. Click **View report** in the Actions column on the right of the target diagnosis task to view the diagnosis report details of the session. For more details, see [Observability diagnosis](https://docs.byteplus.com/en/docs/Observability_Platform/Observability_diagnosis_agentkit).
