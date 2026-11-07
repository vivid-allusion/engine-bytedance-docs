---
title: "Monitoring VCI with VMP"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Monitoring-VCI-instances-using-Vital-Managed-Service-for-Prometheus"
---

Basic VCI monitoring can be implemented based on VMP. This topic describes how to configure collection rules for VCI monitoring metrics and how to query metrics.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud\-native observability has been enabled for the VCI business cluster based on VCI. For details, see [Enabling cloud-native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The prometheus\-agent add\-on in the VCI business cluster has been upgraded to version v2.2.0 or later. For details, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/prometheus-agent).


<span id=".6YWN572u55uR5o6n6YeH6ZuG6KeE5YiZ"></span>
## Configuring collection rules

After you have enabled cloud\-native observability for the VCI business cluster and installed the corresponding add\-ons, you need to configure the relevant collection rules to collect metrics properly. The following procedure describes how to configure collection rules in VCI scenarios. For details, see [Observability](https://docs.byteplus.com/en/docs/vke/VKE-observability) and [AI resources observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability).


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar of the cluster management page, click **Observability settings**.

5. Enable the observability add\-ons as needed and edit the VCI metric configuration. For detailed steps and descriptions, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability) and [AI resources observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In VCI scenarios, you mainly use the <strong>Container service</strong> and <strong>AI resources</strong> observability add\-ons.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Non\-GPU metric settings (such as CPU, memory, and network) can be edited in the VKE add\-ons.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">GPU\-related metric settings can be edited in the <strong>AI resources</strong> observability add\-ons.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed monitoring metrics supported by VCI, see <a href="https://docs.byteplus.com/en/docs/vke/Getting-VCI-metrics-through-virtual-nodes">Getting VCI metrics through virtual nodes</a> and <a href="https://docs.byteplus.com/en/docs/vke/VCI-GPU-metrics">VCI GPU monitoring metrics</a>.   </div>
   


<span id=".5p-l6K-i55uR5o6n5oyH5qCH"></span>
## Querying metrics

After configuring the monitoring collection rules, you can query VCI metrics in the VMP console. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, click **Explore** to go to the Explore page.

4. In the upper\-right corner of the page, specify the **workspace**, **time range**, and **data refresh method** for the metric query.

5. Use PromQL query statements to query VCI metrics.

   * Query VCI metrics via virtual nodes by using `$metric_name{node="$virtual_node_name"}`, for example, `container_cpu_usage_seconds_total{node="vci-node1-cn-beijing-a"}`.

   * Query VCI GPU metrics by using `$metric_name{pod="$VCI_instance_name"}`, for example, `DCGM_FI_DEV_DEC_UTIL{pod="vci-ini2-d75d77bc5-82lch"}`.

6. Click **Query** to query the metrics and display the metrics dashboard.
