---
title: "LLM trace analysis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/LLM_trace_analysis"
---

Trace analysis uses reported span and log data to provide capabilities like trace analysis and single trace search. This facilitates troubleshooting, performance optimization, and system monitoring to improve O&M efficiency. This topic provides a detailed description of how to use LLM trace analysis for general AI application monitoring.

## Background

* Span is the fundamental unit of work in distributed tracing. A span represents a single operation within a system, such as a database query, a function execution, or a remote service call. Each span has a unique identifier with key attributes such as operation name, start time, end time, tags, and logs.

* Trace is a directed acyclic graph composed of multiple spans. A trace represents the complete call chain of a request in a distributed system. Each trace has a globally unique identifier, and all spans belonging to the same request are associated with this trace. The parent\-child relationships between traces and spans help visualize the request's execution path, facilitating distributed tracing.

## Prerequisites

LLM\-related applications have been integrated with AI application monitoring, and observability data is reported normally. Integration methods vary by programming language. For more details, see [Integration methods](https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_AI_application_monitoring).

## Procedure

### Step 1: Filter trace data

1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar.

2. In the left navigation bar, select **Trace Analysis** to go to the LLM trace analysis page.

3. Filter the trace data you need to analyze based on your needs. Multiple filtering methods are currently available.

   > **tip**

   > All filters and rules apply based on AND logic. Only data meeting all conditions will be filtered for analysis.

   * > Six types of filters are supported. Filters apply based on AND logic. Only data meeting all criteria will be returned.

   * > Some filters, such as tag filters and span attribute filters, support multiple filter rules. Multiple filter rules within the same filter apply based on AND logic. This indicates that only data that meets all filter rules will be returned.

   |Serial number |Filter item |Description |
   |---|---|---|
   |1 |Aggregation method |Aggregation method for data displayed in the chart.<br><br><br>* Automatic aggregation: a dynamic aggregation method. The system automatically selects an appropriate aggregation time based on the amount of filtered data.<br><br>* Specified aggregation time: a static aggregation method with data displayed based on the specified aggregation time. The minimum supported interval is 30 seconds, and the maximum is 1 day. |
   |2 |Time range |The time range for data filtering. Data can be refreshed manually or automatically as needed.<br><br><br>* Filter by recent: Filters trace data within the most recent time period based on the current time. For example, filter data from the past hour.<br><br>* Specify time range: Specify a time range to filter trace data within a certain period. For example, filter data from 2025\-11\-08 00:00:00 to 2025\-11\-10 00:00:00. |
   |3 |Filter by tag |You can filter data by tag key\-value pairs. Up to 20 tags can be configured. Multiple tags are applied based on AND logic. This indicates that only data associated with all specified tags will be returned. |
   |4 |workspace |Filters data from the specified workspace. |
   |5 |Keywords in input and output content |Filters data based on keywords in the input and output content. |
   |6 |Span attribute filtering |Filters data based on span attribute key\-value pairs. You can configure multiple span attribute rules. Multiple rules are applied based on AND logic. This indicates that only data matching all specified rules will be returned. |
   |7 |Manage |Click **Manage ** to customize the filter fields displayed in the filter panel. You can also click ** Restore default** to reset the filter fields to the system default configuration. |
   |8 |User feedback |Specifies the display scope for list data.<br><br><br>* Off: Displays all trace data.<br><br>* On: Displays trace data with user feedback. |
   |9 |Other attribute\-based filters |Multiple trace\-associated filter options for granular filtering, such as trace ID, AI span type, service name, model name, operation, and status code. Multiple filters apply based on AND logic. This indicates that only data that matches all filter rules will be returned. |

### Step 2: Analyze trace data

After the data is filtered, you can proceed with data analysis and trace tracking. Currently, span list, performance analysis, and error propagation chain analysis are provided.

**Root Span list**

The root span list section contains all root span\-related traces within the current filtered scope and displays detailed trace information. For example, TraceID, span type, service name, input/output, model name, total tokens, AI span type, start time, duration, service name, operation, and session ID. You can sort the list by Total Tokens, Input Tokens, Output Tokens, start time, or duration to quickly locate errors and slow queries.

> **tip**

> In distributed tracing, a Root Span is the root node of a complete Trace. Each Trace has exactly one Root Span, from which all child Spans originate to form a complete request tracing tree.

**Span list**

Span list mainly displays the trend of trace events and the trace list of the currently filtered data.

#### Trend of span events

It displays the trend of trace events based on the currently filtered data, with a visual and intuitive view of the health status of trace events. This facilitates tasks such as fault troubleshooting, performance evaluation, and capacity planning. For example, a sudden, significant increase in trace events at a specific time may indicate a system activity exception. By correlating this time point with other observability metrics, you can quickly pinpoint the specific service where the issue occurred.

#### Span list

The trace list section contains all traces within the current filtered scope and displays detailed trace information. For example, TraceID, span type, service name, input/output, model name, total tokens, AI span type, start time, duration, service name, operation, and session ID.

* The trace list supports sorting by total tokens, input tokens, output tokens, start time, and duration to quickly locate errors and slow queries. Sorting by total tokens, input tokens, output tokens, and duration is available only for data within a time range not exceeding 24 hours.

* Click the setting button in the upper right corner of the trace list to customize the information to be displayed and the display order.

* Click the refresh button in the upper right corner of the trace list to manually refresh the data in the trace list.

### Step 3: View single trace details

**Trace details**

Click the Trace ID to go to the details page of a single trace. Switch to the Trace details tab to view the complete request trace and detailed span information for fine\-grained data analysis.

|Serial number |Module |Description |
|---|---|---|
|1 |Trace information |Displays details about the current trace, such as trace ID, SESSION ID, start time, total duration, number of applications, number of spans, status code, and the number of user likes/dislikes.<br><br><br>* SESSION ID: The session ID. Click SESSION ID to go to the ** LLM session analysis** page and view details.<br><br>* Like and dislike icons: Display the number of user likes and dislikes for the current trace. Click an icon to go to the **User feedback record** tab and view details. |
|2 |View switch |Three views are provided: list, topology map, and flame graph. You can select the appropriate view as needed to view span details.<br><br><br>* List: Provides comprehensive information that makes filtering and locating spans quick and convenient.<br><br>* Topology map: Displays trace relationships and enables quick identification of key upstream and downstream nodes.<br><br>* Flame graph: Visualizes performance analysis and enables in\-depth analysis of function call relationships. |
|3 |Span filtering |Quick filter configuration. Supported searching features include component labels, LLM component tags, error span viewing, and keyword search. |
|4 |Span view |Span detail view. You can select an appropriate view for fault analysis or performance analysis. |
|5 |Span details |Click the target span to view related details, such as basic information, LLM data, attributes, resources, events and span metrics related to processes, containers, and LLM.<br><br>> **tip**<br><br><br>> LLM data and LLM metrics are displayed only when the service associated with the current distributed tracing contains LLM data.<br> |

**Detailed logs of traces**

Switch to the "Detailed logs of traces" tab to view all service logs associated with the request path during a time period, including both normal and error logs. This helps to pinpoint issues during troubleshooting.

**User feedback record**

Switch to the user feedback record tab to view the feedback summary and details of the current Trace, including the total number of feedback records, likes, and dislikes, as well as the time, record ID, user, feedback result, feedback content, and source of each feedback record.

**AI trace diagnosis**

Click **AI trace diagnosis ** in the upper\-right corner. The intelligent O&M assistant calls the `ai-agent-trace-diagnosis` skill to run an in\-depth diagnostic analysis on the current trace, generate a diagnostic report, and provide a diagnostic conclusion, issue analysis, and repair suggestions. You can refer to the report to fix the issue.

> **tip**

> `ai-agent-trace-diagnosis` is a single\-turn in\-depth diagnostic skill designed for AI agent diagnostic scenarios. For more information about the intelligent O&M assistant, see [Overview of intelligent O&M assistant](https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_Intelligent_Operations_Assistant).

## Other operations

* The **span export** feature is provided for trace lists related to AI applications. You can export span information for other in\-depth analyses. For more details, see [Span export](https://docs.byteplus.com/en/docs/apmplus/Span_export).

* For models involving tool calls, the Input field in the **LLM data** section of the Details tab (in the lower right corner of the single trace details page) displays relevant calling information. Click the dropdown button next to a tool to view its calling details.

* After you locate an abnormal LLM call, if the call has reported parsable data, you can click ** Go to Playground**. The system automatically populates the full context of the call to reproduce the original call scenario. You can modify the prompt or adjust parameters directly in **Playground**, rerun the call, and verify the fix. For more information, see [Playground](https://docs.byteplus.com/en/docs/Observability_Platform/Playground?TagIDs=2,405&lang=en&type=preview).

   > **tip**

   > This entry point is available only for LLM spans.

* For multimodal scenarios, both the Input and Output fields in the **LLM data** section of the Details tab (in the lower right corner of the single trace details page) support the display of Markdown\-formatted text and multimodal content.
