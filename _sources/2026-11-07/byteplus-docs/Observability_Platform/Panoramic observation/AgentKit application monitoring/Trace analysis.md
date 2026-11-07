---
title: "Trace analysis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Trace_analysis"
---

AI application monitoring provides a dedicated trace analysis page for AgentKit and its deployed agents. This page is used to track the full call chain of agent applications, facilitating query of call relationships and analysis of trace\-related issues. This topic provides a detailed description of how to view trace information related to AgentKit applications.

## Prerequisites

Resources such as runtime, memory, and knowledge base have been created on the AgentKit platform, and observability has been enabled. Learn more about [creating a runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console) or [memory](https://docs.byteplus.com/en/docs/agentkit/Creating_memories) and [importing a knowledge base](https://docs.byteplus.com/en/docs/agentkit/Managing_knowledge_bases).

## Procedure

1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar.

2. In the left navigation bar, select **AgentKit Application Observability**.

3. Click **Trace Analysis**, and select a time range. You can then view the list of all traces and basic trace information within the specified time period.

4. Switch to the **Root Span List** or **Spans** tab to view the Span list and the trend of Span events. Data can be filtered by span attributes, trace ID, model name, span type, AI span type, interface name, and other dimensions. You can sort by total tokens, input tokens, output tokens, start time, and duration. For more details, see [Trace analysis](https://docs.byteplus.com/en/docs/Observability_Platform/LLM_trace_analysis).

   > **tip**

   * > In distributed tracing, a Root Span is the root node of a complete Trace. Each Trace has exactly one Root Span, from which all child Spans originate to form a complete request tracing tree.

   * > Click**Manage**to customize the filter fields displayed in the filter panel. You can also click **Restore default** to reset the filter fields to the system default configuration.

   Click the target Trace ID in the Root Span List or Spans to navigate to the single trace details page. Then, you can view the complete request trace and full Trace log.

   **Trace details**

On the "Trace details" tab, find the ** LLM data column** in the Details tab in the lower\-right corner to view basic data of the model called in the current trace. For example, input/output data, request operating system, model, type, response model, input cache hit tokens, input tokens, output tokens, and total tokens.

   Navigate to the **LLM** section in the metrics tab at the lower right corner of the single trace details page. Then, view the service related to the specified trace and large language model data. For example, large language model call QPS, large language model call count, token usage, large language model response duration, TTFT, and TPOT monitoring dashboards.

   **Detailed logs of traces**

Switch to the "Detailed logs of traces" tab to view all service logs associated with the request path during a time period, including both normal and error logs. This helps to pinpoint issues during troubleshooting.

   **User feedback record**

Switch to the user feedback record tab to view the feedback summary and details of the current Trace, including the total number of feedback records, likes, and dislikes, as well as the time, record ID, user, feedback result, feedback content, and source of each feedback record.

   **AI trace diagnosis**

Click ** AI trace diagnosis** in the upper\-right corner. The intelligent O&M assistant calls the `ai-agent-trace-diagnosis `skill to run an in\-depth diagnostic analysis on the current trace, generate a diagnostic report, and provide a diagnostic conclusion, issue analysis, and repair suggestions. You can refer to the report to fix the issue.

   > **tip**

   > `ai-agent-trace-diagnosis` is a single\-turn in\-depth diagnostic skill designed for AI agent diagnostic scenarios. For more information about the intelligent O&M assistant, see [Overview of intelligent O&M assistant](https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_Intelligent_Operations_Assistant).

## Other operations

* **Span export** for AgentKit\-related traces is supported. Check the target information and click the **Span export** button on the right side of the Span list to export Span information for further in\-depth analysis.**** Currently, two export destinations are supported: local files and the CozeLoop evaluation dataset. For more details, refer to [Span export](https://docs.byteplus.com/en/docs/apmplus/Span_export).

* For models involving tool calls, the Input field in the **LLM data** section of the Details tab (in the lower right corner of the single trace details page) displays relevant calling information. Click the dropdown button next to a tool to view its calling details.

* For multimodal scenarios, both the Input and Output fields in the **LLM data** section of the Details tab (in the lower right corner of the single trace details page) support the display of Markdown\-formatted text and multimodal content.
