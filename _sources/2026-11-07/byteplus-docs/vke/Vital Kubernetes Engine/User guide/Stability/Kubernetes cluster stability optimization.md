---
title: "Kubernetes cluster stability optimization"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Kubernetes-cluster-stability-optimization"
---

This topic introduces configuration and operational recommendations related to Kubernetes cluster stability in the context of VKE stability optimization.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Growing containerized workloads can bring greater pressure and more complex challenges to your business system. Stability optimization helps ensure that the system can adapt to increasing demands and support business expansion. VKE, with workloads and Kubernetes clusters as its core, can help you improve business stability without requiring intrusive modifications.

This topic covers Kubernetes cluster stability optimization. For more information on stability optimization, see the following topics:


* [Basic stability capability configuration](https://docs.byteplus.com/en/docs/vke/Basic-stability-capability-configuration)

* [Workload stability optimization](https://docs.byteplus.com/en/docs/vke/Workload-stability-optimization)


<span id=".6ZuG576k5rC05L2N5LiO6IqC54K55rC05L2N"></span>
## Cluster resource utilization and node resource utilization

After cluster creation is complete, cluster resource utilization information is available. You can statically adjust the number of nodes in the cluster based on this resource utilization information. For details, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). 

After nodes are added to a cluster, information such as node\-level resource utilization and the amount of resources requested by Pods becomes available. For details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes). 

<span id=".6ZuG576k5LiO57uE5Lu25Y2H57qn"></span>
## Cluster and add\-on upgrade

We recommend upgrading existing clusters and add\-ons to their latest versions to benefit from new features and bug fixes. For details, see the following topics:


* [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster)

* [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on)


In addition, we recommend recreating any Kubernetes resources that have a GA (Generally Available) version available but are currently using a Beta version. Typical Kubernetes resources are as follows:


|Resource |API version |Kubernetes version |
|---|---|---|
|HPA |autoscaling/v2beta2 |=1.20.x |
||autoscaling/v2 |≥1.24.x |
|CronJob |batch/v1beta1 |=1.20.x |
||batch/v1 |≥1.24.x |


<span id=".6ZuG576k5Yqo5oCB5Ly457yp"></span>
## Cluster autoscaling

A managed cluster supports dynamic scaling of nodes within the cluster by using Cluster Autoscaler (CA). CA uses a specified scheduling policy to dynamically scale out nodes within a node pool with autoscaling enabled based on the number of pending pods in the cluster. It also monitors node resource utilization to achieve dynamic scale\-in. For information about how CA works, see [Cluster Autoscaler best practices](https://docs.byteplus.com/en/docs/vke/Cluster-Autoscaler-best-practices).

<span id=".5L2_55So5ZG95ZCN56m66Ze06ZqU56a76LWE5rqQ"></span>
## Resource isolation with namespaces

In multi\-tenant or multi\-application hybrid deployment scenarios, namespaces are typically used to isolate workloads. Kubernetes allows limiting the available resource quotas for namespaces. For information about how to configure resource quotas for different namespaces, see [Setting resource quotas](https://docs.byteplus.com/en/docs/vke/Setting-ResourceQuotas).

<span id=".5L2_55SoLXZjaS3pmpTnprvotYTmupA="></span>
## Resource isolation with VCI

When workloads run on ECS nodes, pods may experience resource contention and mutual interference, especially for network bandwidth and other resources that are not managed by Kubernetes. VCI instances run on virtual nodes, with each VCI instance exclusively occupying a virtual node. If better isolation and elasticity are critical to your applications, we recommend running workloads on VCI instances. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

<span id=".5L2_55SoLXZjaS3kuI4tZWNzLea3t-WQiOW8ueaApw=="></span>
## VCI and ECS combination for hybrid elasticity

[ResourcePolicy scheduling](https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling) allows workloads to run simultaneously on VCI and ECS. When ECS resources are insufficient, CA is triggered to dynamically scale out the cluster, which provides more flexible elastic resource scheduling and ensures business stability.

<span id=".5L2_55So6Ieq5a6a5LmJ57O757uf6ZWc5YOP"></span>
## Custom operating system images

Custom operating system images can speed up node provisioning, which is critical for the speed and success rate of large\-scale node scaling scenarios.

If your cluster needs to scale from tens to thousands of nodes in a short time, we recommend using custom operating system images in node pools. Custom operating system images can be created using ECS or Docker. For details, see [Creating custom images based on ECS](https://docs.byteplus.com/en/docs/vke/Creating-a-custom-image-based-on-ECS) or [Creating custom images based on Docker](https://docs.byteplus.com/en/docs/vke/Creating-a-custom-image-based-on-Docker).

For other regular scenarios, using public images is sufficient. For more information, see [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).

<span id=".6ZuG576k5Z6C55u05YiG54mH"></span>
## Vertical cluster sharding

Deploying different businesses in separate clusters can effectively isolate faults and risks. Problems in a single cluster will not affect the operational status of other clusters. This isolation mechanism prevents cluster\-level single points of failure or local issues from spreading to the entire system. Additionally, a multi\-cluster architecture enables more flexible scaling strategies. You can independently scale the resources or the number of nodes in a specific cluster based on business needs without affecting other clusters. Each cluster can also enforce independent security policies and access control, which reduces potential security risks.

<span id=".6ZuG576k5rC05bmz5YiG54mH"></span>
## Horizontal cluster sharding

A single cluster has workload limits. When the cluster load gradually increases and approaches the upper limit, you can build multiple identical business clusters to offload workloads. For information about scaling managed VKE clusters, configuring node pool quota limits, and setting add\-on limits, see [Limits](https://docs.byteplus.com/en/docs/vke/Limits).

<span id=".5aSa5Zyw5Z-f6YOo572y"></span>
## Multi\-region deployment

By deploying clusters in different geographic locations, you can ensure that one or more clusters continue to provide services in the event of regional disasters, such as natural disasters, power outages, and network failures. This geographic dispersion mitigates the risk of single points of failure. Additionally, distributing clusters nationwide or globally enables better load balancing. User requests can be routed to the nearest cluster, thereby reducing latency, spreading workloads, and improving user experience. For information about regions where VKE is available, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones).
