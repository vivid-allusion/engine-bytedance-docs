---
title: "vci-virtual-kubelet"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet"
---

The vci\-virtual\-kubelet add\-on schedules and runs Vital Container Instance (VCI) instances through virtual nodes. Virtual nodes are created by default after the add\-on is deployed.Virtual nodes are created by default after the add\-on is deployed. This topic mainly describes the change history of the vci\-virtual\-kubelet add\-on.

For more information about add\-ons, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id="0pghJQOP"></span>
## July 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|1.48.0 |Cluster version ≤ v1.36 |Being maintained |* The VCI inventory\-aware scheduling feature is optimized.<br><br>* The NetworkPolicy feature can be enabled for VCIs.<br><br>* Dynamic EFS mounting is supported for VCIs. |None |
|1.47.0 |Cluster version ≤ v1.34 |No longer maintained |VCI creation performance is optimized for passwordless image pulls. |None |


<span id="EzHKeeSP"></span>
## June 2026


|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|1.46.0 |Cluster version ≤ v1.36 |No longer maintained |The Kubernetes dependency is upgraded to v1.36. |None |


<span id="vIvml1fx"></span>
## March 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.45.0 |Cluster version ≤ v1.34 |No longer maintained |Kubernetes dependencies are upgraded to v1.34. |None |


<span id="tH9oPFi3"></span>
## January 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.44.0 |Cluster version ≤ v1.32 |No longer maintained |Kubernetes dependencies are upgraded to v1.32. |None |


<span id="C547TBZH"></span>
## October 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.43.0 |Cluster version: v1.30 or earlier |No longer maintained |The method of calculating resources for the VCI inventory\-aware scheduling feature is optimized. |None |


<span id="pvluv7dN"></span>
## September 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.42.0 |Cluster version: v1.30 or earlier |No longer maintained |* GNR models support local data disks.<br><br>* GPU exclusive mode can be enabled when starting VCI instances. |None |


<span id="76mWyhpu"></span>
## June 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.40.1 |Cluster version: v1.30 or earlier |No longer maintained |Custom image repository addresses can be configured for VCI pods. |None |


<span id="3sAxn0BY"></span>
## May 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.40.0 |Cluster version: v1.30 or earlier |No longer maintained |A new instance fault O&M scenario named DPUHostNotReady is added. |None |


<span id="RA6Cwv2o"></span>
## April 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.39.0 |Cluster version: v1.28 or earlier |No longer maintained |The image cache configuration is ignored, and VCI instances are created if the specified image caches of VCI pods do not exist or are unavailable. |None |


<span id="QpiQ2s3A"></span>
## March 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.38.0 |Cluster version: v1.28 or earlier |No longer maintained |* Node affinity can be configured for VCI inventory\-aware scheduling.<br><br>* Fixed the issue where mutually dependent environment variables of pods could not be parsed correctly during configuration.<br><br>* Kubernetes dependencies are upgraded to v1.30. |None |


<span id="ZXRFRTI5"></span>
## February 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.37.0 |Cluster version: v1.28 or earlier |No longer maintained |* Sidecars can be injected into VCI instances based on OpenKruise SidecarSet.<br><br>* The metrics related to instance specifications can be exposed. |None |


<span id="xkDnou4j"></span>
## January 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.36.0 |Cluster version: v1.28 or earlier |No longer maintained |The size of a single log can be configured for log collection in VCI instances. |None |


<span id="SpqBXfjv"></span>
## December 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.35.0 |Cluster version: v1.28 or earlier |No longer maintained |Image caches can be specified for VCI instances. |None |


<span id="tnBgb7G6"></span>
## November 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.34.0 |Cluster version: v1.28 or earlier |No longer maintained |Multiple availability zones and specifications can be configured for VCI instances. |None |


<span id="ZDzRTguX"></span>
## October 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.33.0 |Cluster version: v1.28 or earlier |No longer maintained |* The VCI pod status synchronization performance is optimized.<br><br>* The in\-place upgrade of env is supported. |None |


<span id="1lywlayS"></span>
## September 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.32.0 |Cluster version: v1.28 or earlier |No longer maintained |The vm.watermark_scale_factor parameter can be configured for VCI instances. |None |


<span id="HkiYse5j"></span>
## July 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.31.0 |Cluster version: v1.28 or earlier |No longer maintained |The memory usage of the add\-on is optimized. |None |


<span id="xpsuhBy7"></span>
## June 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.30.0 |Cluster version: earlier than v1.28 |No longer maintained |* DNS nameservers can be configured for custom image pulling in VCI instances.<br><br>* Time zones can be configured for VCI instances. |None |


<span id="XHpJmRpC"></span>
## 

<span id="_2024-05"></span>
## May 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.29.0 |Cluster version: v1.28 or earlier |No longer maintained |* VCI pod exec enables you to set both `stderr and tty to true` at the same time.<br><br>* The in\-place restart of a VCI pod is supported when its single container image is being updated. |None |
|1.28.2 |Cluster version: v1.28 or earlier |No longer maintained |* vePFS Container Storage Interface (CSI) is supported.<br><br>* node\-local\-dns is supported. |None |


<span id="_2024-04"></span>
## April 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.28.0 |Cluster version: v1.26 or earlier |No longer maintained |* Pod IP addresses remain unchanged during workload upgrades (for example, a container image is being updated).<br><br>* The issue of pod status rollback is fixed. |None |
|1.27.2 |Cluster version: v1.26 or earlier |No longer maintained |Multiple pod subnets can be used to create instances, and the subnet with the largest number of available IP addresses can be used to create instances. |None |


<span id="_2024-03"></span>
## March 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.27.1 |Cluster version: v1.26 or earlier |No longer maintained |Ephemeral volumes in Kubernetes are supported. |None |
|1.27.0 |Cluster version: v1.26 or earlier |No longer maintained |* VCI inventory\-aware scheduling is supported.<br><br>* The configurations for creating secondary/primary network interface cards (NICs) in VKE and VCI are unified.<br><br>* The issue where kubectl exec on VCI pods becomes unresponsive in kubectl 1.29+ is fixed. |None |


<span id="_2024-01"></span>
## January 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.26.1 |Cluster version: v1.26 or earlier |No longer maintained |The vci\-profile global configuration feature is supported. |None |
|1.26.0 |Cluster version: v1.26 or earlier |No longer maintained |General\-purpose and cache\-type NAS can be configured. |None |
|1.25.4 |Cluster version: v1.26 or earlier |No longer maintained |GPU driver version can be selected for workloads. |None |


<span id="_2023-12"></span>
## December 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.25.3 |Cluster version: v1.26 or earlier |No longer maintained |Metrics are optimized, and the container startup time metric is added. |None |
|1.25.1 |Cluster version: v1.26 or earlier |No longer maintained |* The issue where a pod fails to be created when configured with an empty imagePullSecret is fixed.<br><br>* The displayed status information about a pod after it fails to be created is optimized. |None |


<span id="_2023-11"></span>
## November 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|1.25.0 |Cluster version: v1.26 or earlier |No longer maintained |The issue where a ConfigMap and a Secret in a Project Volume do not take effect when they are mounted on a container as files is fixed. |None |
