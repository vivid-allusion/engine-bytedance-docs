---
title: "Basic stability capability configuration"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Basic-stability-capability-configuration"
---

This topic mainly introduces configurations and operational recommendations related to basic stability for VKE applications.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Growing containerized workloads can bring greater pressure and more complex challenges to your business system. Stability optimization helps ensure that the system can adapt to increasing demands and support business expansion. VKE, with workloads and Kubernetes clusters as its core, can help you improve business stability without requiring intrusive modifications.

This topic covers basic stability optimization. For more information on stability optimization, see the following topics:


* [Workload stability optimization](https://docs.byteplus.com/en/docs/vke/Workload-stability-optimization)

* [Kubernetes cluster stability optimization](https://docs.byteplus.com/en/docs/vke/Kubernetes-cluster-stability-optimization)


<span id=".5Z-656GA56iz5a6a5oCn"></span>
## Basic stability


|Category |Item |Description |Related documentation |
|---|---|---|---|
|Cluster planning |Configuring control plane high\-availability |Build a highly available control plane by configuring subnets in multiple availability zones. |* [Configuration recommendations for high availability and stability](https://docs.byteplus.com/en/docs/vke/Usage-notes#.56iz5a6a6auY5Y-v55So6YWN572u5o6o6I2Q)<br><br>* [Modifying the subnets of API servers](https://docs.byteplus.com/en/docs/vke/Modifying-API-server-subnets) |
|Add\-on management |Using standard add\-ons provided by VKE |Avoid using third\-party tools for business management. Always deploy standard add\-ons provided by VKE. |[Add-on overview](https://docs.byteplus.com/en/docs/vke/Add-on-overview) |
||Preferring VCI\-based deployment |To avoid add\-on resource overloading and subsequent impact on application functionality, we recommend that you preferentially use **VCI\-based deployment** as the **deployment option** when deploying add\-ons (that is, deploying add\-ons using VCI resources). |* [Add-on overview](https://docs.byteplus.com/en/docs/vke/Add-on-overview)<br><br>* [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on) |
|Node pool management |Managing nodes by using node pools |Manage a group of node resources in a cluster as a node pool. |[Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) |
||Using managed node pools |It is recommended to use managed node pools to manage node resources. Managed node pools provide common fault detection and self\-healing for nodes. |* [Creating managed node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool)<br><br>* [Node check and self-healing in a node pool](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair) |
||Monitoring and increasing quotas |Quota limits apply to VKE resource usage. When the quota consumption is high, increase the quota in time. You can also configure alerting in the [Quota Center](https://console.byteplus.com/quota) so that you can receive notifications before quota depletion and act accordingly in advance. |* [Limits](https://docs.byteplus.com/en/docs/vke/Limits)<br><br>* [How do I increase quotas?](https://docs.byteplus.com/en/docs/vke/How-do-I-increase-a-quota) |
|Enabling observability |Integrating metric monitoring and alerting |Use cloud native observability (basic observability and full\-stack observability) or Cloud Monitor to implement collection, monitoring, and alerting of clusters, basic resources, and application metrics. |* [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability)<br><br>* [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability)<br><br>* [Full-stack observability](https://docs.byteplus.com/en/docs/vke/Cloud-native-observability) |
||Integrating logging |Collect logs of the control plane, workloads, add\-ons, and cluster events into TLS to achieve log and event persistence. |* [Log overview](https://docs.byteplus.com/en/docs/vke/Log-overview)<br><br>* [Configuring and viewing persistent events](https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events) |
||Enabling cluster auditing |Enable cluster auditing to collect cluster operation logs to TLS. |[Cluster auditing](https://docs.byteplus.com/en/docs/vke/Cluster-auditing) |
||Enabling add\-on monitoring |Monitor metrics of common add\-ons, such as Ingress, DNS, and CNI. |* [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability)<br><br>* [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability)<br><br>* [CNI network observability](https://docs.byteplus.com/en/docs/vke/CNI-network-observability) |
||Enabling network and application monitoring |Monitor Layer 4/Layer 7 network traffic metrics and visually manage upstream and downstream calls to achieve network and application observability. |[Full-stack observability](https://docs.byteplus.com/en/docs/vke/Cloud-native-observability) |
||Enabling cluster inspection |Cluster inspection helps identify potential risks in clusters. |[Configuring cluster inspection](https://docs.byteplus.com/en/docs/vke/Configuring-cluster-inspection) |
||Enabling diagnosis |Fault diagnosis provides rapid diagnosis capabilities for cluster resources, such as node pools, nodes, and pods. |* [Node pool diagnosis](https://docs.byteplus.com/en/docs/vke/NodePool-diagnosis)<br><br>* [Node diagnosis](https://docs.byteplus.com/en/docs/vke/Node-diagnosis)<br><br>* [Pod diagnosis](https://docs.byteplus.com/en/docs/vke/Pod-diagnosis) |
