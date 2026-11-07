---
title: "Insight dashboards"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Insight_dashboards"
---

AI application monitoring provides the insight dashboard feature specific to AgentKit and enables visual observability of statistics and trend analysis of data from various agent\-related resources. This facilitates health checks, performance optimization, exception detection, and other aspects. This topic provides a detailed introduction to how to view insight dashboards of AgentKit applications.

<span id="uld8SlWP"></span>
## Procedure


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Click **Insight dashboard ** and select a time range and the dashboard to view the dashboard data for the specified time period.


You can perform the following operations on insight dashboards:


|Serial number |Action |Descriptions |
|---|---|---|
|1 |Switch dashboard |The insight dashboard feature provides independent dashboards for each resource, facilitating health checks, performance optimization, anomaly detection, and other operational tasks. The currently available dashboards include usage analysis and performance analysis. Click the target dashboard name to switch. |
|2 |Resource scope |Filter data by resource. "All" is selected by default. You can configure the agents you want to observe based on the actual needs. |
|3 |Time range |Filters data by the specified time range. The specified time range can be either a relative time range or an absolute time range. |
|4 |Refresh frequency |The data refresh frequency supports manual or automatic refreshes based on a specified time. |
|5 |Chart\-based action |Operations available for individual charts, such as zoom\-in, period\-over\-period comparison, and data download as CSV.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported operations vary across different charts. Refer to the actual display for details.</div><br><br><br><br>* Enlarge: View a chart in full screen.<br><br>* Period\-over\-period comparison: Only trend charts support this action. Specify a time period for period\-over\-period data and trend comparison.<br><br>* Download as CSV: Export data as a CSV file for statistics or analysis. |


<span id="EoSQ5hcS"></span>
## Dashboard details


<Tabs>
<Tab zoneid="s34wQFH9Ho" title="Usage analysis">
<TabTitle>Usage analysis</TabTitle>

<span id="aEqPMqzu"></span>
### Usage overview

The overview of key metrics related to AgentKit agent resource usage.


|Metric |Descriptions |
|---|---|
|AgentKit call count |The total call count of AgentKit agents within the specified time range. It can be used to assess business access volume and system load level, providing data support for resource planning, scaling strategies, and business traffic analysis. |
|AgentKit Call Trends |The trend chart of AgentKit agent call count within the specified time range. It visually presents the change patterns of call volume over time, and can be used to quickly identify abnormal fluctuations such as sudden surges or drops in traffic, locate service disruptions, access exceptions, or business peaks, and assist in capacity planning and troubleshooting. |
|AgentKit active sessions |The active session count of AgentKit agents within the specified time range. Active sessions include sessions that complete initialization, generate event reporting, or terminate abnormally. The active session count is a basic metric for measuring the business scale and access volume at the session level, and can directly reflect the scale of business sessions, user access volume, and system load level. |
|AgentKit Active Sessions Trend |The trend chart for active session count of AgentKit agents within the specified time range. It can be used to quickly detect abnormal fluctuations such as sudden surges or drops in session volume, and locate issues including service disruptions, access exceptions, and traffic jitters. |
|Token consumption |The total token consumption of AgentKit agents within the specified time range. It can be used to estimate costs and identify high\-consumption scenarios, providing data support for optimizing call strategies and controlling operating costs. |
|Token consumption trend |The trend chart of total token consumption of AgentKit agents within the specified time range. It visually presents the evolution patterns of token consumption over time, and can be used to identify abnormal cost fluctuations and evaluate optimization effects. This provides decision support for cost control and resource configuration adjustment. |


<span id="KS6K3HJO"></span>
### Usage ranking

The Top 50 ranking of key metrics related to AgentKit agent resource usage.


|Metric |Descriptions |
|---|---|
|AgentKit Call Ranking |The Top 50 ranking of AgentKit agents by call volume within the specified time range. It intuitively presents the business dependency and usage popularity of each agent, and can be used to identify core high\-frequency agents and assess business distribution. This provides data support for stability assurance and business optimization. |
|AgentKit Token Consumption Ranking |The Top 50 ranking of AgentKit agents by token consumption within the specified time range. It intuitively presents the cost proportion and resource consumption distribution of each agent, and can be used to identify high\-consumption agents, optimize call strategies, and control operating costs. This provides decision\-making basis for refined cost control and resource configuration. |
|AgentKit Execution Steps Ranking |The Top 50 ranking of AgentKit agent call operations within the specified time range. It intuitively presents the operational complexity and frequently executed paths of agents, and can be used to identify inefficient or redundant operations, optimize agent decision\-making logic, and improve execution efficiency. This provides guidance for business process streamlining and performance optimization. |





</Tab>
<Tab zoneid="AkRrDd4oV6" title="Performance analysis">
<TabTitle>Performance analysis</TabTitle>

<span id="aNnH2HOn"></span>
### Performance overview

The overview of key metrics related to AgentKit agent performance.


|Metric |Descriptions |
|---|---|
|AgentKit call average latency |The average latency of AgentKit agent calls within the specified time range. It measures the overall response efficiency of agent calls, reflects the trace performance from request initiation to result return, and serves as a core basic metric for evaluating user experience and service quality. |
|AgentKit call average latency trend |The average latency trend chart of AgentKit agent calls within the specified time range. It visually presents the change patterns of average latency over time, and can be used to identify performance fluctuations, locate performance degradation nodes, and verify optimization effects. This provides a reference for long\-term performance monitoring and early warning. |
|AgentKit call P90 delay |The P90 latency of AgentKit agent calls within the specified time range. It means that 90% of call requests can be completed within this latency threshold, and can be used to measure the tail performance of agent calls and service stability in extreme scenarios. It serves as a key metric for evaluating system robustness and the lower limit of user experience. |
|AgentKit call P90 latency trend |The P90 latency trend chart of AgentKit agent calls within the specified time range. It visually presents the long\-term evolution trend of tail latency, and can be used to identify tail latency issues, evaluate pressure test effects, and alert on performance risks. This guarantees service stability in key business scenarios. |
|AgentKit call error rate |The error rate of AgentKit agent calls within the specified time range. It measures the service reliability and trace stability of agent calls, reflects the health status of business requests, and acts as a core metric for assessing service availability and fault impact scope. |
|AgentKit Call Error Rate Trends |The error rate trend chart of AgentKit agent calls within the specified time range. It visually presents the fluctuation of error rate over time, and can be used to quickly identify service failures, impacts of version changes or dependency anomalies and provide early warnings of service disruption risks. This guarantees business continuity. |
|AgentKit P90 Execution Time Ranking |The Top 50 ranking of operations by P90 execution latency of AgentKit agents within the specified time range. It intuitively presents the operation nodes with the highest latency in agent execution traces, and can be used to locate performance bottlenecks and identify inefficient logic. This provides data support for targeted optimization to improve overall execution efficiency and response speed. |


<span id="DtavF5Uo"></span>
### Tool calls

Provide an analysis dashboard for tools in AgentKit to display data, trends and rankings related to tool calls.


|Metric |Descriptions |
|---|---|
|Tool call count |The call count of all tools within the specified time range. It reflects the business load scale and usage popularity of the tool layer, and serves as a basic metric for assessing tool service pressure and planning resource configurations and expansion strategies. |
|Tool Call Trend |The trend chart for the call count of all tools within the specified time range. It visually presents the patterns of tool call volume changes over time, and can be used to identify business peaks, abnormal traffic fluctuations, or impacts of dependency changes. This provides a basis for resource scheduling and troubleshooting. |
|Tool Call Leaderboard |The Top 50 raning of call count for all tools within the specified time range. It intuitively presents the business dependency and usage popularity rankings of each tool, and can be used to identify core high\-frequency tools and low\-utilization redundant tools. This provides data support for tool governance, resource prioritization, and business process optimization. |
|average tool call time |The average latency of tool calls within the specified time range. It measures the overall response efficiency of tool calls, reflects the trace performance from the initiation of tool calls to result return, and serves as a key metric for evaluating tool service quality. |
|Average Tool Call Time Trend |The average latency trend chart of tool calls within the specified time range. It visually presents the long\-term fluctuations and evolution patterns of average latency for tools, and can be used to locate performance degradation issues, evaluate optimization effects, and alert on high latency risks. This guarantees consistent experience of tool calls. |
|Average time spent on tool calls |The Top 50 ranking of tools by average call latency within the specified time range. It intuitively presents the average response efficiency ranking of each tool, and can be used to identify tools with performance bottlenecks and guide targeted optimization. This boosts the response speed of the overall tool call trace. |
|Tool call P90 time consuming |The P90 latency of tool calls within the specified time range. It means that 90% of tool call requests can be completed within this latency threshold, and can be used to measure the tail performance of tool calls and the lower limit of user experience in extreme scenarios. It serves as an important metric for evaluating the tool service stability. |
|Tool Call P90 Time Consumption Trend |The P90 latency trend chart of tool calls within the specified time range. It visually presents the long\-term evolution trend of tool tail latency, and can be used to identify tail latency issues, evaluate pressure test effects, and alert on performance risks. This guarantees service stability in key business scenarios. |
|Tool Call P90 Time Consumption Leaderboard |The Top 50 ranking of P90 latency for tool calls within the specified time range. It intuitively presents the tail performance ranking of each tool, and can be used to locate tools with high latency risks and optimize resource configurations. This prevents tail latency issues from affecting overall business stability. |


<span id="NU934xb9"></span>
### Memory analysis

Provide a dedicated tool analysis dashboard for memory libraries to visually display data, trends, and rankings related to memory library tool calls.


|Metric |Descriptions |
|---|---|
|Memory calls |The memory library tool call count within the specified time range. It reflects the business load scale and usage frequency of the memory library service, and serves as a basic metric for evaluating the activity level of memory capabilities and planning resource configuration. |
|Memory call trend |The trend chart of memory library tool call count within the specified time range. It visually presents the patterns of memory library call volume changes over time, and can be used to identify business peaks, abnormal traffic fluctuations, or impacts of dependency changes. This provides a basis for resource scheduling and troubleshooting of the memory service. |
|Memory Calling Top 50 |The Top 50 raning of memory library tool call count within the specified time range. It intuitively presents the business dependency and usage popularity rankings of each memory library tool, and can be used to identify core high\-frequency memory operations and low\-utilization redundant logic. This provides data support for memory library governance, resource prioritization, and business process optimization. |
|Memory call average time |The average latency of memory library tool calls within the specified time range. It measures the overall response efficiency of the memory library service, reflects the trace performance from request initiation to data return, and serves as a key metric for evaluating memory capability performance and user experience. |
|Memory call average time trend |The average latency trend chart of memory library tool calls within the specified time range. It visually presents the long\-term fluctuations and evolution patterns of average latency for memory libraries, and can be used to locate performance degradation issues, evaluate optimization effects, and alert on high latency risks. This guarantees consistent experience of the memory service. |
|Average Memory Call Time |The Top 50 ranking of average latency for memory library tool calls within the specified time range. It intuitively presents the response efficiency ranking of each memory library, and can be used to identify operations with performance bottlenecks and guide targeted optimization. This boosts the response speed of the overall memory trace. |
|Memory call P90 time consuming |The P90 latency for memory library tool calls within the specified time range. It means that 90% of memory library call requests can be completed within this latency threshold, and can be used to measure the tail performance of the memory service and its stability in extreme scenarios. It serves as an important metric for evaluating the memory capability robustness. |
|Memory call P90 time consuming trend |The P90 latency trend chart for memory library tool calls within the specified time range. It visually presents the long\-term evolution trend of tail latency for memory libraries, and can be used to identify tail latency issues, evaluate pressure test results, and alert on performance risks. This guarantees the stability of the memory service in key business scenarios. |
|Memory Call P90 Time Consumption Ranking |The Top 50 ranking of P90 latency for memory library tool calls within the specified time range. It intuitively presents the tail performance ranking of each memory library operation, and can be used to locate operations with high latency risks and optimize resource configurations. This prevents tail latency issues from affecting overall business stability. |


<span id="8ZVZQfI5"></span>
### Knowledge base analysis

Provide a dedicated tool analysis dashboard for knowledge bases to visually display data, trends, and rankings related to knowledge base tool calls.




</Tab>
</Tabs>
