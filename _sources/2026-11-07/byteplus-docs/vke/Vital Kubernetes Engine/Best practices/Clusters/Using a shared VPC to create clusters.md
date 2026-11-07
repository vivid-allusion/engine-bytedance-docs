---
title: "Using a shared VPC to create clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_a_shared_VPC_to_create_clusters"
---

VKE allows you to create clusters by using a shared VPC, which enables you to create and manage cloud resources in the same VPC. This topic describes how to create a VKE cluster by using a shared VPC.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This VPC feature is currently in beta. Contact your account manager to enable the feature and obtain permissions to view the corresponding documentation.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The shared VPC enables multiple accounts to share a single VPC. With this feature, multiple accounts can create and manage cloud resources in the same VPC. This simplifies network planning and centralized cloud resource management. It also helps simplify network architecture and reduce network O&M costs.


&nbsp;

* **Resource owner**: The owner of the shared VPC, which is the initiator of the shared VPC.

* **Resource user**: The user of the shared VPC, which is the recipient of the shared VPC. Resource users can use shared subnets to create and manage cloud resources.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about the shared VPC feature, see <a href="https://docs.byteplus.com/en/docs/vpc/Shared-VPC-Overview">Shared VPC overview</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* Only clusters that use the VPC\-CNI network model support the shared VPC feature.

* When you create a cluster by using a shared VPC, the public access feature cannot be enabled.

* The support for the shared VPC feature varies based on different cloud services, including the compute, network, and storage services. Before you create a cluster by using a shared VPC, make sure that the required cloud service supports the shared VPC feature. For cloud services that VKE clusters rely on, see [Cloud service dependencies](https://docs.byteplus.com/en/docs/vke/Dependencies-between-VKE-and-other-cloud-services).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

After the resource owner of the shared VPC (Account A) shares the VPC with the resource user (Account B), Account B can use the shared VPC and subnets when creating a VKE cluster.


1. (Account A) Create a shared VPC and specify Account B as the resource user. For details, see [Getting started with the shared VPC feature.](https://docs.byteplus.com/en/docs/vpc/Getting-Started-with-Shared-VPC)

2. (Account B) Log in to the [VKE console](https://console.byteplus.com/vke) and create a VKE cluster. During networking configuration, select the VPC and subnet that are shared by Account A. For more configurations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).
