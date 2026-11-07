---
title: "LLM session analysis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/LLM_session_analysis"
---

The AI application monitoring probe supports observability for large language model (LLM) applications. After the self\-developed Python probe is integrated with LLM applications, you can view a list of sessions, session details, and related LLM trace details that meet specific query conditions within a selected time range. This topic describes how to view LLM session analysis and manage session data.

<span id="2W5cSQP9"></span>
## Prerequisites

Your LLM application has been integrated with Server\-side Monitoring, and auto\-instrumentation is enabled. For specific steps, see [Python application integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_Python_applications).

<span id="N2ndKwE7"></span>
## View session details

<span id="nLKPmro0"></span>
### Step 1: Integrate LLM session analysis

Ensure that your LLM application is successfully integrated with Server\-side Monitoring with auto\-instrumentation enabled, and that LLM traces and metrics are automatically generated. Then, pass session analysis metadata (session_id and user_id) from your application code. For example, in Langchain, manually add session_id and user_id to config.metadata when you call a chain/agent. Sample code:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can use any string to identify session_id or user_id. Sessions with the same session_id will be recognized as the same session.</div>


```Python
# Your existing Langchain code to create the chain.
... 

# Pass session_id/user_id as metadata to the chain invocation.
chain.invoke(
    {"animal": "dog"}, # your input
    config={
        "metadata": {
            "session_id": "your-session-id",
            "user_id": "your-user-id",
        },
    },
)
```


<span id="z2InsR9H"></span>
### Step 2: View LLM session data


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **Session Analysis** to go to the LLM session list.

3. To obtain the list of target sessions, filter sessions by workspace, time range, tags, session ID, total tokens, user ID, and other conditions. From the session list, you can view basic session information, such as session ID, duration, total tokens, input tokens, output tokens, trace count, user ID, and start time.

4. Click the name of the target session or the **Details ** button in the Actions column on the right of the target session. You can then view the data of the specified session on the **Session Data** tab, such as the total tokens, number of traces, start time for each trace, input, output, trace ID, user ID, token count, and model name.

5. Click the trace ID to go to the **LLM trace analysis** page to view detailed information about LLM trace analysis. For trace analysis details, see [Trace analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis).


<span id="yLxtiV61"></span>
### Step 3: View insight details

On the **Insight details** tab, you can view the session insight details, including insight time, insight result, evaluation reason, and associated insight tasks. Click the task name to navigate to the task details page and view task information. For details, see [Insight tasks](https://docs.byteplus.com/en/docs/Observability_Platform/renwu?lang=en#IRmlySsa).

<span id="NH9xVx2M"></span>
## Export session data

Session analysis supports exporting both the session list data and the detailed trace data of a specific session.


<Tabs>
<Tab zoneid="HMkwUa6aUH" title="Export session list data">
<TabTitle>Export session list data</TabTitle>

Go to the session management page. Select the sessions you wish to export, click the **Export ** button in the upper\-right corner of the page, and the basic information data related to the sessions will be exported to a CSV file based on the session list.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">You can export at most 100 records at a time.</div>



</Tab>
<Tab zoneid="CJfuvId0h6" title="Export session details data">
<TabTitle>Export session details data</TabTitle>

On the session management page, click the target session ID to go to the session details page. Click the **Export** button in the upper\-right corner of the page to export the detailed trace data related to the selected session to a CSV file.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">You can export up to 1000 trace data records at a time.</div>



</Tab>
</Tabs>


<span id="TBVu5yii"></span>
## Diagnose a session

Trace and Session data of the current session can be temporarily used for diagnosis and analysis, and detailed diagnosis reports are provided.


1. Go to the Session analysis list, click **Session diagnostics** in the Actions column of the target session, and confirm the prompt. You are redirected to the **Observational diagnostics** page, and a session diagnosis task starts automatically.

2. When the task status is "Completed", the diagnosis is complete, and the report is generated. Click **View report** in the Actions column on the right of the target diagnosis task to view the diagnosis report details of the session. For more details, see [Observability diagnosis](https://docs.byteplus.com/en/docs/Observability_Platform/Observability_diagnosis).
