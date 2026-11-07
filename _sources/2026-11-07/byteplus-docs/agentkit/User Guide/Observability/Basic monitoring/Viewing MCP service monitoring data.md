---
title: "Viewing MCP service monitoring data"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_MCP_service_monitoring_data"
---

MCP service is integrated with BytePlus [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor), allowing observability into MCP performance metrics. Based on the monitoring data, you can view the operating status of the MCP service across dimensions such as traffic volume, response performance, and network load.

<span id="GzC78dfa"></span>
## Notes


* You can view monitoring data only when the associated MCP service is in the **Running ** state. Query\-related limits are as follows:

   * The supported time range for one query is from 1 hour to 15 days.

   * You can only query monitoring data within the past 30 days. Time ranges exceeding 30 days are not supported.

* The collection frequency for MCP service monitoring metrics is 30s, which means that related monitoring metrics are collected every 30s.


<span id="8gqFZ6XY"></span>
## Procedure


1. Log in to [the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the top menu bar, select the project and region of the target MCP service.

3. In the left\-side navigation pane, select "Gateway \> MCP Service".

4. On the MCP service list page, click the name of the target MCP service and then select the "Monitoring" tab to view the monitoring metric data of the specified MCP service.

   * **Time filtering range**

      By default, monitoring data from the past 24 hours is displayed. You can also customize the time range (accurate to the minute).

   * **Chart linkage**

      After enabling chart linkage, you can quickly view monitoring metrics and information at the same time point across all charts.

   * **Currently supported metrics**

      
      |Category |**Metric** |Unit |Description |
      |---|---|---|---|
      |Service call |Number of requests |Count |Total number of requests received by the MCP service interface within the statistical period you specify (for example, 1 hour). |
      ||Request distribution (range/accuracy) |Count |Within the statistical period you specify (for example, 1 hour), the MCP service monitoring metrics are displayed across the range and exact dimensions of request distribution.<br><br><br>* Request distribution (range): Request distribution statistics are based on macro intervals or ranges.<br><br>* Request distribution (accuracy): Request distribution statistics are based on specific objects or values. |
      ||Average latency |ms |Average duration of MCP service request processing within the statistical period you specify (for example, 1 hour). |
      ||Egress response bandwidth |bit/s |The traffic transferred per second out of AgentKit within the statistical period you specify (for example, 1 hour).<br><br>> Refers to the public network traffic that the MCP service sends back to the agent when accessed over the public network, including both public and private networks. |
      ||Public egress response bandwidth |bit/s |The traffic per second that the MCP service sends back to the MCP client when accessed over the internet within the statistical period you specify (for example, 1 hour).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Refers to the total traffic responded by the MCP service to the agent when accessed through the public or private network, including both public and private network traffic.</div><br> |
      |Service operation<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Metrics of MCP instance resources are available only for MCP services with a creation type of "<a href="https://docs.byteplus.com/en/docs/agentkit/MCP_services#GsgcqzsJ">Deployed MCP service</a>". Only MCP services whose backend service is "JSON configuration" or "Image" are considered deployed.</div><br> |CPU usage |% |Displays the CPU usage of the MCP service for the selected time period (for example, 1 hour).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This value represents the average CPU usage across all instances under the target MCP service.</div><br> |
      ||Memory usage |% |Displays the memory usage of the MCP service for the selected time period (for example, 1 hour).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This value represents the average memory usage across all instances under the target MCP service.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Memory usage<strong> = </strong>Actual memory consumed / Maximum memory consumption allowed.</div><br> |
      ||Number of instances |Count |Displays the number of running instances associated with the MCP service for the selected time period (for example, 1 hour). |
