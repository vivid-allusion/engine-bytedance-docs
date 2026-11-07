---
title: "Trace analysis"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Trace_analysis"
---

Trace analysis uses reported span and log data to provide capabilities like trace analysis and single trace search. This facilitates troubleshooting, performance optimization, and system monitoring to improve O&M efficiency. This topic describes how to use trace analysis.

## Background

* Span is the fundamental unit of work in distributed tracing. A span represents a single operation within a system, such as a database query, a function execution, or a remote service call. Each span has a unique identifier with key attributes such as operation name, start time, end time, tags, and logs.

* Trace is a directed acyclic graph composed of multiple spans. A trace represents the complete call chain of a request in a distributed system. Each trace has a globally unique identifier, and all spans belonging to the same request are associated with this trace. The parent\-child relationships between traces and spans help visualize the request's execution path, facilitating distributed tracing.

## Prerequisites

Your application has been integrated with Server\-side Monitoring and is reporting observability data normally. The integration method varies by programming language. For more details, see the [integration guide](https://docs.byteplus.com/en/docs/apmplus/Integration_guide).

## Limits

To view performance or error propagation chain analysis, specify at least the span type, service name, and interface name to retrieve analysis data.

## Procedure

### Step 1: Filter trace data

1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). In the top navigation bar, select the target project and region.

2. Click **Click to go to service list** to go to the Service management page.

3. In the left navigation pane, select **Service Monitoring \> Trace Analysis** to go to the Trace Analysis page.

4. Filter the trace data you need to analyze based on your needs. Multiple filtering methods are currently available.

> **tip**

> All filters and rules apply based on AND logic. Only data meeting all conditions will be filtered for analysis.

* > Six types of filters are supported. Filters apply based on AND logic. Only data meeting all criteria will be returned.

* > Some filters, such as tag filters and span attribute filters, support multiple filter rules. Multiple filter rules within the same filter apply based on AND logic. This indicates that only data that meets all filter rules will be returned.

|Serial number |Filter item |Description |
|---|---|---|
|1 |workspace |Filters data from the specified workspace. |
|2 |Aggregation method |Aggregation method for data displayed in the chart.<br><br><br>* Automatic aggregation: a dynamic aggregation method. The system automatically selects an appropriate aggregation time based on the amount of filtered data.<br><br>* Specified aggregation time: a static aggregation method with data displayed based on the specified aggregation time. The minimum supported interval is 30 seconds, and the maximum is 1 day. |
|3 |Time range |The time range for data filtering. Data can be refreshed manually or automatically as needed.<br><br><br>* Filter by recent: Filters trace data within the most recent time period based on the current time. For example, filter data from the past hour.<br><br>* Specify time range: Specify a time range to filter trace data within a certain period. For example, filter data from 2025\-11\-08 00:00:00 to 2025\-11\-10 00:00:00. |
|4 |Filter by tag |You can filter data by tag key\-value pairs. Up to 20 tags can be configured. Multiple tags are applied based on AND logic. This indicates that only data associated with all specified tags will be returned. |
|5 |Span attribute filtering |Filters data based on span attribute key\-value pairs. You can configure multiple span attribute rules. Multiple rules are applied based on AND logic. This indicates that only data matching all specified rules will be returned. |
|6 |Manage |Click **Manage** to customize the filter fields displayed in the filter panel. You can also click **Restore default** to reset the filter fields to the system default configuration. |
|7 |Other attribute\-based filters |Associated trace filter options such as trace ID, span type, service name, and interface name. They are used for fine\-grained filtering. Multiple filters apply based on AND logic. This indicates that only data that matches all filter rules will be returned. |

### Step 2: Analyze trace data

After the data is filtered, you can proceed with data analysis and trace tracking. Currently, span list, performance analysis, and error propagation chain analysis are provided.

**Root Span list**

The root span list displays all root span\-related traces within the current filter scope along with detailed trace information, such as trace ID, status code, start time, duration, service name, interface name, and operation. Additionally, the root span supports sorting by start time and duration, enabling you to quickly locate errors and slow queries.

> **tip**

> In distributed tracing, a Root Span is the root node of a complete Trace. Each Trace has exactly one Root Span, from which all child Spans originate to form a complete request tracing tree.

**Span list**

Span list mainly displays the trend of trace events and the trace list of the currently filtered data.

#### Trend of span events

It displays the trend of trace events based on the currently filtered data, with a visual and intuitive view of the health status of trace events. This facilitates tasks such as fault troubleshooting, performance evaluation, and capacity planning. For example, a sudden, significant increase in trace events at a specific time may indicate a system activity exception. By correlating this time point with other observability metrics, you can quickly pinpoint the specific service where the issue occurred.

#### Span list

The trace list displays all traces within the current filter scope along with detailed information, such as trace ID, status code, start time, duration, service name, interface name, operation, downstream service type, downstream service name, and service type.

* The trace list supports sorting by start time and duration, enabling you to quickly locate errors and slow queries. Note that duration\-based sorting is only supported for data with a time span not exceeding 24 hours.

* Click the setting button in the upper right corner of the trace list to customize the information to be displayed and the display order.

* Click the refresh button in the upper right corner of the trace list to manually refresh the data in the trace list.

**Performance analysis**

On the performance analysis page, you can view the list of aggregated traces of service interfaces that meet the filtering conditions within a specified time period. With the collected duration\-related data of each node in the traces, the duration distribution is visually displayed with the trace duration list provided, helping users quickly locate performance bottlenecks.

> **tip**

* > To obtain performance analysis data, specify filters properly—at least the span type, service name, and interface name.

* > A maximum of 200 error traces from the current filtered result can be used for performance analysis.

#### Time consumption distribution

This chart provides a visual representation of time consumption distribution, helping you quickly identify the number of spans and view sample lists within different latency ranges. How it works: The spans filtered by the query conditions on the left are sorted by duration and then evenly divided into 50 buckets (represented as bars). Each bar is associated with up to 5 sample spans.

Click a bar in the chart to pop up the corresponding sample list. Click **View traces** in the Actions column on the right side of the sample list to view the details of a single trace.

#### Trace latency list

This list presents the results of an aggregated analysis on traces that meet the filter criteria. In this analysis, the root node refers to a span meeting the query conditions, and the other nodes are its downstream nodes. The aggregated results include the following fields:

|**Field** |**Field description** |**Example** |
|---|---|---|
|Trace |`{Service name}::{Interface name}`. If the current node only has a ServerSpan, use the service name and interface name of the ServerSpan. If the node has both ClientSpan and ServerSpan, use the service name and interface name of the ServerSpan. If the node only has a ClientSpan, directly use the downstream service name and interface name. |server_b::/resource_bb<br><br> |
|Span count/request multiplier |Span count indicates the number of spans in all traces. Trace count indicates the number of traces that contain the current span.<br><br>Request multiplier = Span count / trace count. |256 / 135.45% |
|Request count / request ratio |Request count indicates the number of traces that contain the current span among all traces.<br><br>Request ratio = request count / root node request count. |189 / 100.00% |
|Error request count / error request ratio |Error request count indicates the number of traces that contain the current span and where the span status is error.<br><br>Error request ratio = error request count / root node request count. |0 / 0.00% |
|Time consumption |Indicates the average duration for the current node across multiple traces. If a node is called multiple times by upstream nodes, the total time occupied is used. |1.40s |
|Maximum subtree size |Maximum subtree size indicates the maximum number of descendant nodes in all traces. Descendant node count indicates the total number of all descendant nodes (counting only Client and Server Spans) for this node in a single trace. |20 |
|Average network call latency |Average network call latency = client span latency of upstream calls to the current node \- local server span latency of the current node. |646.70μs |
|Average local latency |Average local net duration = Duration of this node's Server Span \- Total duration of all its downstream Client Spans. |72.79μs |
|Flag |Indicates: Excessive descendant nodes: Applies when a node's descendant node count exceeds the threshold (\>50). Repeated calls: Applies when the call multiplier is above the threshold (\>5). |Repeat call |

Click **view Span** in the Actions column on the right side of the trace latency list to view span samples. Click **View traces** in the Actions column on the right side of the sample list to view the details of a single trace.

**Error propagation chain analysis**

On the error propagation chain analysis page, you can view the list of aggregated traces of service interfaces that meet the filtering conditions within a specified time period. With the obtained possible sources of propagation for error nodes and impacts on upstream and downstream nodes, error impact analysis and source analysis are visually displayed, helping users quickly analyze error propagation paths.

> **tip**

* > To obtain performance analysis data, specify filters properly—at least the span type, service name, interface name, and status code. The span type is fixed to the server type, and the status code is fixed to the error code (excluding 0 and 200).

* > A maximum of 200 error traces from the current filtered result can be used for error propagation chain analysis.

#### Error impact analysis

This feature is used to analyze which upstream nodes the error of the currently analyzed node propagates to, the specific propagation path, and the impact level. For example, errors in the `/java_service_d/http` interface of `java_server_d` propagated to its upstream node `java_server_b`, with a propagation ratio of 100%. The aggregated analysis result includes the following fields:

|**Field** |**Field description** |**Example** |
|---|---|---|
|Trace |The displayed name varies by span type. For the server type, the name is `{service name}::{interface name}`. For the client type, it is `{service name}->{downstream service name}::{interface name}`. For the common type, it is `{service name}::{operation name}`. |java_server_d::/java_service_d/http |
|Call count |The total number of times this node occurs in the analyzed error traces.<br><br> |200 |
|Error count |The total number of errors occurring on the current node in the analyzed error traces. |200 |
|Error rate |Error rate = error count / call count. |100% |
|Propagation ratio |The error propagation ratio of the current node in the error traces. Propagation ratio = error count of this node / total error trace count. |10.00% |
|Error details |Displays examples of error types that occurred at the current node in all traces. Click **More** in the Actions column on the right to go to the error details page. Click the target trace in the Actions column on the right side of the error details to view its details. |java.lang.RuntimeException<br><br> |

#### Error source analysis

This feature is used to analyze the key downstream error sources, error propagation chains, and the error contribution ratio of each node for the currently analyzed node. For example, errors in the `/java_service_d/http` interface of the `java_server_d `service were caused by the `spring.controller` interface (a downstream node within the same `java_server_d` service), with a 100% contribution rate. The aggregated analysis result includes the following fields:

|Field |Field description |Example |
|---|---|---|
|Trace |The displayed name varies by span type. For the server type, the name is `{service name}::{interface name}`. For the client type, it is `{service name}->{downstream service name}::{interface name}`. For the common type, it is `{service name}::{operation name}`. |server_b::/resource_bb<br><br> |
|Call count |The total number of times this node occurs in the analyzed error traces.<br><br> |200 |
|Error count |The total number of errors occurring on the current node in the analyzed error traces. |200 |
|Error rate |Error rate = error count / call count. |100% |
|Contribution rate |The error contribution ratio of the current node in error traces. Calculation formula: error count of the current node / total number of error traces. |10.00% |
|Error details |Displays examples of error types that occurred at the current node in all traces. Click **More** in the Actions column on the right to go to the error details page. Click the target trace in the Actions column on the right side of the error details to view its details. |java.lang.RuntimeException<br><br> |

### Step 3: View single trace details

**Trace details**

Click the target trace ID to go to the details page of a single trace. Switch to the Trace details tab to view the complete request trace and detailed span information for fine\-grained data analysis.

|Serial number |Module |Description |
|---|---|---|
|1 |Trace information |Displays details about the current trace, such as trace ID, start time, total duration, number of applications, and number of spans. |
|2 |View switch |Three views are provided: list, topology map, and flame graph. You can select the appropriate view as needed to view span details.<br><br><br>* List: Provides comprehensive information that makes filtering and locating spans quick and convenient.<br><br>* Topology map: Displays trace relationships and enables quick identification of key upstream and downstream nodes.<br><br>* Flame graph: Visualizes performance analysis and enables in\-depth analysis of function call relationships. |
|3 |Span filtering |Quick filter options. Three quick search options are available: Component label, View error Span, and keyword search. |
|4 |Span view |Span detail view. You can select an appropriate view for fault analysis or performance analysis. |
|5 |Span details |Click the target span to view its details, including basic information, attributes, resources, events, and other span information, as well as metric details related to processes, containers, and more. |

**Detailed logs of traces**

Switch to the "Detailed logs of traces" tab to view all service logs associated with the request path during a time period, including both normal and error logs. This helps to pinpoint issues during troubleshooting.

**AI trace diagnosis**

Click **AI trace diagnosis** in the upper\-right corner. The intelligent O&M assistant calls the `ai-agent-trace-diagnosis` skill to run an in\-depth diagnostic analysis on the current trace, generate a diagnostic report, and provide a diagnostic conclusion, issue analysis, and repair suggestions. You can refer to the report to fix the issue.

> **tip**

> `ai-agent-trace-diagnosis` is a single\-turn in\-depth diagnostic skill designed for AI agent diagnostic scenarios. For more information about the intelligent O&M assistant, see [Overview of intelligent O&M assistant](https://docs.byteplus.com/en/docs/observability/Overview_of_Intelligent_Operations_Assistant).

## What to do next

The **span export** feature is provided for trace lists related to AI applications. You can export span information for other in\-depth analyses. For more details, see [Span export](https://docs.byteplus.com/en/docs/apmplus/Span_export).
