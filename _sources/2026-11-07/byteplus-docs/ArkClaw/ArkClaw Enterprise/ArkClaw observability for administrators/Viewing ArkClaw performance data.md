---
title: "Viewing ArkClaw performance data"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_performance_data"
---

The platform provides a performance analysis dashboard to facilitate global monitoring of ArkClaw performance. This topic describes how to view the performance analysis dashboard.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The dashboard metrics and data filters for employee Claw instances and enterprise service agents differ. Refer to the console for the actual display.</div>


<span id="jHg3kvPx"></span>
## Prerequisites


* The administrator has completed basic settings (such as enterprise system permissions and callback configuration) and has activated ArkClaw Enterprise. For details, see [Getting started with space activation](https://docs.byteplus.com/en/docs/ArkClaw/Getting_Started).

* Enterprise employees have provisioned ArkClaw instances and started conversations with ArkClaw to process tasks. For details, see the [ArkClaw guide for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employee_use_of_ArkClaw_new_version).


<span id="MH2Clkb0"></span>
## Viewing the dashboard


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **O&M \> Observability**.

3. Select the data source for the observability dashboard and data analytics. The Claw instance page displays the observability dashboards and data analysis related to employee Claw instances. The enterprise service agent page displays the observability dashboards and data analysis related to enterprise service agents.

4. Click the **Performance analysis** tab to access the ArkClaw performance analysis dashboard.


<span id="Op3KmJN7"></span>
### Operation overview


|Metric |Description |
|---|---|
|Request count |The number of complete end\-to\-end requests initiated by the selected ArkClaw instances within the specified time range. This information reflects the load scale and traffic fluctuation trends. It is a basic metric for evaluating system capacity. |
|Request count trend |The trend of the number of complete end\-to\-end requests initiated by the selected ArkClaw instances within the specified time range. The chart displays how request traffic changes over time, which directly reveals business load fluctuations. This can be used to identify business peak and off‑peak hours, monitor abnormal traffic fluctuations, and plan resource scaling in advance. |
|Average request latency |The average duration of requests initiated by the selected ArkClaw instances within the specified time range. It measures the overall response efficiency of end\-to\-end requests, reflecting the end\-to\-end performance from request initiation to result output. |
|Average request latency trend |The trend of the average duration of requests initiated by the selected ArkClaw instances within the specified time range. Use charts to visualize the trend in end\-to\-end response time, reflecting the long\-term evolution of full\-link performance. This can be used to identify performance degradation issues, validate the effectiveness of performance optimizations, and provide early warning of performance risks. |
|Request P99 latency |The P99 latency of requests initiated by the selected ArkClaw within the specified time range. Used to measure system tail performance under high load and the lower bound of user experience. It is a key metric for evaluating service stability and response quality, reflecting end\-to\-end performance in extreme scenarios. |
|Request P99 latency trend |The trend of request P99 latency initiated by the selected ArkClaw within the specified time range. It visually shows the pattern of tail latency changes over time in chart form, reflecting the long\-term system stability and extreme performance evolution trends. It can be used to locate performance degradation, evaluate load test results, warn of high\-latency risks, and ensure consistency of user experience. |
|Gateway starts |The total number of gateway starts for the selected ArkClaw instances during the specified time range. It reflects the stability and self\-healing capability of gateway instances, and can be used to evaluate the impact of operations and maintenance on service availability. |
|Gateway startup distribution |The distribution of the gateway starts for the selected ArkClaw instances during the specified time range. The frequency and distribution of gateway restarts and starts are displayed in a chart. This reveals system stability and O&M pace and can be used to evaluate system stability, analyze O&M impacts, and optimize self\-healing policies. |


<span id="iu6zMGru"></span>
### Instance operation analysis

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Click the instance ID above a measurement bar to quickly go to the details page of the instance and view its detailed information.</div>



|Metric |Description |
|---|---|
|Top 50 CPU utilization |The top 50 ArkClaw instances ranked by average CPU utilization in the selected ArkClaw instances within the specified time range. It is used to identify instances with the highest computing resource consumption, precisely locate computing power bottlenecks, ensure computing capacity for core services, and prevent response latency and service interruptions caused by CPU overload. |
|Top 50 memory utilization |The top 50 ArkClaw instances ranked by average memory utilization in the selected ArkClaw instances within the specified time range. It can be used to optimize memory resource structure, deeply analyze risks such as memory leaks and resource exhaustion, fundamentally prevent instance crashes caused by OOM, and ensure the stability and efficiency of instance operation. |
|Top 50 disk IOPS (read) |The top 50 ArkClaw instances ranked by disk IOPS in the selected ArkClaw instances within the specified time range. It highlights the instances with the densest disk read requests and identifies the upper limit of storage I/O processing capacity. It can be used to raise alerts for disk IOPS resource exhaustion and ensure data timeliness. |
|Top 50 disk IO bandwidth (read) |The top 50 ArkClaw instances ranked by disk I/O bandwidth within the specified time range. It identifies instances with the highest disk read traffic, assesses bandwidth pressure on the storage link, and ensures healthy transmission links of the storage network. It can be used to optimize network architecture configuration and improve the speed and reliability of data access. |


<span id="6bVbbrMa"></span>
### Tool calling


|Metric |Description |
|---|---|
|Tool executions |The total number of tool executions performed for the selected ArkClaw instances within the specified time range. This metric reflects the scale of invocations and business dependency at the tool layer, and can be used to evaluate the strength of support the tool layer provides for the overall business. |
|Top 50 tool executions |Top 50 tools ranked by the number of invocations by the selected ArkClaw within the specified time range. Not only can it be used to locate frequently invoked core tools and intuitively reflect the business dependency structure, core productivity tools, and traffic distribution at the tool layer, but it can also be leveraged to evaluate the business value of tools and prioritize the stability and performance optimization of core tools. |
|Tool execution errors |The number of tool execution errors for the selected ArkClaw instances within the specified time range. It measures the reliability of tool execution and reflects anomalies in factors such as the tools themselves, network communication, and parameter passing. |
|Top 50 tool execution errors |The top 50 tools ranked by execution errors occurred when the selected ArkClaw invoked tools within the specified time range. Not only can it be used to locate error\-prone tools, quickly identify the root cause of faults, and measure the reliability and health of tool execution, but it can also be leveraged to rapidly narrow down the scope of fault diagnosis, improve troubleshooting efficiency, and ensure the service availability of the tool layer. |
|Average tool execution latency |The average duration of tool executions for the selected ArkClaw instances within the specified time range. It measures the performance efficiency of the tool execution phase and serves as a key sub\-metric for decomposing end\-to\-end request latency. |
|Average tool execution latency trend |The average duration trend of tool executions for the selected ArkClaw instances within the specified time range. Shows the evolution of tool execution performance over time. It reflects the long\-term performance and load changes of the tool layer. This metric can be used to identify performance degradation and bottlenecks, verify performance optimization results, issue performance risk warnings, and break down end\-to\-end request latency to pinpoint specific problem layers. It also provides data support for capacity planning, resource scheduling, and rate\-limiting policies at the tool layer, ensuring efficient tool response and a good usage experience. |


<span id="aCfASkOL"></span>
### Agent call


|Metric |Description |
|---|---|
|Agents |The total number of agents that have engaged in data interactions for the selected ArkClaw instances within the specified time range. This metric reflects the scale of the agent ecosystem covered by ArkClaw and the activity level of connected agent instances. It can be used to evaluate service coverage and ecosystem activity and to measure the penetration level of ArkClaw. |
|Agent invocations |The total number of agent invocations for the selected ArkClaw instances within the specified time range. It reflects the agent scheduling intensity of ArkClaw. This information can be used to analyze business traffic and support resource scaling and rate\-limiting strategies. |
|Average agent invocation latency |The average duration of agent invocations by the selected ArkClaw instances within the specified time range. It measures the response efficiency in the agent invocation phase and reflects agent invocation performance from request initiation to result output. |
|Agent invocation distribution by channel |Invocation distribution by channel for the selected ArkClaw instances within the specified time range. It presents the invocation shares of different channels and reflects the composition of traffic sources. This information can be used to analyze the traffic contribution of each channel, identify core and marginal channels, and provide data support for channel management and resource allocation. |
|Top 5 channels by agent invocation count |The top 5 channels by agent invocation of the selected ArkClaw instances within the specified time range. It lists the core channels that account for the highest share of traffic. This information allows you to identify core business entry points that require guaranteed stability and performance priority. You can optimize resource configuration for better user experience with these channels and business availability. |
|Average latencies of agent invocations​ |The trend of the average agent invocation duration for the selected ArkClaw instances within the specified time range. It displays the duration fluctuations over time, reflecting performance fluctuations and long\-term performance evolution trends. This helps identify time points of sudden duration increases or decreases and correlate such anomalies with version releases, O&M operations, or external events to locate the root cause of performance changes. This information also helps predict future performance trends, support proactive planning of resource scaling or performance optimization, and avoid subsequent performance degradation. |
|LLM invocation success rate |The success rate of large model invocations initiated by the selected ArkClaw within the specified time range. Used to measure service reliability and link stability during large model invocations, reflecting the overall health from request initiation to effective result return from the model. |
|LLM invocation success rate trend |The trend of success rates for large model invocations initiated by the selected ArkClaw within the specified time range. It visually shows fluctuations in large model invocation success rates over time in chart form, reflecting the long\-term evolution of model service stability and link health. It can be used to identify service failures, version change impacts, or network anomalies. |


<span id="ILjNtEnG"></span>
### Messages


|Metric |Description |
|---|---|
|Messages |The total number of messages generated in chats by the selected ArkClaw instances within the specified time range. It reflects the overall chat load and is the basic metering metric for evaluating message processing performance. |
|Message processing success rate |The message processing success rate of the selected ArkClaw instances within the specified time range. It measures the service availability and stability of the ArkClaw instance. This information, together with metrics such as average message queue length and average message processing duration, enables rapid troubleshooting and root cause identification. The message processing success rate is the percentage of successful message processing tasks to the total message processing tasks. |
|Average message processing latency |The average message processing time of the selected ArkClaw instances within the specified time range. It measures the average time from message receipt to completion, and directly reflects wait time and usage experience. In addition, as a service availability indicator, it can be used to assess whether the agreed response time requirements (such as P95 and P99 latencies) are met. |
|Average message queue length |The number of messages awaiting processing in the selected ArkClaw scope during the specified time range. It measures the degree of message processing congestion and reflects the match between service throughput capacity and request volume. |
|Message distribution by source |The distribution of message\-sending sources for the selected ArkClaw instances within the specified time range. It displays the proportional composition of messages from different sources and reflects the distribution characteristics of message\-sending entities. You can use this information to identify core message source groups, evaluate the business contribution of different sources, and optimize product strategy formulation and prioritization. |
|Message channel distribution |Message distribution by channel for the selected ArkClaw instances during the specified time range. It displays the proportional composition of messages from different channels and reflects the distribution pattern of message traffic entrances. |


<span id="NOsISbrg"></span>
### Session analysis


|Metric |Description |
|---|---|
|Laggy sessions |The number of sessions with lag anomalies occurring on the selected ArkClaw instances within the specified time range. This reflects the scale of lag exceptions in sessions and serves as a basic metric for measuring the degree of usage experience degradation. |
|Average latency of laggy sessions |The average duration of laggy sessions for the selected ArkClaw instances within the specified time range. It measures the duration of a single laggy session and reflects the impact of lag on usage experience. |
|Session distribution by status |Distribution of sessions by session status for the selected ArkClaw instances within the specified time range. This information shows the status transition of sessions and reflects the overall system health and abnormal fluctuations. It enables rapid identification of sudden or abnormal changes in the proportion and helps assess the impact of O&M operations and traffic fluctuations on session statuses. |


<span id="usHAnrQE"></span>
## What to do next

The following operations are available on the monitoring dashboard:


|Serial number |Actions |Description |
|---|---|---|
|1 |Resource filter |Filter data by user, email, and instance. The default values of these fields are All. |
|2 |Time range |The time range for data filtering. You can specify a relative or absolute time range. |
|3 |Refresh frequency |Data refresh frequency. Available refresh methods include manual refresh or auto\-refresh at the specified intervals. |
|4 |Chart actions |The operations that are supported by a chart, such as Enlarge, Compare, and Download as CSV.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported operations vary based on different charts. The displayed operations apply.</div><br><br><br><br>* Enlarge: Switch to the full\-screen view.<br><br>* Compare: Only trend charts support this action. Compares data between two time periods to provide trend insights.<br><br>* Download as CSV: Export the raw or formatted data to a CSV file for statistics or analysis. |
|5 |Chart data filtering |Click a specific item in the legend at the bottom of a chart to filter data sources in the chart.<br><br><br>* Click a data source to show or hide the corresponding data in the chart.<br><br>* On the right of the specified data source, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_121d43c534f90353b5ddce79208da3c6.png) </span> icon to display only the graph element for that data source and hide the graph elements for other data sources. |
|6 |Quick redirection to instance details |Click the instance ID above the metering bar to quickly jump to the detail page of the current instance and view detailed information. |
