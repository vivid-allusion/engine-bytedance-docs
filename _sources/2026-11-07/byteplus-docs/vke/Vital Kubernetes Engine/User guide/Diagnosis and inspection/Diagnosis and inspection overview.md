---
title: "Diagnosis and inspection overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/AIOps-overview"
---

VKE provides the diagnosis and inspection feature to perform O&M and management on clusters. The feature accumulates the rich O&M experience and solutions of Kubernetes container clusters within BytePlus. This helps you efficiently perform O&M and management on clusters.

<span id="W8PwbmLk"></span>
## Feature overview

A native Kubernetes cluster involves worker nodes, networks, storage, and various system add\-ons due to its complex architecture and long links. As business continuously grows, O&M teams often encounter pain points such as difficulty in fault identification during sudden business interruptions, slow manual fixing for abnormal underlying node hardware, and difficulty in promptly detecting potential cluster configuration risks.

The cluster diagnosis and inspection feature is a one\-stop solution to address the preceding pain points. It standardizes scattered troubleshooting operations and creates an end\-to\-end assurance system that achieves prevention before an incident, self\-healing during an incident, and identification after an incident. This helps you quickly locate issues, automatically fix faults, and proactively prevent risks in complex cluster environments.

The diagnosis and inspection feature can help you resolve the following issues:


* **Sudden business failure troubleshooting**: When a business application suddenly becomes inaccessible or experiences network latencies, you can use the fault diagnosis feature to quickly perform drill\-down analysis to determine whether the issue lies at the node layer, Pod layer, or Ingress layer. This accurately pinpoints the source of the exception.

* **Underlying infrastructure self\-healing**: When a node encounters GPU hardware failures, kernel deadlocks, or system host exceptions, the system can use the check and self\-healing feature to achieve unattended automatic isolation and recovery. This prevents failed nodes from continuously affecting business instances.

* **Periodic cluster health checks**: Before business deployment, before major event protection, or during routine maintenance, you can use the risk inspection feature to proactively identify potential risks of clusters, such as security configuration non‑compliance and resource quota saturation. This eliminates issues before they occur.


<span id="tjsao0yH"></span>
## Diagnosis

The diagnosis feature can quickly identify common issues of cluster resources and provide fix suggestions. It mainly provides the following features:


|Diagnostic object |Diagnostic content |
|---|---|
|[Node pool diagnosis](https://docs.byteplus.com/en/docs/vke/NodePool-diagnosis) |It applies to common issues of node pools, such as issues with the node pool status, node pool and related service quotas, and node pool autoscaling. |
|[Node diagnosis](https://docs.byteplus.com/en/docs/vke/Node-diagnosis) |It applies to common issues of nodes, such as issues with the node resource, node kernel, node version, node status, and node network. |
|[Pod diagnosis](https://docs.byteplus.com/en/docs/vke/Pod-diagnosis) |It applies to common pod issues, such as those related to resources, status, and images. |
|[Ingress diagnosis](https://docs.byteplus.com/en/docs/vke/Ingress_diagnosis) |It helps you identify risks in Ingress resources within VKE clusters. Ingress instance diagnosis, add\-on diagnosis, and CLB diagnosis are included. |


<span id="R2SJN3gA"></span>
## Check and self\-healing

In a container cluster, nodes are the underlying infrastructure that hosts business, and their running status directly determines application stability. However, during actual O&M, nodes may become unavailable due to various reasons such as underlying hardware failures, kernel deadlocks, system add\-on exceptions, and GPU disconnection.

Entirely relying on manual troubleshooting not only results in slow response but may also cause prolonged business interruptions. [Node inspection and self-healing](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair?lang=en) can effectively address these pain points. By using the "automated monitoring and repair" mode, it achieves early detection, immediate mitigation, and quick repair of node issues. This reduces downtime from minutes to seconds and significantly improves system robustness.

<span id="latcHRxF"></span>
## Risk inspection

Risk inspection helps you discover potential risks and security issues in VKE clusters and provides fix suggestions. It enables you to promptly discover and fix existing issues in clusters. This ensures the stable and secure operation of your business. It mainly provides the following features:


|Feature category |Inspection object |Inspection content |
|---|---|---|
|[Inspection](https://docs.byteplus.com/en/docs/vke/Configuring-cluster-inspection?lang=en) |cluster |Check the configurations required for normal and stable cluster operation, such as deletion protection, high availability, audit logs, security groups, and CoreDNS add\-on. |
||Nodes |Check the status of cluster nodes to promptly identify nodes in abnormal status, and ensure the availability of cluster resources. |
||Resource utilization |Check the utilization of various cluster resources, such as cluster utilization, node utilization, and pod utilization. |
||ResourceQuota |Check the quota usage of various cluster resources, such as the CLB quota, node quota, and node pool quota. |
|[Baseline inspection](https://docs.byteplus.com/en/docs/vke/Baseline-inspection?lang=en) |Nodes |Based on security standards, baseline inspection provides security inspection for cluster nodes, enabling the timely detection of insecure configurations in cluster nodes. |
|[Application inspection](https://docs.byteplus.com/en/docs/vke/Application-inspection?lang=en) |Cluster resources such as the Workload, Pod, and ConfigMap |Based on security standards and container security best practices, application inspection can promptly detect and block unsafe configurations to prevent applications from being attacked or exploited. This ensures the stable and secure operation of your business. |


<span id=".5qOA5p-l57uT5p6c54q25oCB6K-05piO"></span>
## Inspection result status descriptions

After cluster inspection or diagnosis, the system generates a report. The following table describes the status of inspection results in the report.


|Status |Description |
|---|---|
|Compliant |The check is passed, and no operations need to be performed. |
|Not passed |Issues exist and need to be addressed at the earliest opportunity. This prevents cluster or business failures caused by these issues. |
|Warning |If issues exist, you can choose to address them. In most cases, the issues need to be analyzed based on the actual cluster or service situation. |
|Error |An error is reported during the check. The service may encounter an exception. We recommend that you try again. |
