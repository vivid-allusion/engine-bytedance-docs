---
title: "Knowledge base analysis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Knowledge_base_analysis"
---

AI application monitoring supports monitoring API call count, average latency, total error rate, and other detection data. This feature can be used to optimize resources, maintain system stability, enhance user experience, and support business decision\-making. This topic provides a detailed description of how to view knowledge base analysis data.

<span id="SPPtVGwh"></span>
## Background

AgentKit Knowledge supports one\-click configuration and import capabilities for mainstream knowledge bases (for example, Viking knowledge base). This allows you to associate an agent with knowledge bases and deploy it on the AgentKit platform. For more details, refer to [Knowledge base overview](https://docs.byteplus.com/en/docs/agentkit/Knowledge_base_overview).

<span id="xrtWmuL2"></span>
## Prerequisites

A knowledge base has been imported into AgentKit and used for knowledge retrieval or knowledge Q&A. For more details, refer to [Managing knowledge bases](https://docs.byteplus.com/en/docs/agentkit/Managing_knowledge_bases).

<span id="6LTazRcM"></span>
## Procedure


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Click **Knowledge base analysis**, and select a time range. You can then view the knowledge retrieval data and knowledge base list for the specified period.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only data generated through SDK calls is used for knowledge base analysis. Data from non\-AgentKit runtime calls and direct API calls is excluded.</div>



|Metric |Descriptions |
|---|---|
|API call count |Total number of knowledge base operations called via the SDK within a specified time period. |
|Average latency |Average response time for knowledge base operations called via the SDK within a specified time period. |
|Total error rate |Error rate for knowledge base operations called via the SDK within a specified time period. Total error rate = number of operations with errors / total number of operations. |



4. Click the name of the target knowledge base or **Monitoring details** in the Actions column on the right to view the knowledge base details. Then, select the **Trace analysis** tab to view trace details related to the target knowledge base for the specified period.

   You can then view the related trace list and trend of trace events, and filter data by span attributes, trace ID, model name, span type, AI span type, interface name, and other dimensions. You can sort by total tokens, input tokens, output tokens, start time, and duration to quickly locate errors and slow queries. For more details, refer to [Trace analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Trace_analysis).

5. Click the ID of the target trace to go to the single trace details page. You can then view the complete request trace and full trace logs related to the knowledge base. On the Single trace details page, after switching to the **LLM data** column in the Details tab in the lower right corner, you can view basic data of the model called in the current trace. For example, input/output data, request operating system, model, type, response model, input cache hit tokens, input tokens, output tokens, and total tokens.



&nbsp;

Select the **LLM** section in the metrics tab at the lower right corner of the single trace details page. Then, view the service related to the specified trace and large language model data. For example, large language model call QPS, large language model call count, token usage, large language model response duration, TTFT, and TPOT monitoring dashboards.
