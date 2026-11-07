---
title: "keda"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/keda"
---

The keda add\-on provides an autoscaler driven by Kubernetes events to enhance the capability of elastic scaling. This topic describes the change history of the keda add\-on.

For more information about add\-ons and how to use them, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management).

<span id="ZkYA55AJ"></span>
## September 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v2.13.0\-vke.4 |v1.24 ≤ Cluster version ≤ v1.36 |Being maintained |* Supports configuration of add\-on resource usage, node affinity, and taint toleration.<br><br>* High\-availability configuration is enabled by default. If you require higher availability, scale out the add\-on.<br><br>* Fixes the compatibility constraints between the add\-on version and the cluster version. |None |
|v2.13.0\-vke.3 |All versions |No longer maintained |Metric collection can be configured, and preset dashboards are available. |None |


<span id="_2025-03"></span>
## March 2025


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v2.13.0\-vke.2 |All versions |No longer maintained |The authentication method for querying VMP is optimized. |None |


<span id="_2025-02"></span>
## February 2025


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v2.13.0\-vke.1 |All versions |No longer maintained |The keda add\-on is officially released for the first time and supports event\-driven autoscaling. |None |
