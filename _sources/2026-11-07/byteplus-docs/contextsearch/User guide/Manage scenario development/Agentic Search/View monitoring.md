---
title: "View monitoring"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/View_monitoring"
---

ContextSearch integrates with CloudMonitor, allowing you to view various monitoring metrics for the Agentic Search scenario directly in the ContextSearch console or CloudMonitor console, and analyze the scenario's running state in real time. This topic describes how to view monitoring.

<span id="ceKwOpdB"></span>
## Prerequisites

An Agentic Search scenario has been created and initialized. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario) and [Initialize an Agentic Search scenario](https://docs.byteplus.com/en/docs/contextsearch/Initialize_an_Agentic_Search_scenario).

<span id="lW6rWBfA"></span>
## Procedure


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **My Scene**, then click the target Agentic Search scenario.

4. Click the **Performance Monitoring** tab at the top of the page.

   Under the **Monitoring Overview** tab, you can view the scene’s resource metrics and business metrics.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, monitoring information of the last day is displayed. You can view the monitoring data of the last month. You can use the time window on the page to define a custom time range for viewing, accurate to the minute, with a maximum interval of 14 days. ContextSearch also offers quick options for 1 hour, 3 hours, 6 hours, 12 hours, 1 day, 3 days, and 7 days.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you check <strong>chart linkage</strong>, when hovering over any monitoring chart to view the specific value of that item at a certain time, the exact values of other items under the current monitoring category at that time will also display synchronously in their corresponding charts.   </div>
   

   
   <Tabs>
   <Tab zoneid="QAn2zkyXAe" title="Resource metrics">
   <TabTitle>Resource metrics</TabTitle>
   
   
   |**Metric name** |**MetricName**<br><br> |**Unit** |**Subnamespace**<br><br> |**Description** |
   |---|---|---|---|---|
   |CPU usage |ai_node_cpu_usage |% |ai |CPU usage rate at the node where the scene is located. |
   |Memory usage |ai_node_memory_usage |% |ai |Memory usage of the node where the scenario is located. |
   |Disk usage |ai_node_disk_usage |% |ai |Disk usage rate of the node where the scene is located. |
   |GPU usage |ai_node_gpu_usage |% |ai |GPU usage of the node where the scenario is located. |
   |GRAM usage |ai_node_gram_usage |% |ai |GRAM usage rate at the scenario node. |
   
   
   
   </Tab>
   <Tab zoneid="h7kosxYK0x" title="Business metrics">
   <TabTitle>Business metrics</TabTitle>
   
   
   |**Metric name** |**MetricName** |**Unit** |**Subnamespace** |**Description** |
   |---|---|---|---|---|
   |QPS |ai_node_qps |\- |ai |Requests processed per second at the node where the scene is located. |
   |Average response time. |ai_node_mean_reponse_ms |ms |ai |Average response time for requests handled by the node where the scene is located. |
   |Request success rate |ai_node_success_request_percent |% |ai |Request success rate of the node where the scenario is located. |
   |TPS |ai_node_tps |\- |ai |The number of Tokens processed per second by the node where the scene is located. |
   
   
   
   </Tab>
   </Tabs>
