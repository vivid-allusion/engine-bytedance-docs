---
title: "Viewing tool monitoring data"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_tool_monitoring_data"
---

Through integration with BytePlus [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor), tool monitoring delivers basic metric observability capabilities. You can view tool monitoring data from two dimensions: tools and tool instance resources. This helps you understand the overall health of your tools and quickly troubleshoot O&M issues.

## Notes

* You can view monitoring data only when the target tool is in the ** Running ** state. Query\-related limits are as follows:

   * The supported time range for one query is from 1 hour to 15 days.

   * You can only query monitoring data within the past 30 days. Time ranges exceeding 30 days are not supported.

* The collection frequency for tool monitoring metrics is 30s, which means that related monitoring metrics are collected every 30s.

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the top menu bar, select the project and region of the target tool.

3. In the left\-side navigation pane, select "Sandbox Template".

4. On the tool list page, click the name of the target tool, and select the "Monitoring" tab to view the monitoring metric data of the specified tool.

   * **Time filtering range**

      By default, monitoring data within the past 1 day is displayed. You can also customize the time range (accurate to the minute).

   * **Chart linkage**

      After enabling chart linkage, you can quickly view monitoring metrics and information at the same time point across all charts.

   * **Currently supported metrics**

      |Category |Metric name |Unit |Description |
      |---|---|---|---|
      |Tool |Request count |Count |Displays the total number of requests received by the tool API in the current sampling period (such as 1 hour). This is used to observe changes in tool invocation volume and identify request spikes, drops, or abnormal invocation volume. |
      ||Request distribution (range/exact) |Count |Displays the tool request volume distribution of each group within the current sampling period (such as 1 hour), by different dimensions. Two statistical methods are supported: "Request distribution (range)" and "Request distribution (exact)". This helps you identify exceptions from an overall overview and then locate details step by step.<br><br>> **tip**<br><br><br><br>* > Request distribution (range) and Request distribution (exact) correspond to summary overview and detailed tracing, respectively. We recommend first identifying abnormal ranges using Request distribution (range) and then identifying specific status codes, request paths, APIs, or call sources using Request distribution (exact).<br><br><br>* > The console displays only data actually generated under the current time range and filter criteria. If a certain HTTP status code is not displayed, it indicates no request returned that status code within the current query range. This does not indicate a monitoring data exception.<br><br><br>* > The results displayed on the page are affected by the selected sampling period, time range, and filter criteria.<br><br><br>* **Request distribution (range)** <br><br>   Request distribution (range) aggregates and counts requests after grouping specific attribute values into predefined ranges. You can use it to view the request volume and proportion of each range and quickly assess overall request health.<br><br>   For example, when counting **by HTTP status code ranges**, classify 200, 201, and 206 into `2xx`, 403 and 404 into 4xx, and 500 and 502 into `5xx`.<br><br>* **Request distribution (exact)** <br><br>   Performs detailed counting by specific attribute values of requests. This is used to identify status codes, <br><br>   For example, when counting by **HTTP status code**, the number of requests corresponding to status codes such as 200, 301, 404, and 500 is counted separately. |
      ||Average latency |ms |Displays the average time taken by the tool to process requests in the current sampling period (such as 1 hour). This is used to observe tool response performance and identify overall slowdowns, increased latency, or performance bottlenecks. |
      ||Egress response bandwidth |bit/s |Displays the traffic flowing out of the tool per second within the current sampling period (such as 1 hour). This is used to observe changes in response data traffic and identify excessively large response content, traffic spikes, or outbound bandwidth pressure. |
      |Tool instance resources |CPU usage |% |Displays the CPU utilization of the target tool within the current sampling period (such as 1 hour). This is used to observe the overall CPU load of the tool and identify excessive compute pressure, insufficient instance resources, or the need for scale\-out.<br><br>> **tip**<br><br><br>> This value represents the average CPU usage across all instances associated with the target tool.<br> |
      ||Memory usage |% |Displays the memory utilization of the target tool within the current sampling period (such as 1 hour). This is used to observe the overall memory load of the tool and identify high memory utilization, memory leak risks, or the need for scale\-out.<br><br>**Memory utilization = Actual consumed memory/Maximum consumed memory allowed × 100%.** <br><br>> **tip**<br><br><br>> This metric indicates the average memory utilization across all instances associated with the target tool.<br> |
      ||Number of instances |Count |Displays the number of running instances of the target tool within the current sampling period (such as 1 hour). This is used to observe changes in tool instance scale and identify abnormal instance reduction, scaling exceptions, or insufficient running capacity. |
