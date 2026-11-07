---
title: "Built-in dashboard"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Dashboard-overview"
---

Vital Managed Service for Prometheus (VMP) provides multiple types of built\-in dashboards to facilitate viewing monitoring information. This topic describes how to view a built\-in dashboard.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace is created. For more details, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Cloud services or custom business is integrated with VMP. For more details, refer to [Access guide](https://docs.byteplus.com/en/docs/vmp/Monitoring-Guide).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. Click **Monitor dashboard** on the left navigation bar to go to the Monitor dashboard page.

4. Select the dashboard that you want to view in the left\-side **Dashboard list** panel, and configure the workspace and refresh method to view the monitoring information of the specified dashboard. For the basic operations on built\-in dashboards, refer to [Basic operations](https://docs.byteplus.com/en/docs/vmp/Basic_operations).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2aec42d6425e3758625bf395953cd9c8.png) </span>


|No. |Description |
|---|---|
|1 |The dashboard list. The dashboard name starts with the abbreviation of a service name. For example, `vke-xxx` indicates [the dashboard of VKE](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Kubernetes-Engine). Click a dashboard name in the list to view the details of the dashboard. |
|2 |Select a data source for the dashboard, which is a VMP workspace, and configure the query time range, refresh method, and refresh interval. |
|3 |The details of the dashboard. You can select cloud service resources. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In addition to system built\-in dashboards, it is recommended to use Grafana to view metrics and create dashboards. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster">Deploying Grafana and accessing workspaces in the VKE cluster</a>.</div>


* <div data-tips="true" data-tips-type="tip">For specific descriptions of built\-in dashboards for different services, refer to the documentation of the corresponding service. For example, for the description of the monitoring dashboards for VKE, see <a href="https://docs.byteplus.com/en/docs/vke/Basic-observability">Basic observability</a>.</div>
