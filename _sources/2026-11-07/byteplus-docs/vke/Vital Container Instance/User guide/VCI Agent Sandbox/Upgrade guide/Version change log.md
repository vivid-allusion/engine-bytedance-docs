---
title: "Version change log"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Version_change_log"
---

This topic provides a version change log for the agent\-sandbox template in Helm.

<span id="Ie7NVALW"></span>
## June 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.4.6\-vke.1 |v1.26 ≤ Cluster version<br><br> |Maintained |* Community feature alignment<br><br>   * The prewarming pool's object model has evolved from ‌direct Pod binding‌ to ‌Sandbox binding‌.<br><br>   * Sandbox Service creation is now optional‌.<br><br>* VCI enhancements<br><br>   * In\-place updates‌ of Sandbox container images are supported, eliminating the need for Pod recreation.<br><br>   * Snapshot creation upon Sandbox suspension is now ‌optional‌ (previously default).<br><br>* Helm Chart template optimizations<br><br>   * The workload type of agent\-sandbox\-controller changed from StatefulSet to Deployment.<br><br>   * Helm values ‌are aligned with community standards‌.<br><br>* Bug fixes<br><br>   Fixed an issue where the E2B List API did not support pagination. |* Due to the workload type change from ‌StatefulSet‌ to ‌Deployment‌, ‌existing Sandboxes cannot be created, deleted, or modified during add\-on upgrades‌.<br><br>* In the old version, a Service is automatically created for each Pod, and this behavior cannot be disabled. In the new version, Service creation is optional. The Helm Chart's `defaultSandboxService` parameter defaults to `true` (creating Pod Services) to ensure upgrade compatibility.<br><br>* Helm Chart template parameters have changed. After selecting this version, you need to configure the relevant parameters. For details, please see the [installation guide](https://docs.byteplus.com/en/docs/vke/Installation_guide).<br><br><br> |


<span id="x4ZI3AaW"></span>
## May 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.1.1\-vke.3 |v1.26 ≤ Cluster version ≤ v1.36 |Maintained |Certain E2B interfaces are supported. |None |


<span id="MfCA9bzQ"></span>
## April 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.1.1\-vke.2 |v1.26 ≤ Cluster version ≤ v1.36 |Maintained |Fixed an issue where the Sandbox could not automatically enter the Running state after Pod startup in certain scenarios. |None |


<span id="6Kdc1tjM"></span>
## March 2026


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.1.1\-vke.1 |v1.26 ≤ Cluster version ≤ v1.36 |Maintained |The first release of Helm Chart for VCI Agent Sandbox capabilities:<br><br><br>* Sandbox lifecycle management is supported.<br><br>* Sandbox data persistence is supported.<br><br>* Image archiving is supported. |None |
