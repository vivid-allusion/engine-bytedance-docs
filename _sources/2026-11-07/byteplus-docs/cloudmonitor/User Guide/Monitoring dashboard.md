---
title: "Monitoring dashboard"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Monitoring-dashboard"
---

Cloud Monitor provides preset dashboards for some cloud products. If the single\-instance dashboard in a product console does not meet your business requirements, you can use a preset dashboard to view multi\-instance monitoring scenarios.

<span id="fd5c759e"></span>
## Limits


* The data storage duration varies based on different cloud services. For more details, refer to [Supported cloud services](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).

* You can select up to 50 resources for a monitoring dashboard.

* The query interval can be up to 14 days on a monitoring dashboard.

   * The time aggregation interval varies based on different query intervals.

      * If 0 < query interval ≤ 6 hours, the aggregation interval is 30 seconds.

      * If 6 hours < query interval ≤ 1 day, the aggregation interval is 1 minute.

      * If 1 day < query interval ≤ 7 days, the aggregation interval is 10 minutes.

      * If 7 days < query interval ≤ 14 days, the aggregation interval is 60 minutes.


<span id="9fb3c3cf"></span>
## View preset monitoring dashboards

This topic provides an example on how to view the monitoring data of multiple Elastic Compute Service (ECS) instances in the Cloud Monitor console.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Monitoring Dashboard**.

3. On the Dashboard Best Practice page, click the + icon before **Elastic Compute** and then click **ECS/default**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e48ce73768cd57b87eb599eabd51be20.png) </span>

4. On the **ECS** monitoring dashboard page, select the query interval, resource ID, instance, and disk. Then, you can view the corresponding monitoring dashboards.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you select resource IDs, you can select a region and resources. You can select up to 50 resources.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can move the pointer over a chart to view metric values, and sort metrics by value.   </div>
   

&nbsp;


&nbsp;

&nbsp;

&nbsp;
