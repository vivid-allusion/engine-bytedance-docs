---
title: "O&M overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/OM-overview"
---

Cluster O&M is an O&M management feature that improves cluster stability, reduces management costs, and enables self\-healing. This topic describes the role of cluster O&M in VKE and the differences among common O&M methods.

<span id="AOMPv2iq"></span>
## Role of cluster O&M

As Kubernetes clusters continue to scale and business microservice architectures grow increasingly complex, manual daily inspections and troubleshooting can no longer meet high business continuity requirements. The health of underlying physical nodes, stability of core control plane components, availability of network and storage plugins, and compliance of workload configurations all face severe round\-the\-clock challenges.

Therefore, introducing systematic and automated cluster O&M is essential. By using the built\-in cluster O&M capabilities provided by VKE, you can achieve the following core values:


* **Prevent issues before they occur**: Promptly detect potential security risks, configuration defects, and resource bottlenecks in the cluster.

* **Improve troubleshooting efficiency**: When anomalies occur, significantly shorten MTTR through clear event alerts and remediation suggestions.

* **Reduce management costs**: Offload routine O&M tasks to automated systems, freeing O&M personnel to focus on core business architecture optimization.


<span id="mLumLftU"></span>
## O&M method comparison

VKE provides multiple O&M features for different operational needs. The following table summarizes their purposes and key differences.


|**Comparison dimension** |Automatic O&M |**O&M events** |Cluster inspection |
|---|---|---|---|
|Core positioning |User\-initiated automatic O&M or upgrade features for the cluster control plane, Kubernetes patch versions, and add\-on versions. |System\-initiated proactive notification and collaborative handling feature for cluster control plane risks. |User\-initiated diagnostics and suggestions for cluster resources, configurations, and workloads. |
|O&M object |Container cluster control plane and data plane resources, including cluster control plane, Kubernetes patches, and component versions. |Events that may affect cluster stability, security, and availability when anomalies occur in the container cluster control plane, infrastructure, and system patches. |Cluster data plane resources, including user\-side events such as user quotas, resource status, and Kubernetes best practice compliance. |
|Driving method |Periodic scanning, actively triggered by users. |Proactive scanning or event\-triggered execution, with no user action required. |On\-demand or periodic scanning, initiated by users. |
|Interaction method |View in console. |View in console and push to user\-specified channels. |View results in the console, obtain inspection reports, or receive pushes through user\-specified channels. |
|Typical scenario |* Control plane routine O&M.<br><br>* Kubernetes patch automatic upgrade.<br><br>* Add\-on automatic upgrade. |* APIServer certificate is about to expire.<br><br>* Control plane scheduled maintenance.<br><br>* High\-risk security vulnerability (CVE). |* Quota check for cluster\-related resources.<br><br>* Checking for cluster/node status and resource usage.<br><br>* Checking for cluster features, component status, and security configurations.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For the inspection items supported by cluster inspection, see Inspection item descriptions and remediation suggestions.</div><br> |
|Related documentation |[Automatic O&M](https://docs.byteplus.com/en/docs/vke/Operation-and-maintenance-configuration) |[O&M events](https://docs.byteplus.com/en/docs/vke/OM-events) |[Configuring cluster inspection](https://docs.byteplus.com/en/docs/vke/Configuring-cluster-inspection) |
