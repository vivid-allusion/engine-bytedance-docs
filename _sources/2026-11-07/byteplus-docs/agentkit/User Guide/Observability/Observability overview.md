---
title: "Observability overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Observability_overview"
---

The AgentKit observability system consists of three parts: **basic monitoring (metrics), application observability (traces), and logs**. It supports layered monitoring from underlying hardware resources to upper\-layer business applications, together with end\-to\-end log collection. You can therefore track the running status of various resources, business usage, and the complete event information produced while the system runs.

<span id="rmhhLZNd"></span>
## Applicable scenarios

Basic monitoring and application observability differ in monitoring scope and collected data. Choose the appropriate observability method based on your actual scenario.


* ### **Basic monitoring** <span id="5xpqSASr"></span>

   Basic monitoring ** targets resource instances and components ** such as gateway instances, agent runtimes, tools, MCP services, MCP toolsets, and memories. It displays the running status of components in real time through multidimensional metrics and visualization dashboards, and can be used to check service health status, request count, resource usage trends, and system errors. It is mainly used to **determine whether the underlying resources themselves are functioning normally**. It is suitable for scenarios such as resource health checks, capacity evaluation, and post\-release stability verification.

* ### **Application observability** <span id="ANupFv0Q"></span>

   Application observability **targets agents or business applications**, providing complete call chains, session records, and metric statistics and analysis to enable fine\-grained observability across the entire agent workflow. In addition to some basic monitoring capabilities, it also tracks the complete internal execution process of an application, and is primarily used for **locating program failures, optimizing runtime performance, and evaluating business outcomes**. It is suitable for scenarios such as trace tracking, performance tuning, business outcome evaluation, and root cause analysis.

* ### **Logs** <span id="FgvbSPO7"></span>

   **The logging scope covers resource instances and system components**, including agent runtimes, tools, MCP services, and gateway instances. Logs contain output such as running status, request information, resource usage, and system errors. You can use logs to **check whether the underlying resources and components run normally**. This enables quick detection of service exceptions, capacity fluctuations, and system\-level errors. Applicable scenarios include resource health checks, stability verification, post\-release observation, and basic troubleshooting.


<span id="RthTTnv4"></span>
## Billing instructions


* **Basic monitoring** is available at no additional cost.

* **Application observability** is billed based on platform rules. Before you use application observability, confirm the relevant billing details and quota policies. For detailed billing rules, see [Application observability billing notes](https://docs.byteplus.com/en/docs/apmplus/Server_side_billing_instructions).

* **Logs ** are billed according to the TLS billing rules. Before you use logs, confirm the billing details. For the actual billing details, see[ TLS billing overview](https://docs.byteplus.com/en/docs/tls/billable_items?lang=en).


<span id="VEs8IoG0"></span>
## Observability capabilities

<span id="yeROz82X"></span>
### Concepts


|Concept |Description |
|---|---|
|Memory recall |Memory recall refers to the process in which an agent, when handling a new request, retrieves, matches, and **extracts relevant historical memories** (such as conversation history, user preferences, and exclusive information) from the memory based on the current context. It is the core step of "retrieving" memory, and related monitoring is typically used to observe recall call scale, average latency, and error rate. |
|Event creation |A creation event refers to the process in which an agent, while interacting with users or executing tasks, filters and extracts valuable information from massive amounts of raw data and **stores it in the memory**. It is the preceding step for "storing" memory, and related monitoring is typically used to observe whether the write path is stable and whether latency is abnormal. |


<span id="IoN48o9I"></span>
### Basic monitoring

Basic monitoring monitors the metric status of AgentKit components across the following dimensions, and is suitable for scenarios such as resource health inspections, capacity observation, troubleshooting, and post\-release stability verification.


|Feature |Description |
|---|---|
|[Viewing agent runtime monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_agent_runtime_monitoring_data) |Monitors basic agent runtime metrics across two dimensions: agent running status and instance resources. Supports viewing key metrics such as "request count", "request distribution", "average latency", and "instance count", providing a clear view of the **agent's overall running load and monitoring status**. |
|[Viewing tool monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_tool_monitoring_data) |Monitors metrics for tools and tool instance resources. Supports viewing basic metrics such as "request count", "request distribution", "CPU usage", and "instance count", making it easy to observe **tool call volume and instance resource usage**. |
|[Viewing memory monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_memory_monitoring_data?TagIDs=2&lang=en) |Provides monitoring of memory\-related runtime metrics, covering memory creation events and memory recall scenarios. Supports viewing "API call count", "average latency", and "total error rate", which can be used to **evaluate the availability and response performance of the memory service**. |
|[Viewing MCP service monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_service_monitoring_data?lang=en) |Collects basic runtime metrics for MCP services, including "request count", "request distribution", and "average latency", which can be used to analyze the **call performance and stability of MCP services**. |
|[Viewing MCP toolset monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_toolset_monitoring_data) |Monitors runtime metrics for MCP toolsets. Supports viewing "semantic search request count", "tag search request count", "tool index count", and more, which can be used to **evaluate tool search efficiency and tool index scale**. |
|[Viewing gateway instance monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_gateway_instance_monitoring_data?lang=en) |Monitors request processing and traffic metrics for gateway instances. You can view key metrics such as QPS, request count, total inbound/outbound bandwidth, and inbound/outbound internet bandwidth. These metrics help you track the ** request load, response performance, and traffic throughput of gateway instances** visually. |
|[Viewing model service monitoring data](https://docs.byteplus.com/en/docs/agentkit/Viewing_model_service_monitoring_data?lang=en) |Collects token consumption and generation performance metrics for the model service. You can view metrics such as input/output tokens, cache hit ratio, TTFT, and TPOT by Proxy API Key and by model. These metrics help you ** evaluate model call cost, generation latency, and streaming response performance**. |


<span id="x8h54Gp1"></span>
### Application observability

Application observability is designed for agents and upper\-layer business applications, providing diversified monitoring and analysis capabilities. The following monitoring modules are included: runtime overview, memory analysis, knowledge base analysis, session analysis, trace tracking, model monitoring, log analysis, tool analysis, insight dashboards, and alert templates. It is suitable for scenarios such as business metric analysis, performance tuning, root cause analysis, and business outcome evaluation. For details, refer to [Observability](https://docs.byteplus.com/en/docs/agentkit/Observability-?lang=en).

<span id="RgNX44E0"></span>
### Logs


1. [Enable logs](https://docs.byteplus.com/en/docs/agentkit/Enabling_logs?lang=en)

   After you enable the log service, you can view the runtime logs of various resources directly in the **AgentKit console**. Viewing these logs helps you locate call exceptions and supports troubleshooting and business operations analysis.

2. [Viewing logs](https://docs.byteplus.com/en/docs/agentkit/Viewing_logs?lang=en)

   You can view logs, that is, the runtime logs of each resource, to analyze log information and quickly locate anomalies.


<span id="tzf3dkRM"></span>
## Troubleshooting recommendations

When troubleshooting is required, we recommend that you first use **basic monitoring** to check whether an underlying resource failure has occurred. If the resources are running as expected, use **application observability** to dive into the business execution flow and locate the cause of the anomaly. Common typical anomalies corresponding to each type of observability are listed below:


|Observability type |Typical anomalies |
|---|---|
|Basic monitoring |Sudden drop or spike in request volume<br><br>Continuously rising average latency<br><br>Sudden increase in error rate<br><br>Abnormal fluctuation in instance count<br><br>Abnormal changes in index volume or search requests |
|Application observability |Call chain interruption<br><br>Missing instrumentation events<br><br>Sharp drop in business metrics<br><br>Abnormal latency in core steps<br><br>Incomplete instrumentation field reporting |
|Logs |Sudden drop or spike in request volume<br><br>Service unavailable or concentrated occurrence of 5xx errors<br><br>Abnormal changes in index volume or search requests<br><br>Network errors or connection timeouts<br><br>Sudden increase in error rate<br><br>Abnormal fluctuation in instance count |
