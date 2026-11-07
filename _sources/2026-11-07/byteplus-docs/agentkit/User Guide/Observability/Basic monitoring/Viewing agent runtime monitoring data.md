---
title: "Viewing agent runtime monitoring data"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_agent_runtime_monitoring_data"
---

Through integration with BytePlus [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor), agent runtime monitoring delivers basic metric observability capabilities. You can view agent runtime monitoring data from two dimensions: runtime status and instance resources. This helps you understand the overall health of your agent runtimes and quickly troubleshoot O&M issues.

<span id="Cjq55PXf"></span>
## Notes


* You can view monitoring data only when the target agent runtime is in the **Running** state. Query\-related limits are as follows:

   * The supported time range for one query is from 1 hour to 15 days.

   * You can only query monitoring data within the past 30 days. Time ranges exceeding 30 days are not supported.

* The collection frequency for agent runtime monitoring metrics is 30s, which means that related monitoring metrics are collected every 30s.


<span id="j6QSLia6"></span>
## Procedure


1. Log in to [the AgentKit console](https://console.byteplus.com/agentkit).

2. In the top menu bar, select the project and region of the target agent runtime.

3. In the left\-side navigation pane, select "Agent Runtime".

4. On the agent runtime list page, click the name of the target agent runtime, and select the "Monitoring" tab to view the monitoring metric data of the specified agent runtime.

   * **Time filtering range**

      By default, monitoring data within the past 1 day is displayed. You can also customize the time range (accurate to the minute).

   * **Chart linkage**

      After enabling chart linkage, you can quickly view monitoring metrics and information at the same time point across all charts.

   * **Currently supported metrics**

      
      |Category |Metric |Unit |Description |
      |---|---|---|---|
      |Agent runtime |Number of requests |Count |Displays the total number of requests received by the agent runtime interfaces during the selected time period (for example, 1 hour). |
      ||Request distribution (range/accuracy) |Count |Displays agent runtime monitoring metrics from the dimensions of request distribution range and precision during the selected time period (for example, 1 hour).<br><br><br>* Request distribution (range): Request distribution statistics are based on macro intervals or ranges.<br><br>* Request distribution (accuracy): Request distribution statistics are based on specific objects or values. |
      ||Average latency |ms |Displays the average time taken by the target agent runtime to process requests during the selected time period (for example, 1 hour). |
      ||Egress bandwidth |bit/s |Displays the traffic flowing out of the agent runtime per second during the selected time period (for example, 1 hour). |
      |Agent instance resources |CPU |% |Displays the CPU usage of the agent runtime during the selected time period (for example, 1 hour).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This value represents the average CPU utilization across all instances under the target agent runtime.</div><br> |
      ||Memory |% |Displays the memory usage of the target agent runtime during the selected time period (for example, 1 hour).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This value represents the average memory usage across all instances under the target agent runtime.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Memory usage <strong>=</strong> Actual memory consumed / Maximum memory consumption allowed.</div><br> |
      ||Instance quantity |Count |Displays the number of running instances of the target agent runtime during the selected time period (for example, 1 hour). |
