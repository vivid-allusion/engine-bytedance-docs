---
title: "Cluster monitoring"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-monitoring"
---

Vital Kubernetes Engine (VKE) has integrated with Cloud Monitor to provide monitoring and alerting capabilities for VKE\-related resources. This topic describes how to view the monitoring information of a VKE cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VKE cluster has been created. For instructions on how to create a cluster, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Make sure that the current account has obtained the relevant permissions on the Cloud Monitor service.

* Make sure that the Cloud Monitor add\-on metrics\-collector has been installed in the cluster.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar of the VKE console, click **Cluster**.

3. Find the target cluster and click  **`...`**  \> **View monitoring** in the Actions column. Then, you are redirected to the monitoring page of the Cloud Monitor console. On this page, you can view the monitoring information of the current cluster.


<span id=".5p-l55yL55uR5o6n"></span>
## Viewing monitoring data

You can specify a custom time range to view the visual monitoring charts of cluster\-related monitoring items, which helps you understand the health status of the cluster. Monitoring items include cluster CPU usage, cluster CPU utilization, cluster memory usage, cluster memory utilization, and the number of nodes.

<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

To configure an alert policy for the cluster, go to the **Alert policy ** page and click **Create alert policy**. On the page that appears, configure an alert rule. For parameter configurations, see [Creating alert strategies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).
