---
title: "Viewing memory monitoring data"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_memory_monitoring_data"
---

You can view memory monitoring data to understand the operation and usage of basic memory metrics, enabling you to quickly identify O&M issues.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">AgentKit memory basic monitoring is free of charge.</div>


<span id="raxCCpOh"></span>
## Note


* You can only view monitoring data when the memory is in the **Available** status. Query\-related limits are as follows:

   * The supported time range for one query is from 5 minutes to 7 days.

   * You can only query monitoring data within the past 15 days. Time ranges exceeding 15 days are not supported.

* The collection frequency for memory metrics is 30 seconds, which means that related monitoring metrics are collected every 30 seconds.


<span id="78DlD99a"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the top menu bar, select the project and region of the target memory.

3. In the left\-side navigation pane, select "Memory".

4. In the memory list, click the name of the target memory.

5. In the monitoring overview area, you can view the corresponding metrics for "Create event" and "Memory recall".

   * **Time filtering range**

      By default, monitoring data from the past 1 hour is displayed. You can customize the time range to filter the period by specifying "Recent" or "Range".

   * **Currently supported metric**

      
      |Category |Metric |Unit |Description |
      |---|---|---|---|
      |Create event |API call count |Count |Indicates the total number of requests received by memory interfaces, such as the **interfaces for adding sessions, events, or profiles** within the statistical period you specify (for example, 1 hour or 1 day). |
      ||Average latency |ms/s |Indicates the average response time for **memory addition requests** of the memory within the statistical period you specify (for example, 1 hour or 1 day). |
      ||Total error rate |% |Indicates the error rate of **memory addition operations**. Total error rate = number of failed operations  **/**  total number of operations within the statistical period you specify (for example, 1 hour or 1 day). |
      |Memory recall |API call count |Count |Indicates the total number of requests of the memory **retrieval interface** within the statistical period you specify (for example, 1 hour or 1 day). |
      ||Average latency |ms |Indicates the average response time of memory **retrieval interface** requests within the statistical period you specify (for example, 1 hour or 1 day). |
      ||Total error rate |% |Indicates the error rate of the memory **retrieval interface**. Total error rate = number of failed operations  **/**  total number of operations within the statistical period you specify (for example, 1 hour or 1 day). |
