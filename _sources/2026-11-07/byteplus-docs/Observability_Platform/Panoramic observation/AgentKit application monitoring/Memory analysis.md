---
title: "Memory analysis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Memory_analysis"
---

AI application monitoring supports tracking key metrics, traces, logs, and time periods related to agent\-associated memories. This feature can be used to monitor memory resource performance, accuracy, retrieval effectiveness, and reliability in real time. This topic provides a detailed description of how to view memory analysis data.

<span id="4Y1YOTiE"></span>
## Background

The memory feature of AgentKit provides enterprise\-grade long\-term memory management capabilities for agents. Based on connected mainstream memory frameworks (such as VikingDB) via unified interfaces, agents can achieve cross\-session context awareness, personalized interaction, and continuous learning and evolution. For more details, refer to [Memory overview](https://docs.byteplus.com/en/docs/agentkit/Memory_overview).

<span id="wEH346at"></span>
## Prerequisites

A memory has been created in AgentKit and called in agents. Currently, two memory types are supported: VikingDB. 

<span id="rc82fJ2S"></span>
## Procedure


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Click **Memory analysis**, and select a time period. You can then view the summary of memory data and the memory list within the specified period.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only data generated through SDK calls is used for memory analysis. Data from non\-AgentKit runtime calls and direct API calls is excluded.</div>



|Metric |Descriptions |
|---|---|
|API call count |Total number of memory operations called via the SDK within a specified time period. |
|Average latency |Average response time for memory operations called via the SDK within a specified time period. |
|Total error rate |Error rate for memory operations called via the SDK within a specified time period. Total error rate = number of operations with errors / total number of operations. |



4. Click the name of the target memory or the **Monitoring details** button in the Actions column on the right to view the memory details. Then, select the **Trace analysis** tab to view trace details related to the target memory for the specified period. You can then view the related trace list and trend of trace events, and filter data by span attributes, trace ID, model name, span type, AI span type, interface name, and other dimensions. You can sort by total tokens, input tokens, output tokens, start time, and duration to quickly locate errors and slow queries. For more details, refer to [Trace analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Trace_analysis).

5. To view the complete request trace and full trace log related to the memory, click the target trace ID or **Trace ID** in the session details to go to the Single trace details page.

   On the Single trace details page, after switching to the **LLM data** column in the Details tab in the lower right corner, you can view basic data of the model called in the current trace. For example, input and output data, request operating system, model, type, response model, input cache hit tokens, input tokens, output tokens, and total tokens.

   Select the **LLM** section in the metrics tab at the lower right corner of the single trace details page. Then, view the service related to the specified trace and large language model data. For example, large language model call QPS, large language model call count, token usage, large language model response duration, TTFT, and TPOT monitoring dashboards.
