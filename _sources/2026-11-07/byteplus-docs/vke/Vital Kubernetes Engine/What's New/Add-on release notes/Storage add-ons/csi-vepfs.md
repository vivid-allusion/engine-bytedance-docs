---
title: "csi-vepfs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-vepfs"
---

The csi\-vepfs is a PFS service add\-on that enables container clusters to use the service through the standard CSI interface. This topic describes the change history of the csi\-vepfs add\-on.

For more details on the add\-on, see [Managing add-ons](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id="cUsJ2FVB"></span>
## May 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.18.0 |All versions |Maintained |It provides an add\-on configuration page, where you can specify custom node deployment settings and resource configuration for the add\-on. |None |


<span id="JBSIcMog"></span>
## April 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.17.0 |All versions |Maintained |* The WatchList feature is enabled by default to optimize APIServer memory usage. For details, see [Streaming List responses](https://kubernetes.io/blog/2025/05/09/kubernetes-v1-33-streaming-list-responses/).<br><br>2. Upgraded the csi sidecar version, synchronized to the latest community version, and resolved known CVE issues. |The client\-side processing duration slightly increases. |


<span id="4kD7ubvj"></span>
## July 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.16.0 |All versions |Maintained |Any volumeHandle can use the same "mountpoint + subpath" combination. |None |


<span id="_2024-10"></span>
## February 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.13.0 |All versions |Maintained |* Supports Ubuntu 20 and Ubuntu 22.<br><br>* Supports TOP gateway bootstrapping.<br><br>* Fixes the issue where the VKE node ID was not the node IP, resulting in unsuccessful restore operations in case of vePFS client pod failures. |None |


<span id="7VK5CTHs"></span>
## October 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.11.0 |All versions |Maintained |* Newly added support for defining a file system subpath in the persistent volume and mounting it as a volume.<br><br>* Fixed the issue where restarting kubelet might cause the pod to be stuck in the terminating status when using vepfs volume.<br><br>* Operation and maintenance capabilities are enhanced. |None |


<span id="_2024-08"></span>
## August 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.9.0 |All versions |Maintained |* The ECS third\-generation model supports the use of veLinux 1.0 image with kernel version 5.10.<br><br>* Fixed the issue where CSI Node could not ensure idempotence for multiple NodePublishVolume operations.<br><br>* Fixed the issue where if a VKE node failed to join the vepfs management cluster, it could not join another management cluster.<br><br>* Fixed the issue where vepfs client pod caused the node to be unable to scale\-in. |None |


<span id="_2024-07"></span>
## July 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.8.0 |All versions |Maintained |* Optimizes the policy for mounting and scheduling vePFS: Associates with VKE scheduler, supporting vePFS scheduling awareness. The pods bound with different mount services will not be repeatedly scheduled to the same node. Guarantees that only one vePFS client\-end exists on a single node, to improve user experience and business continuity.<br><br>* Optimized the consistency between vePFS clusters and members of VKE clusters after restarting the csi controller.<br><br>* The remove CLI command supports specifying the \-\-id and \-\-ip parameters to cover scenarios using non\-default VKE node names. |None |
