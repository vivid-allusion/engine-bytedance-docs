---
title: "Runtime overview"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Runtime_overview"
---

AI application monitoring provides comprehensive observability support for agents deployed on AgentKit, such as automatic trace data collection, automatic metric generation, trace analysis, and log search. This enables real\-time observability into agent performance and reliability. This topic provides a detailed description of how to view runtime monitoring and related analysis data.

<span id="96qPJZzk"></span>
## Background

AgentKit Runtime provides agents with a secure, isolated, managed runtime environment that is framework\- and model\-agnostic. It supports automatic scaling of associated session instances based on business traffic, and supports built\-in IAM roles to control agent runtime access permissions to cloud resources. For more details, refer to [Runtime overview](https://docs.byteplus.com/en/docs/agentkit/Agent_runtime_overview).

<span id="28rnZq9I"></span>
## Prerequisites

An agent runtime has been created in AgentKit, and observability has been enabled. For details, refer to [Creating agent runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

<span id="gMpDmAoX"></span>
## Procedure


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Click **Runtime overview**, and select a time range. You can then view an overview of all runtimes within the specified time period. The runtime overview and runtime list are displayed. In addition to basic data statistics, visualized monitoring dashboards for session count, call count, and error rate are also provided, making it easy for users to assess data health or locate issues.



|Metric |Descriptions |
|---|---|
|Runtime count |Total number of runtimes created in AgentKit. A runtime list is provided, which allows you to view detailed information about runtimes. |
|Session count |Total number of sessions with calls within the specified time period. A monitoring data dashboard is provided for user convenience. |
|Token consumption |Total token consumption during large language model calls within the specified time period, including both input and output token counts.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">AI application monitoring supports tracking agent data related to large language model calls. When an agent calls a large language model, relevant data is observed. For more details, refer to <a href="https://docs.byteplus.com/en/docs/Observability_Platform/Model_monitoring">Model monitoring</a>.</div><br> |
|Call count |Total call count across all runtime instances within the specified time period. A monitoring data dashboard is provided for user convenience. |
|Error count |Total number of failed requests within the specified time period. |
|Error rate |The proportion of failed requests to total call count within the specified time period. Error rate = error count / call count. A monitoring data dashboard is provided for user convenience. |



4. Click the name of the target runtime or the **Monitoring details** button in the Actions column on the right of the target runtime. Then, switch to the **Runtime overview** tab to view the overview and trend dashboards of the current runtime within the specified time. This helps users assess the health status of individual runtimes.



|Metric |Descriptions |
|---|---|
|Session count |Displays the total number of sessions created by the current runtime instance within the specified time period. |
|Token consumption |Displays the total token consumption for large language model calls by the current runtime instance within the specified time period, including both input and output token counts. |
|Call count |Displays the call count of the current runtime instance within the specified time period. |
|Error count |Displays the total number of failed requests for the current runtime instance within the specified time period. A monitoring data dashboard is provided for user convenience. |
|Error rate |Displays the proportion of failed requests to total calls for the current runtime instance within the specified time period. Error rate = error count / call count. |



5. Switch to the **Runtime monitoring** tab to view resource consumption of the current runtime within the specified time.



|Metric |Descriptions |
|---|---|
|CPU time |Indicates the CPU time consumed by the current runtime instance at a specific moment within the specified time period. It includes user\-mode CPU time and kernel\-mode CPU time. CPU time is a direct indicator of the execution efficiency of the current runtime. |
|CPU utilization |Indicates the total CPU usage rate of the current runtime instance at a specific moment within the specified time period. If the current runtime is using multiple CPU cores simultaneously, the final result may exceed 100%. |
|Memory usage |Indicates the memory usage of the current runtime instance at a specific moment within the specified time period, including: RSS memory (Resident Set Size) and VMS memory (Virtual Memory Size). Trends in memory usage can help detect memory allocations and identify memory leaks. |
|Number of GC objects |Indicates the number of new GC objects added to each generation (0/1/2) of the current runtime instance at a specific moment within the specified time period (counted since the last garbage collection) **.**  You can analyze this metric together with memory data to assess system stability and prevent system crashes. |
|Number of threads |Indicates the number of threads of the current runtime instance at a specific moment within the specified time period. The thread count trend can be used to identify thread resource bottlenecks and optimize thread concurrency. |
|Number of context switches |Indicates the number of context switches for the current runtime instance at a specific moment within the specified time period, including voluntary and involuntary switches. You can use this metric together with CPU usage data to assess the runtime performance of the system, optimize thread scheduling, or perform other optimizations. |



6. Switch to the **Session analysis** tab to view the list of sessions associated with the current runtime and basic session information within the specified time.


Sessions can be filtered by Runtime name, session ID, user ID, duration, and other conditions. From the session list, you can view basic session information, such as Session ID, Duration, Total Tokens, Input Tokens, Output Tokens, Trace Count, User ID, and Start Time.

Click the name of the target session or the **Details** button in the Actions column on the right of the target session for details, such as the start time and Input/Output details of each trace, as well as total token count, trace count, trace ID, user ID, and model name.


7. Switch back to the **Trace analysis** tab in the runtime details to view detailed information about traces associated with the current runtime within the specified time period. Information includes Span list, performance analysis, and error propagation analysis. For more detailed information, refer to [Trace analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Trace_analysis).

* **Span list**: Displays the trace list and trend of trace events related to the current runtime. You can filter data by span attributes, trace ID, model name, span type, AI span type, interface name, and other dimensions. You can sort by Total Tokens, Input Tokens, Output Tokens, start time, and duration to quickly locate errors and slow queries.

* **Performance analysis**: Displays the list of aggregated traces of service interfaces that meet the filtering conditions within a specified time period. With collected duration\-related data of each node in the traces, the duration distribution is visually displayed with the trace duration list provided, helping users quickly locate performance bottlenecks. To obtain performance analysis data, specify filters properly—at least the span type, runtime name, and interface name.

* **Error propagation analysis**: Displays the list of aggregated traces of service interfaces that meet the filtering conditions within a specified time period. With obtained possible sources of propagation for error nodes and impacts on upstream and downstream nodes, error impact analysis and source analysis are visually displayed, helping users quickly analyze error propagation paths. To obtain performance analysis data, specify filters properly—at least the span type, runtime name, and interface name.


To view the complete request trace and full trace log, click the target trace ID in the span list or **Trace ID** in the session details to go to the Single trace details page.

On the Single trace details page, after switching to the **LLM data** column in the Details tab in the lower right corner, you can view basic data of the model called in the current trace. For example, Input/Output data, Request operating system, model, type, response model, Input cache hit tokens, Input Tokens, Output Tokens, and total Tokens.

Select the **LLM** section in the metrics tab at the lower right corner of the single trace details page. Then, view the service related to the specified trace and large language model data. For example, large language model call QPS, large language model call count, token usage, large language model response duration, TTFT, and TPOT monitoring dashboards.


8. Switch to the **Log analysis** tab in the runtime details to view logs of the current runtime during the specified time period, including runtime logs and runtime build logs.

* **Runtime logs**: Logs generated during the runtime process, used for troubleshooting and behavior tracing during runtime. Token\-based search and data filtering by runtime name, log level, and trace ID are supported.

* **Runtime build logs**: Logs generated during the runtime build process via the continuous delivery pipeline, used for troubleshooting and behavior tracing during the build process.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Detailed runtime build logs are generated only when the runtime is created via the AgentKit command\-line tool. Otherwise, the log content is empty.</div>
