---
title: "Viewing ArkClaw traces"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_traces"
---

The platform provides a separate ArkClaw trace analysis page for tracking full traces. This facilitates querying invocation relationships and diagnosing trace\-related issues. This topic describes how to view ArkClaw traces in detail.

<span id="7XO9r3IK"></span>
## Background information


* A span is ‌a unit of work in distributed tracing that represents an operation executed within the system, such as a database query, function execution, or remote service call. Each span has a unique identifier and carries some essential attributes, such as operation name, start time, end time, tag, and log.

* A trace is a directed acyclic graph composed of multiple spans that represents the complete path a request takes in a distributed system. A trace has a globally unique identifier, and all spans of the same request are associated with this trace. The parent\-child relationship between traces and spans helps clarify the execution chain of requests in the system and facilitates tracing.


<span id="0SkrgW5E"></span>
## Prerequisites


* The administrator has completed basic settings (such as enterprise system permissions and callback configuration) and has activated ArkClaw Enterprise. For details, see [Getting started with space activation](https://docs.byteplus.com/en/docs/ArkClaw/Getting_Started).

* Enterprise employees have provisioned ArkClaw instances and started conversations with ArkClaw to process tasks. For details, see the [ArkClaw guide for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employee_use_of_ArkClaw_new_version).

* (Optional) To view complete input and output information, ensure the observability data masking feature is disabled for the ArkClaw instances. For more details, see [Observability data masking](https://docs.byteplus.com/en/docs/ArkClaw/Masking_observability_data).


<span id="OLwaWwBC"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **O&M \> Observability**.

3. Select the data source for the observability dashboard and data analytics. The Claw instance page displays the observability dashboards and data analysis related to employee Claw instances. The enterprise service agent page displays the observability dashboards and data analysis related to enterprise service agents.

4. Click the **Trace analysis** tab. Filter the trace data as needed. Multiple data filters are provided.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">All filters and rules of a filter take effect based on the "AND" logic. This means that only data that meets all specified conditions will be included in the filtered results for analysis.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The system supports five filters. They combine under ‌the "AND"‌ logic, which means that only data that meet all specified conditions will be included in the filtered results for analysis.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Some filters, such as the tag filter and span attribute filter, support configuring multiple internal filtering rules. Filtering rules within the same filter apply with the "AND" logic, meaning that only data that meets all the filtering rules will be selected.   </div>
   

   
   |Serial number |Filter |Description |
   |---|---|---|
   |1 |Aggregation method |The method of aggregating data to be displayed in the chart.<br><br><br>* Auto: Automatically selects an appropriate aggregation timeframe based on the amount of selected data.<br><br>* Fixed: Aggregates data statically based on the specified aggregation timeframe. The smallest and largest timeframes for data aggregation are 30 seconds and 1 day, respectively. |
   |2 |Time range |Time range for data filtering. Data can be refreshed manually or automatically. You can choose a data refresh type as needed.<br><br><br>* By relative time: This mode dynamically filters traces for the most recent time period relative to the current time, for example, the last 1 hour.<br><br>* By absolute time: This mode statically filters traces within a fixed user\-specified time range, for example, from 2025\-11\-08 00:00:00 to 2025\-11\-10 00:00:00. |
   |3 |Tag filter |Filters data by tag (key\-value pair). You can specify up to 20 tags in a tag filter. Multiple tags are applied under the "AND" logic, meaning only data matching all tags will be selected. |
   |4 |Span attributes |Filters data by span attribute (key\-value pair). You can specify multiple span attributes. Multiple span attribute rules are applied under the "AND" logic, meaning only data that matches all span attributes will be selected. |
   |5 |Other attributes |This filter is used for fine\-grained data filtering based on multiple trace correlations. You can specify conditions such as ArkClaw instance ID, trace ID, model name, span type, AI span type, and AIP name. Filtering rules are applied using the "AND" logic, meaning only data that matches all specified rules will be selected. |
   

5. Once data filtering is completed, you can proceed with data analysis and tracing.

   * **Root Spans**: Lists all traces related to root spans that match the specified filtering conditions and displays trace details, such as trace ID, input/output tokens, model name, total tokens, AI span type, start time, duration, service name, API name, action, and session ID. Additionally, you can sort them by total token count, input token count, output token count, start time, and duration to quickly identify errors and slow queries.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In distributed tracing, a root span is the root node span of a complete trace. Each trace has only one root span. All child spans start from the root span to form a complete trace tree.      </div>
      

   * **Spans reported**: Displays the number of traces reported for the selected data over time. It provides an intuitive visualization of the health status of reported spans. This information is useful in scenarios such as troubleshooting, performance evaluation, and capacity planning. For example, a surge in the number of reported traces at a certain point in time may indicate abnormal system activity. You can quickly locate the specific service where the problem occurs by cross\-referencing the time point with other observability metrics.

   * **Spans**: Lists all traces related to spans that match the specified filtering conditions and displays trace details, such as trace ID, input/output tokens, model name, total tokens, AI span type, start time, duration, service name, API name, action, and session ID. Additionally, you can sort them by total token count, input token count, output token count, start time, and duration to quickly identify errors and slow queries.

6. Click the target trace ID in the root span list or span list to view the details of the single trace, including the complete request path and complete logs.



<Tabs>
<Tab zoneid="NkbUollkyw" title="Trace details">
<TabTitle>Trace details</TabTitle>

On the Trace details tab, inspect the complete request trace and detailed span information for a fine\-grained data analysis.


|Serial number |Module |Description |
|---|---|---|
|1 |Trace information |Displays details about the trace, such as the trace ID, start time, total duration, number of applications, and number of spans. |
|2 |View switching |Provides three views for examining span details: list, topology graph, and flame graph. You can choose the optimal view based on your scenario:<br><br><br>* List: Delivers comprehensive information for rapid filtering and span lookup.<br><br>* Topology: Intuitively visualizes trace relationships. It allows you to quickly locate critical upstream or downstream nodes related to problems.<br><br>* Flame graph: Enables visual performance analysis. It is ideal for in\-depth analysis of function invocation dependencies. |
|3 |Span filter |Provides quick filtering options, including component tags, model tags, abnormal spans, and keywords. |
|4 |Span view window |The span window. You can select an appropriate view for troubleshooting, performance analysis, and more. |
|5 |Span details |Click the target span to view detailed information about the span, including its details (such as basic information, LLM data, attributes, resources, and events) and its related metric details (such as processes, containers, and LLM).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">LLM data and LLM\-related metric information will only be displayed when the service involved in the current trace contains LLM data.</div><br> |





</Tab>
<Tab zoneid="YWk4EA2z5C" title="Complete trace logs">
<TabTitle>Complete trace logs</TabTitle>

On the **Complete trace logs** tab, view logs from all services along the request trace in chronological order on the timeline, including both normal logs and error logs. These logs are useful for troubleshooting.




</Tab>
</Tabs>


<span id="7uopUamr"></span>
## More operations


* On the Trace details tab, go to the lower\-left corner of the Trace details tab and click Details \> **LLM data**. Then, you can view the basic data about model invocations for the trace, such as input, output, request information (system, model, and type), and response information (model, cache hit tokens for the input, input tokens, output tokens, and total tokens).

* On the Trace details tab, go to the lower\-left corner of the Trace details tab and click Metrics \> **LLM**. You can view information about the services and LLM related to the current trace, including LLM invocation QPS, total LLM invocation count, token usage, LLM response latency, TTFT (Time to First Token), and TPOT (Time Per Output Token).

* Span information can be exported and used in scenarios such as data evaluation, trace diagnosis algorithm verification, detection rule optimization, exception identification effectiveness assessment, and fault case accumulation and reproduction. For more detailed descriptions, see [Exporting span data to local files](https://docs.byteplus.com/en/docs/ArkClaw/Exporting_span_data_to_local_files).


&nbsp;
