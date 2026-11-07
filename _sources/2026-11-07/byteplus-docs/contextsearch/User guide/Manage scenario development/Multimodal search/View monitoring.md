---
title: "View monitoring"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/View_multimodal_monitoring"
---

ContextSearch has integrated with Cloud Monitor, allowing you to view various monitoring metrics for multimodal search scenarios directly in the ContextSearch console or the Cloud Monitor console. This enables real\-time analysis of the scenario's running state. This topic describes how to view monitoring.

## Prerequisites

Created and initialized multimodal search scenarios. For detailed operations, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario) and [Initialize a multimodal search scenario](https://docs.byteplus.com/en/docs/contextsearch/Initialize_a_multimodal_search_scenario).

## Procedure

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. In the left navigation pane, select **My Scene**, then click the target multimodal search scenario.

4. Click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77957c2465a295f7c4c33f66bd77ad27.png) the icon on the right side of the page to open the **Scene configuration** panel, select the **Monitoring** tab, and view the scenario’s resource and business metrics.

   > **tip**

   * > By default, monitoring information of the last day is displayed. You can view the monitoring data of the last month. You can use the time window on the page to define a custom time range for viewing, accurate to the minute, with a maximum interval of 14 days. ContextSearch also offers quick options for 1 hour, 3 hours, 6 hours, 12 hours, 1 day, 3 days, and 7 days.

   * > If you check **chart linkage**, when hovering over any monitoring chart to view the specific value of that item at a certain time, the exact values of other items under the current monitoring category at that time will also display synchronously in their corresponding charts.

   **Resource metrics**

|**Metric name** |**MetricName**<br><br> |**Unit** |**Subnamespace**<br><br> |**Description** |
   |---|---|---|---|---|
   |CPU usage |ai_node_cpu_usage |% |ai |CPU usage rate at the node where the scene is located. |
   |Memory usage |ai_node_memory_usage |% |ai |Memory usage of the node where the scenario is located. |
   |Disk usage |ai_node_disk_usage |% |ai |Disk usage rate of the node where the scene is located. |
   |GPU usage |ai_node_gpu_usage |% |ai |GPU usage of the node where the scenario is located. |
   |GRAM usage |ai_node_gram_usage |% |ai |GRAM usage rate at the scenario node. |

   **Business metrics**

|**Metric name** |**MetricName**<br><br> |**Unit** |**Subnamespace**<br><br> |**Description** |
   |---|---|---|---|---|
   |QPS |ai_node_qps |\- |ai |Requests processed per second at the node where the scene is located. |
   |Average response time. |ai_node_mean_reponse_ms |ms |ai |Average response time for requests handled by the node where the scene is located. |
   |Request success rate |ai_node_success_request_percent |% |ai |Request success rate of the node where the scenario is located. |
   |TPS |ai_node_tps |\- |ai |The number of Tokens processed per second by the node where the scene is located. |
