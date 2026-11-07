---
title: "Large-scale cluster O&M guarantee"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Large-scale-cluster-OM-guarantee"
---

The stable operation of large\-scale Kubernetes clusters relies on a comprehensive monitoring and alerting system as well as quota management. This topic describes monitoring and alerting configurations and quota management recommendations for large\-scale clusters.

<span id="bzIfoVYx"></span>
## Configure monitoring and alerting

<span id="zEgyx4zl"></span>
### Description

The stable operation of large\-scale Kubernetes clusters relies on a comprehensive monitoring and alerting system. Using VMP as the core monitoring facility, VKE provides multi\-dimensional metric collection and alerting capabilities for the control plane, data plane, network, and workloads.

According to the responsibility model defined in [Shared security responsibility for VKE](https://docs.byteplus.com/en/docs/vke/Shared_security_responsibility_for_VKE) and [Usage notes](https://docs.byteplus.com/en/docs/vke/Usage-notes?lang=en), VKE is responsible for the stability of the Kubernetes control plane, while users need to ensure the stability of the data plane. Therefore, it is crucial to configure comprehensive monitoring and alerting for large\-scale clusters.

<span id="roCpc91g"></span>
### Recommended


1. **Enable VMP\-based observability**: Enable VMP\-based observability for your cluster based on the instructions in [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability?lang=en).

2. **Configure VMP alerts**: Configure key alert rules based on the collected metrics. For the instructions, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Predefined-alerting-rule-templates?lang=en).


<span id="EDeQkouw"></span>
## Plan and manage quotas

<span id="IXuYwEFO"></span>
### Description

When you plan and manage large\-scale clusters, you need to pay attention to various cloud service quotas related to the cluster size and apply for them in advance in the [Quota Center](https://console.byteplus.com/quota/productList). The following table describes core quotas.


|**Category** |**Quota parameter name** |**VKE recommended value/description** |**Purpose description** |
|---|---|---|---|
|Vital Kubernetes Engine |Node |5000 |The maximum number of nodes supported in a single VPC\-CNI cluster. |
||NodePool |100 |The number of node pools supported in a single cluster. |
|ECS |vcpu |Apply as needed |The vCPU quota for each instance family. This directly determines how many ECS instances can be created. |
|VPC |eni |Apply as needed |The number of auxiliary ENIs that can be created in a single region. The number of ENIs that can be mounted varies based on different ECS specifications. This directly affects Pod density in VPC\-CNI mode. |
|EBS |capacity |Apply as needed |The maximum total capacity of various cloud disks. |


<span id="nMpOiIdr"></span>
### Recommended


1. **Apply for quotas**: Manage and increase quotas through the [Quota Center](https://console.byteplus.com/quota/productList) in a centralized manner.

2. **Configure quota alerts**: Configure quota alerts to prevent business scaling failures caused by quota exhaustion.
