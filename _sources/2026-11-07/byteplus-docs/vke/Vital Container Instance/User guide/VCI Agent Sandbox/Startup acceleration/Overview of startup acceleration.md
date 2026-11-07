---
title: "Overview of startup acceleration"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Startup_acceleration"
---

This topic describes solutions for sandbox startup‌ acceleration in the VCI Agent Sandbox, including image caching and warm pools.

<span id="U5qXyCe2"></span>
## Background

Sandbox application scenarios have ‌extreme requirements for startup speed‌:


* **Real\-time interaction scenarios**: AI agents create sandboxes instantly during sessions for code execution. Users are latency\-sensitive, and even ‌delays of seconds degrade the user experience‌.

* **High\-concurrency scaling scenarios**: Short\-lived tasks claim sandboxes in batches during traffic spikes. Creation lags cause queuing bottlenecks‌.

* **Multi\-tenant isolation scenarios**: Each tenant/session requires independent sandboxes. High creation frequency ‌amplifies cold\-start costs‌.


Native Pods take dozens of seconds to transition from creation to the Ready state, involving phases such as scheduling, image pulling, container initialization, and health checking. Image pulling and container initialization are primary bottlenecks‌.


|**Startup phase** |**Proportion of time consumed** |**Main overhead** |
|---|---|---|
|Scheduling and resource allocation |Low |Cluster scheduler decision and node resource preparation. |
|Image pulling |High |Image layer downloads from CR. The latency is strongly related to image size and network bandwidth. |
|Container startup |Moderate |Creation of strong Kata isolation environments, Rootfs mounting, and process initialization. |
|Application readiness |Moderate |Application process startup, health check passed, and Service endpoint updates. |


<span id="Ac8xnQDD"></span>
## Solution overview

VCI Agent Sandbox provides two acceleration solutions for sandbox startup: **ImageCache** and **SandboxWarmPool**.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In practice, the two solutions are ‌not mutually exclusive. One typically serves as the primary approach while the other acts as a secondary enhancement.</div>



|Acceleration solution |Core mechanism |Typical benefit |Application scenario |Constraints |
|---|---|---|---|---|
|[Image cache](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache-overview) |Preloads container images into cloud disk snapshots. When a Pod starts, it directly restores image data from the snapshot, skipping the process of pulling an image from the image repository to shorten the startup time. |The time consumption in the image pulling phase is significantly reduced, especially for GB\-level AI images. |General or AI inference scenarios where the image size is large, the image update frequency is low, or the same image is reused by a large number of Pods.  |Requires pre\-creating caches per image. Caches have retention periods and capacity quotas. |
|[Warm pool](https://docs.byteplus.com/en/docs/vke/Warm_pools) |Declaratively pre\-creates a batch of sandbox instances with the same status via a CRD. Workloads claim ready instances from the pool via a SandboxClaim. |The cold start latency is reduced to the sub\-second level, and the end\-to\-end delivery time is optimized by more than 90%. |Latency\-sensitive scenarios, such as AI agents, code interpreters, and interactive sessions. |Requires sustained resource reservation to maintain the pool capacity. Currently, it cannot be used together with the system disk state persistence capability. |


<span id="YtOA6C83"></span>
## Solution comparison

The following table compares VCI Agent Sandbox's two startup acceleration solutions with traditional sandbox creation without acceleration:


|**Comparison dimension** |**No acceleration used** |**Image cache** |**Warm pool** |
|---|---|---|---|
|Accelerated phases |None |Image pulling |Image pulling, container startup, and readiness check |
|Startup latency |Tens of seconds |Seconds |Sub\-seconds |
|Resource usage |On\-demand allocation |On\-demand allocation and minimal snapshot storage |‌Persistent warm Pods‌ (scales linearly with pool size) |
|Integration complexity |\- |Low (one annotation) |Medium (3\-CRD collaboration) |
|Compatibility with system volume snapshots |Compatible |Compatible |Currently not compatible  |
|Suitable scale |\- |Any scale |Medium or large scale, with a predictable and stable concurrency level |
