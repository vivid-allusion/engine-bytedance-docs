---
title: "Viewing MCP toolset monitoring data"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_toolset_monitoring_data"
---

MCP toolset is integrated with BytePlus [Cloud](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor), providing observability into MCP toolset performance metrics. You can view MCP toolset monitoring data to understand the operational status of the MCP toolset across dimensions such as bandwidth traffic, request invocation, retrieval type, performance latency, and tool index.ool index.

<span id="nZjAfZJe"></span>
## Notes


* You can view monitoring data only when the target MCP toolset is in the **Running ** state. Query\-related limits are as follows:

   * The supported time range for one query is from 1 hour to 15 days.

   * You can only query monitoring data within the past 30 days. Time ranges exceeding 30 days are not supported.

* The collection frequency for MCP toolset monitoring metrics is 30s, which means that related monitoring metrics are collected every 30s.


<span id="COXiiaWd"></span>
## Procedure


1. Log in to [the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the top menu bar, select the project and region of the target MCP toolset.

3. In the left\-side navigation pane, select "Gateway \> MCP Toolset".

4. On the tool list page, click the name of the target toolset, and select the "Monitoring" tab to view the monitoring metric data of the specified toolset.

   * **Time filtering range**

      By default, monitoring data from the past 24 hours is displayed. You can also customize the time range (accurate to the minute).

   * **Chart linkage**

      After enabling chart linkage, you can quickly view monitoring metrics and information at the same time point across all charts.

   * **Currently supported metrics**

      
      |Metric |Unit |Description |
      |---|---|---|
      |Number of requests |Count |Refers to the total number of requests received by the MCP toolset from the client (caller) during the current collection period (for example, 1 hour). |
      |Request distribution (range/exact) |Count |Monitors the MCP toolset metrics from two dimensions: range and exact request distribution during the current collection period (for example, 1 hour).<br><br><br>* Request distribution (range): Request distribution statistics are based on macro intervals or ranges.<br><br>* Request distribution (exact): Request distribution statistics are based on specific objects or values. |
      |Average latency |ms |Refers to the average time taken by the MCP toolset to process requests during the current collection period (for example, 1 hour). |
      |Egress response bandwidth |bit/s |Displays the traffic per second that the MCP toolset sends back to the MCP client (caller) during the current collection period (for example, 1 hour).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Refers to the total traffic responded by the MCP toolset to the agent when accessed through the public or private network, including both public and private network traffic.</div><br> |
      |Public egress response bandwidth |bit/s |Displays the amount of internet traffic per second responded by the MCP toolset to the MCP client when accessed via the internet during the current collection period (for example, 1 hour). |
      |Number of semantic retrieval requests |Count |Displays the total number of` search_tools `requests received by the MCP toolset in **semantic retrieval mode** during the current collection period (for example, 1 hour). |
      |Number of semantic retrieval request tasks |Count |Displays the total number of tasks when the MCP toolset receives `search_tools `requests in **semantic retrieval mode ** during the current collection period (for example, 1 hour).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Under normal circumstances, this metric value <strong>is not less than</strong> the number of semantic retrieval requests. If a search request fails, this metric value <strong>may be less than</strong> the number of semantic retrieval requests.</div><br> |
      |Number of tag retrieval requests |Count |Displays the total number of` list_tools_by_tags `requests received by the MCP toolset in ** tag retrieval mode ** during the current collection period (for example, 1 hour). |
      |Number of semantic retrieval tool indexes |Count |Displays the number of tool indexes built inside the MCP toolset in **semantic retrieval mode** during the current collection period (for example, 1 hour).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Each tool corresponds to one index.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After each switch from semantic retrieval to another tool calling mode, the index information of existing tools is reported as <code>0</code>.</div><br> |
