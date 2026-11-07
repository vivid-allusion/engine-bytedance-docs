---
title: "Workspace monitoring"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Workspace_Monitoring"
---

On the Monitoring page, you can view the trends of write, query, and storage metrics of a workspace within a specified time range. The self\-monitoring capabilities of the workspace help you identify issues such as rate limiting and invalid metrics during self\-troubleshooting.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The Cloud Monitor service has been activated. For details, see [What is Cloud Monitor?](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor)

* A Vital Managed Service for Prometheus (VMP) workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id=".55uR5o6n5aSn55uY"></span>
## Monitoring dashboard


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Click **Workspace** in the left navigation pane, find the target workspace in the workspace list, and then click the workspace name to go to the Overview page of the workspace.

3. Click **Monitoring** in the left navigation pane to view the monitoring dashboard of the workspace.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">We recommend that you enable preset Cloud Monitor alert rules. You can enable preset alert rules by following on\-screen instructions displayed at the top of the console.</div>



   * **Monitoring Dashboard**: includes **write**, **query** and **storage** dashboards. You can view monitoring data within the last day by default.

   * **Time configuration**: You can configure the time range for queries, which can be accurate to the minute. You can query data in the last 30 days at most, with the maximum query time range being 15 days each time.

   * **Chart linkage**: After you select chart linkage, you can quickly view the metrics and values at the same time point of all charts.

   * **View more data**: The Cloud Monitor metrics page opens. You can view details on the monitoring dashboard.

   * **Create alert strategy**: The **Create alert strategy** page opens. You can configure alerting as needed.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aedd070db0c549df72e6abbf4eef8765.png) </span>

<span id=".55uR5o6n5oyH5qCH"></span>
## Metrics

The metrics of the VMP workspace include write, query, and storage metrics. For more details on the metrics, refer to [Metric query](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_Prometheus).
