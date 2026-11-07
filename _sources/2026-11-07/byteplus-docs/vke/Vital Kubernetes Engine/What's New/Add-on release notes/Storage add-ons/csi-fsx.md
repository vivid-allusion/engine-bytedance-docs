---
title: "csi-fsx"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-fsx"
---

The csi\-fsx is a general\-purpose FSX storage add\-on. It enables container clusters to use file systems that support the FSX client through the standard Container Storage Interface (CSI). This topic includes change logs of the csi\-fsx add\-on.

For more information about add\-ons and how to use them, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id="tj2y0GQm"></span>
## June 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.0.0 |v1.24 ≤ Cluster version ≤ v1.36 |Maintained |* Supports features such as rolling upgrades, canary upgrades, and multi‑environment isolation for FSX clients based on the new version of the FSXSet architecture.<br><br>* Supports mounting via the DMC unified mount point. |* Before upgrading to this version, you need to install the fsxset\-controller add\-on first.<br><br>* After the add\-on is running stably, you can uninstall the fsx\-service add\-on.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more information, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_FSX_add-on_feature_optimization_and_fsx-service_add-on_sunsetting">[Product update] fsx\-service deprecation notice</a> and <a href="https://docs.byteplus.com/en/docs/vke/Migrating_FSX_clients">Migrating FSX clients</a>.</div><br> |


<span id="kTzg5lRg"></span>
## January 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.6.1 |Cluster version: v1.24 or later |Maintained |The issue where a pod is stuck in the ContainerCreating state during kubelet restarts is fixed. |None |


<span id="WrH660I8"></span>
## October 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.5.0 |Cluster version: v1.24 or later |Maintained |* TOS authentication via IRSA is supported (no static credentials is required).<br><br>* ARM architecture is supported. |None |


<span id="qkq9PYTS"></span>
## September 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.4.0 |Cluster version: v1.24 or later |Maintained |EFS is supported. |None |


<span id="N34cK6MF"></span>
## August 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.3.0 |All versions |No longer maintained |Hosts with the ARM architecture are supported. |None |


<span id="JyB0Culo"></span>
## April 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.2.0 |All versions |No longer maintained |FileNAS is supported. |None |


<span id="cwgyZtyw"></span>
## January 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v0.1.0 |All versions |No longer maintained |* vePFS access points are supported.<br><br>* TOS is supported.<br><br>* Permissions on the global directory can be modified. |None |


&nbsp;

&nbsp;
