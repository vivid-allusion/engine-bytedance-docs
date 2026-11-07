---
title: "Using dashboards"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_dashboard"
---

VKE provides preset dashboards with features such as data comparison across corresponding periods and dashboard statement copying. This topic describes how to use dashboards.

<span id="qgWhxn3c"></span>
## Comparing data across periods

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In built\-in dashboards, only some metric cards support data comparison across periods. Please refer to the console for details.</div>


Built\-in dashboards support the cross\-period comparison feature, which allows you to compare data between a specified period of time and the current period of time. This makes it easy to understand data changes between two time periods.


1. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, find the target dashboard, move the pointer over the metric card, and then click ... in the upper\-right corner of the metric card. Then, click **Compare** in the drop\-down menu.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69d3ca47eaa1bcfbc4926a78f69c815d.png) </span>

3. In the **Compare Time** drop\-down menu, select the time period for comparison to view the chart of data comparison between the current period of time and the specified period of time. In the chart, the solid line represents data for the current time, and the dashed line represents data for the specified period of time.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c7655c1e19a541e1b61cd837212e4ee3.png) </span>


<span id="UviDubHD"></span>
## Copying dashboard statements

You can copy PromQL statements from built\-in dashboards. These statements allow you to understand the data definitions in the dashboards or build a custom monitoring dashboard in a self\-managed monitoring system (such as self\-managed Grafana).


1. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, find the target dashboard, move the pointer over the metric card, and then click ... in the upper\-right corner of the metric card. Then, click **Copy expression** in the drop\-down menu.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2a7e604c788c32c78b6a7818c7966b24.png) </span>

3. (Optional) You can use the copied PromQL statement to create a dashboard in a self\-managed monitoring system (such as self\-managed Grafana).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can deploy self\-managed Grafana in a VKE cluster or Elastic Compute Service (ECS) instance. For details, see the following topics:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster">Deploying Grafana in a VKE cluster and integrating Grafana with a workspace</a>   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace">Deploying Grafana in an ECS instance and integrating Grafana with a workspace</a>   </div>
