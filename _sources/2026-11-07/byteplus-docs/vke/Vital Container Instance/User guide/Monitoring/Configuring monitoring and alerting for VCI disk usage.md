---
title: "Configuring monitoring and alerting for VCI disk usage"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-the-monitoring-and-alerting-of-VCI-disk-usage"
---

This topic describes how to configure disk usage monitoring and alerting for VCIs.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

When a VCI pod uses an EBS volume, the disk space may become fully utilized as the application runs over time. To address the problem, VCI supports configuring disk usage monitoring and alerting policies for VCI pods. This helps proactively detect related risks and prevent business disruption due to insufficient disk space.

Since VCI pods run on virtual nodes instead of physical servers, disk resources are associated with individual pods rather than nodes. Therefore, to monitor the disk usage of VCI pods, you need to configure pod\-level disk monitoring and alerting. VCI supports pod disk usage monitoring and alerting based on VMP or Cloud Monitor.

<span id=".5L2_55So5omY566hLXByb21ldGhldXMt5pyN5Yqh"></span>
## Using VMP

<span id=".5a-55o6l5pyN5Yqh"></span>
### Connecting to the service

Before configuring VCI pod disk usage monitoring and alerting with VMP, you need to connect to the VMP service. For details, see [Monitoring VCI with VMP](https://docs.byteplus.com/en/docs/vke/Monitoring-VCI-instances-using-Vital-Managed-Service-for-Prometheus).

For the disk\-related monitoring metrics supported by VCI, see the **Volume** table in [Getting VCI metrics through virtual nodes](https://docs.byteplus.com/en/docs/vke/Getting-VCI-metrics-through-virtual-nodes#.5a2Y5YKo5Y23).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">EBS volumes can serve as both the system volume and data volumes for VCI pods. You can distinguish them by the value of the <code>volume_type</code> label:</div>



* <div data-tips="true" data-tips-type="tip"><code>system</code>: A system volume.</div>


* <div data-tips="true" data-tips-type="tip"><code>data</code>: A data volume.</div>



<span id=".55uR5o6n"></span>
### Monitoring

After connecting to VMP, you can query the monitoring metrics for VCI pod disk usage in the VMP console. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, click **Explore** to go to the Explore page.

4. In the upper\-right corner of the page, specify the **workspace**, **time range**, and **data refresh method** for the metric query.

5. Use PromQL statements to query VCI pod disk metrics.

   For example, to query the system volume usage of the VCI pod with ID `vci-3vvac********`, use the following query statement:

   ```SQL
   kubelet_volume_stats_used_bytes{vci_instance_id="vci-3vvac********",volume_type="system"}/kubelet_volume_stats_capacity_bytes{vci_instance_id="vci-3vvac********",volume_type="system"} * 100 
   ```
   

6. Click **Query** to query the metrics and display the metrics dashboard.


<span id=".5ZGK6K2m"></span>
### Alerting

After connecting to VMP, you can configure alerting rules based on query statements and trigger policies in the VMP console. For details, see [Creating alerting rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, click **Alert Center** \> **Alert rule**.

4. On the **Alert rule** page, select **Create** \> **Create manually** to configure parameters based on the system prompts and your actual requirements. For details, see [Creating alerting rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).

   For example, to query the system volume usage of the VCI pod with ID `vci-3vvac********`, you can use the following **query statement**:

   ```SQL
   sum((kubelet_volume_stats_used_bytes{vci_instance_id="vci-3vvac********"}/kubelet_volume_stats_capacity_bytes{vci_instance_id="vci-3vvac********"}) * 100) by (vci_instance_id, volume_type)
   ```
