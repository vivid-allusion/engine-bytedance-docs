---
title: "rdma-device-plugin"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/rdma-device-plugin"
---

As a Remote Direct Memory Access (RDMA) device add\-on, the rdma\-device\-plugin add\-on manages RDMA network interface cards (NICs) and enables pod containers to use RDMA devices. This topic includes the change logs of the rdma\-device\-plugin add\-on.

For more information about the add\-on, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[Public Beta] This add\-on is currently in public beta.</div>


<span id="RGvwy2fK"></span>
## April 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.6.2\-vke.1 |Cluster version: v1.24 or later |Maintained |* Supports bytenic4.<br><br>* Supports liveness health checks. |None |


<span id="orfwANR6"></span>
## September 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.5.1\-vke.12 |All versions |Maintained |* Supports the RDMA shared\-host mode.<br><br>*  Enforces that the number of resources reported by each node is greater than 0. |None |


<span id="7sytfWm7"></span>
## April 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.5.1\-vke.10 |All versions |Maintained |* Supports excluding vRDMA NICs.<br><br>* The RBAC permissions on pods are scoped down to pods/status.<br><br>* Fixes the issue with the automatic calculation of the maximum upper limit in shared\-multi mode.<br><br>* Shared\-multi supports the `/29` mask. |None |


<span id="_2024-07"></span>
## July 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.5.1\-vke.8 |All versions |Maintained |The shared mode supports `/28 subnets` for RDMA NICs. |None |


<span id="_2023-07"></span>
## July 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v3.5.1\-vke.1 |All versions |Maintained |The rdma\-device\-plugin add\-on is added. |None |
