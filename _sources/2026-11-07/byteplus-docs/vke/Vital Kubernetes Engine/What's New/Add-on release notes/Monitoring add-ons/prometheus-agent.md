---
title: "prometheus-agent"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/prometheus-agent"
---

The prometheus\-agent add\-on is the monitoring add\-on of the Vital Managed Service for Prometheus (VMP), which collects the monitoring metrics data of Kubernetes clusters for the BytePlus VMP. This topic mainly introduces the change history of the prometheus\-agent add\-on. For more introductions and usage methods related to the add\-on, refer to [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When upgrading the add\-on, the collection of monitoring metrics will be interrupted shortly.</div>


* <div data-tips="true" data-tips-type="tip">After upgrading the add\-on to v2.2.0 and later versions, the re\-installation of versions earlier than v2.2.0 is not supported. If you have such requirements, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210">submit a ticket</a>.</div>



<span id="_2025-03"></span>
## March 2025


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.10.0\-vke.1.24 |v1.24 ≤ Cluster version ≤ v1.30 |Maintained |* Supports selecting DiscoveryRole.<br><br>* Supports adding global Labels for collected metrics.<br><br>* Enables **Add\-on scaling ** by default.<br><br>* Adds a permission configuration toggle for Secret metrics in kube\-state\-metrics. |For details, refer to [Installing add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on). |
|v2.10.0\-vke.1.20 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |* Supports selecting DiscoveryRole.<br><br>* Supports adding global Labels for collected metrics.<br><br>* Enables **Add\-on scaling** by default.<br><br>* Adds a permission configuration toggle for Secret metrics in kube\-state\-metrics. |For details, refer to [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on). |


<span id="_2024-11"></span>
## November 2024


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.9.0\-vke.1.24 |v1.24 ≤ Cluster version ≤ v1.30 |Maintained |* Supports Kubernetes v1.30.<br><br>* Supports atomic writing of histograms.<br><br>* ServiceMonitor uses `role: endpointslices` by default.<br><br>* `additional-monitoring-config` supports more parameters. |ServiceMonitor uses `role: endpointslices` by default, which will cause the `relabel` configuration that previously used the `meta endpoint label` to fail. |
|v2.9.0\-vke.1.20 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |* Supports atomic writing of histograms.<br><br>* ServiceMonitor uses `role: endpointslices` by default.<br><br>* `additional-monitoring-config` supports more parameters. |ServiceMonitor uses `role: endpointslices` by default, which causes the `relabel` configuration that previously used the `meta endpoint label` to fail. |


<span id="_2024-06"></span>
## June 2024


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.8.0\-vke.1.24 |v1.24 ≤ Cluster version ≤ v1.28 |Maintained |* Fixes the issue of duplicate collection of DCP register nodes.<br><br>* Adds the collection of self\-monitoring metrics of the add\-on. |None |
|v2.8.0\-vke.1.20 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |* Fixes the issue of duplicate collection of DCP register nodes.<br><br>* Adds the collection of self\-monitoring metrics of the add\-on. |None |


<span id="_2024-05"></span>
## May 2024


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.7.0\-vke.1.24 |v1.24 ≤ Cluster version ≤ v1.28 |Maintained |Supports VKEObservabilityRole. |None |
|v2.7.0\-vke.1.20 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports VKEObservabilityRole. |None |


<span id="_2024-03"></span>
## March 2024


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.6.0\-vke.1.24 |v1.24 ≤ Cluster version ≤ v1.28 |Maintained |Supports configuration of ExternalLabels. |Using the ExternalLabels feature will double the active time series in the corresponding workspace. It will recover after one hour. Check whether the workspace volume meets the requirements in advance. For details, refer to [Custom metrics label](https://docs.byteplus.com/en/docs/vke/Customing_metrics_labels). |
|v2.6.0\-vke.1.20 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports configuration of ExternalLabels. |Using the ExternalLabels feature will double the active time series in the corresponding workspace. It will recover after one hour. Check if your workspace volume meets requirements in advance. For details, refer to [Custom metrics label](https://docs.byteplus.com/en/docs/vke/Customing_metrics_labels). |
|v2.5.0\-vke.1.24 |v1.24 ≤ Cluster version ≤ v1.28 |Maintained |* Supports Kubernetes v1.28.<br><br>* Upgrade the kube\-state\-metrics add\-on, which supports more metrics and dimensions. |* When upgrading the add\-on, dashboard data of some metrics may be interrupted for 1 to 2 minutes.<br><br>* After upgrading the add\-on, the active time series of the cluster's workspace will increase by approximately 10% for a short period. It will recover after one hour. Check in advance whether the maximum volume of active time series in the workspace is sufficient.<br><br>* The `kube_*_annotations` and `kube_*_labels` metrics in the kube\-state\-metrics add\-on are no longer exposed, and therefore cannot be queried. For details, refer to [Cannot query kube_namespace_label metrics](https://docs.byteplus.com/en/docs/vke/Cannot-query-the-kube_namespace_label-metric).<br><br>* `The kube_verticalpodautoscaler_.* metrics have been deprecated.` |
|v2.5.0\-vke.1.20 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Upgrade the kube\-state\-metrics add\-on, which supports more metrics and metric dimensions. |* When upgrading the add\-on, some metrics will stop update for 1\-2 minutes.<br><br>* After upgrading the add\-on, the active time series of the workspace associated with clusters will temporarily increase by about 10%. It will return to the original level after one hour.Check in advance if the workspace's maximum capacity for active time series is sufficient.<br><br><br> |


<span id="_2024-02"></span>
## February 2024


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.4.0 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Prohibit scheduling of DCP register nodes. |None |


<span id="_2023-10"></span>
## October 2023


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.3.0 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports writing the collected metrics in external Prometheus. |None |
|v2.2.0 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |* Supports configuration of metrics collection rules and deprecation of unnecessary metrics.<br><br>* The "instance label" has been removed from the kube\-state\-metrics metrics.<br><br>* A new RDMA collection rule has been added. |After upgrading the add\-on to this version, the re\-installation of the add\-on of earlier versions is not supported. If you have such requirements, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210). |


<span id="_2023-09"></span>
## September 2023


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.1.0 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Standardizes the naming of API fields in the add\-on configuration. |None |


<span id="_2023-08"></span>
## August 2023


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.0.5 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Adds `ai.*` Labels for kube_pod_labels. |None |


<span id="_2023-07"></span>
## July 2023


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.0.4 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports collecting Nydus metrics. |None |
|v2.0.3 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |* Supports ECS/VCI Role authentication. Users do not need to set workspace authentication information on the add\-on configuration interface.<br><br>* Supports cluster workspaces. Users do not need to set a workspace on the add\-on configuration interface. |None |


<span id="_2023-06"></span>
## June 2023


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.0.2 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports Kubernetes v1.26. |None |
|v2.0.1 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports service discovery through Service/Pod annotations. |None |


<span id="_2023-05"></span>
## May 2023


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.0.0 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |* Supports prometheus\-operators (such as ServiceMonitor) for collecting Kubernetes Custom Resource Definitions (CRDs).<br><br>* Improves production\-readiness so that the add\-on can collect metrics from ultra\-large\-scale clusters. |None |


<span id="_2023-02"></span>
## February 2023


|Versions |Compatibility with Kubernetes version |Version Status |Description |Impact |
|---|---|---|---|---|
|v1.0.6 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports the collection of DCGM metrics on the Vital Container Instance (VCI). |None |


<span id="_2022-12"></span>
## December 2022


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.5 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |The add\-on architecture is optimized. |None |


<span id="_2022-11"></span>
## November 2022


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.4 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports topology spreading configuration. |None |


<span id="_2022-10"></span>
## October 2022


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.3 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports the collection of mGPU metrics. |None |


<span id="_2022-09"></span>
## September 2022


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.2 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Adds VKE cluster ID for metrics. |None |


<span id="_2022-08"></span>
## August 2022


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.1 |v1.20 ≤ Cluster version ≤ v1.24 |Maintained |Supports hot updates of collection configuration. |None |


<span id="_2022-07"></span>
## July 2022


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.0 |v1.20 ≤ Cluster version ≤ v1.24 |No longer maintained |Supports the basic collection of Prometheus monitoring metrics. |None |
