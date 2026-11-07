---
title: "Operating system monitoring"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-operating-system-monitoring-data"
---

This topic describes how to view the monitoring data of the operating system for an Elastic Compute Service (ECS) instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**.

3. In the top navigation bar, select the target region.

4. Click the name of the target instance in the resource list to go to the monitoring details page. Click the **OperateSystemMonitor** tab to view the metric data of the operating system for the specified instance.

   * Monitoring data: You can view monitoring data within the last day by default. You can also specify a custom time range, which is accurate to minutes.

   * chart linkage: After you select chart linkage, you can quickly view the metrics and values at the same time point of all charts.

   * Time window: You can drag the slider below a chart to select a time window.

      * You can query data in the last 60 days at most. The metric storage duration varies based on different cloud services. For more details, refer to [Cloud service metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).

      * The query time range can be up to 15 days each time.
