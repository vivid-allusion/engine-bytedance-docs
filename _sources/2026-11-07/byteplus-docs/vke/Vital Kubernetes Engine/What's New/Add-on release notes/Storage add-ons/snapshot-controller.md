---
title: "snapshot-controller"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/snapshot-controller"
---

snapshot\-controller is a storage snapshot add\-on that supports storage snapshots in Vital Kubernetes Engine. This topic includes the change logs of the snapshot\-controller add\-on.

For more information and usage instructions on add\-ons, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id="RD5NJJIb"></span>
## March 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v8.4.0\-vke.1 |All versions |Maintained |The WatchList feature is enabled by default to optimize APIServer memory usage. For details, see [Streaming List responses](https://kubernetes.io/blog/2025/05/09/kubernetes-v1-33-streaming-list-responses/). |The client\-side processing latency slightly increases. |


<span id="F8vB7nOk"></span>
## January 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v8.4.0 |All versions |No longer maintained |Synchronized to the latest community version, resolving known CVE issues. |None |


<span id="hmSGwXhy"></span>
## December 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v6.2.3\-vke.1 |All versions |Maintained |Node affinity, taint toleration, and resource limits can be configured. |None |


<span id="5CrjrDUX"></span>
## June 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v6.2.3 |All versions |No longer maintained |ARM hosts are supported. |None |


<span id="_2023-02"></span>
## February 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v6.2.1 |All versions |No longer maintained |Supports PVC snapshot capability. |None |
