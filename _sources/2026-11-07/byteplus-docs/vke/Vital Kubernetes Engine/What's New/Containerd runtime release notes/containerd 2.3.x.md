---
title: "containerd 2.3.x"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Containerd_2-3"
---

VKE supports using containerd 2.3.x on Kubernetes v1.36 or later. This topic describes the main feature updates, deprecated features, and deprecated APIs related to containerd 2.3.x.

<span id="334a837a4d31"></span>
## Features

containerd 2.3 provides the following main capabilities in storage, image handling, runtime management, and observability:


* Adds Mount Manager to centrally manage the filesystem mount lifecycle, including device formatting, mount activation, and cleanup of invalid mounts.

* Supports mounting subdirectories of image volumes and unpacking images in parallel. This improves the flexibility and concurrency of image preparation.

* Enhances the Sandbox API to update Pod Sandbox resource configurations.

* Supports parallel loading of Shim. This reduces the waiting time for recovering a large number of running containers after a containerd restart.

* Enhances the metrics capabilities of the Container Runtime Interface (CRI). It supports querying Pod Sandbox metrics and computing and caching runtime metrics in the background.

* Enhances the Node Resource Interface (NRI). It provides independent Pod and container lifecycle events, WebAssembly (WASM) plugins, metrics, and tracing capabilities.

* NRI lifecycle events have been changed from the unified `StateChange` to independent RPCs. When an old external ttRPC plugin returns `Unimplemented`, the runtime can fall back to `StateChange`, but a deprecation alert is generated. Old WASM plugins do not support this fallback mechanism and must be rebuilt using the new NRI SDK.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more changes, see <a href="https://github.com/containerd/containerd/releases/tag/v2.3.0">containerd 2.3.0 release notes</a>.</div>


<span id="748e67721d48"></span>
## Configuration changes


* containerd 2.3 uses Config v4. VKE provides an independent standard Config v4 template for containerd 2.3. In this way, containerd does not need to automatically migrate old configurations during loading.

* Config v4 migrates the original top\-level `[grpc]`, `[ttrpc]`, `[debug]`, and `[metrics]` configurations to the corresponding Server or Metrics Plugin configuration. When you use custom configuration generators, parsing tools, or configuration modification scripts, adapt them to the new plugin paths accordingly.

* The runc v1.4.x used by containerd 2.3.x changes how `pids.limit` is handled: When it is explicitly set to `0`, it no longer means "unlimited" but is treated as an actual limit value, equivalent to `1` in systemd environments. Check the relevant runtime configurations before the upgrade. If you need to leave the process count unlimited, set it to `-1` or do not specify the field.

* When you upgrade containerd 1.6.x or 2.1.x to 2.3.x, the system only migrates key configurations supported by VKE, such as the sandbox image, SystemdCgroup, GPU runtime, and Nydus\-related configurations, and does not guarantee that all custom configurations are fully preserved. Before the upgrade, verify the custom containerd configurations of the node pool. For details, see [Configuring containerd for node pools](https://docs.byteplus.com/en/docs/vke/Configuring_containerd_for_node_pools).


<span id="37c49add5805"></span>
## Deprecated features and APIs


* The support for the NRI v0.1 plugin has been removed. When using custom NRI plugins, first confirm that the plugin version is compatible with containerd 2.3. Custom plugins using the NRI v0.1 API must be upgraded to the current NRI API. If the upgrade cannot be completed in the short term, consider using `v010-adapter` for compatibility. Before using the adapter, verify plugin functionality and stability in a test environment.

* NRI plugin names can only contain letters, digits, and special characters (`-_.+`). Plugins whose names contain other characters cannot be registered.

* cgroup v1 has been marked as deprecated. cgroup v2 is recommended.

* The `enable_cdi` parameter has been deprecated. containerd 2.3 still recognizes this parameter, but explicitly disabling the Container Device Interface (CDI) generates a deprecation alert. CDI is planned to always be enabled starting with containerd 2.4. Environments that rely on disabling CDI must complete a compatibility assessment in advance.

* The experimental capability of restoring containers from a checkpoint image via CRI `CreateContainer` is disabled by default, has been deprecated, and is planned for removal in a later version. If existing workloads still rely on this capability, you can temporarily set `enable_experimental_restore_via_create to true` and set `enable_criu to true` and make sure that the CRIU version is not earlier than 3.16. This approach is for transitional use only, and you must migrate to the `RestorePod` API defined in KEP\-5823 later.

* The `shim.Command` API has been deprecated and is planned for removal in a later version. Custom shims must migrate to the Shim Bootstrap Protocol.
