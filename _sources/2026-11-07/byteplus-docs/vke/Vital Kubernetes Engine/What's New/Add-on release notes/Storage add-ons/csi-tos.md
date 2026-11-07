---
title: "csi-tos"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-tos"
---

The csi\-tos add\-on is a Torch Object Storage (TOS) service add\-on. It supports the standard CSI interface, enabling container clusters to use TOS services. This topic includes the change logs of the csi\-tos add\-on.

<span id="xXzIhUsU"></span>
## Usage instructions

For csi\-tos add\-on upgrade risks and upgrade verification, refer to: [csi-tos add-on upgrade](https://docs.byteplus.com/en/docs/vke/csi-tos_add-on_upgrade). For more information and usage instructions for the add\-on, refer to [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id="WR8GXSve"></span>
## Version changes

<span id="ug8Jxnmi"></span>
### June 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.0.1 |All versions |Being maintained |The directory for client temporary files on the node can be specified. |No |


<span id="5WrEM45r"></span>
### October 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.0.0 |All versions |Being maintained |* Remove the dependency on Kubelet API to fix the OOM issue caused by a large amount of Pods in completed status on the nodes.<br><br>* Converged ServiceAccount permissions. |No |


<span id="_2024-09"></span>
### September 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.2.9 |All versions |Being maintained |Fixed an issue where the client\-end Pod blocked CA scale\-in in the cluster autoscaler (CA) scenario. |No |


<span id="_2024-07"></span>
### July 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.2.8 |All versions |Being maintained |* Fix the issue of TOS client pods remaining due to frequent cluster node scaling by CA, including cleaning up existing pods in Terminating and CrashLoopBackOff states in the cluster, and removing finalizers from existing FUSE client Pods during the graceful shutdown of csi\-tos\-node.<br><br>* Upgraded CSI spec version to v1.9.0.<br><br>* Upgraded sidecar image version: livenessprobe upgraded to v2.12.0; csi\-node\-driver\-registrar upgraded to v2.10.0.<br><br>* Turn on pprof through Unix Domain Socket.<br><br>* The default read speed at the TOS client is optimized. If you do not specify the `parallel_count` parameter, `-oparallel_count=20` is added by default.<br><br>* Adjust csi\-tos\-node log level to 2 to avoid printing a large amount of invalid information.<br><br>* Add trace module to add trace information for key paths.<br><br>* Adjust the graceful exit wait time of Fuse client\-end Pod to 60 seconds. |* After the upgrade, the finalizer of the stock FUSE client\-end Pods will be removed. The stock will be restored to the new nodes. However, because the key files do not exist, the FUSE client\-end Pods in the CrashLoopBackOff status will eventually be cleared.<br><br>* After completing the upgrade, helm will create a Job, clearing the Pods in the cluster that are in Terminating status but whose corresponding nodes no longer exist.<br><br>* The graceful exit wait time of the FUSE client\-end Pods will change to 60 seconds from the original default 30 seconds.<br><br>* If you have specified `parallel_count`, the specified value will be used. Otherwise, `-oparallel_count=20` will be added by default. |


<span id="_2024-06"></span>
### June 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.7 |All versions |Being maintained |* Fixed the issue where TOS client\-side pods caused CA scale\-in failure.<br><br>* Fixed the issue where TOS client\-end Pods remain after node recovery in IP reuse scenarios. |No |


<span id="_2024-03"></span>
### March 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.6 |All versions |Being maintained |* Adjust the default value for the limit range of Fuse client pods.<br><br>* If Fuse client pods fail to start, they will not be cleared. |Adjusted the default value for limit range of Fuse client pod:<br><br>```Yaml```<br>```# CPU request for fuse client pod.```<br>```fuse_pod_cpu_request: "100m"```<br>```# CPU limit for fuse client pod.```<br>```fuse_pod_cpu_limit: "6"```<br>```# Memory request for fuse client pod.```<br>```fuse_pod_memory_request: 200Mi```<br>```# Memory limit for fuse client pod.```<br>```fuse_pod_memory_limit: "6Gi"```<br> |


<span id="_2024-01"></span>
### January 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.5 |All versions |Being maintained |Fixed the issue where Fuse client pods could not be scheduled on the nodes with taints. |No |


<span id="_2023-11"></span>
### November 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.4 |All versions |Being maintained |* It is compatible with the scenario where the Handle and name of the stock pv volume are different.<br><br>* Check whether the tos `<url>:<bucket><path>` corresponding to the same volumeHandle is consistent. If inconsistent, then prohibit mounting to avoid potential problems.<br><br>* Fixed the issue where Node used a large amount of CPU resources. |The v0.2.4 version starts to officially support pod\-level fault recovery. If you want to use this feature, you need to add annotation for pod: `vke.volcengine.com/csi-inject : true`. |
|v0.2.2 |All versions |No longer maintained |Supports pod\-level fault recovery. |* Creating PVs requires adding the `nodeStageSecretRef` field, which has the same content as `nodePublishSecretRef`.<br><br>* It is compatible with the stock PV. However, it is incompatible if the volume handle and stock PV name differ.<br><br>* Add fuse pod resource requirement configuration. If not configured, use the following default value. If the request node resources configured are insufficient, then the requirement can be removed to prioritize starting fuse pod.<br><br>   ```yaml```<br>```   # CPU request for fuse client pod.```<br>```   fuse_pod_cpu_request: "100m"```<br>```   # CPU limit for fuse client pod.```<br>```   fuse_pod_cpu_limit: "2"```<br>```   # Memory request for fuse client pod.```<br>```   fuse_pod_memory_request: 100Mi```<br>```   # Memory limit for fuse client pod.```<br>```   fuse_pod_memory_limit: "2Gi"```<br>```   ```<br>    |


<span id="_2023-06"></span>
### June 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.1 |All versions |No longer maintained |Fixed the issue where mounting fails if the target multi\-level subdirectory does not exist. |No |


<span id="_2023-05"></span>
### May 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.2.0 |All versions |No longer maintained |* Fixed the issue where mounting subdirectories failed in some scenarios.<br><br>* Fixed the issue where the volume (PV) mounting failed but Pod started successfully. |No |


<span id="_2022-09"></span>
### September 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.1.1 |All versions |No longer maintained |Fixed an issue in which csi\-tos could not umount when the log collection add\-on collected files inside the TOS volume, causing the pod to be stuck during termination. |No |
