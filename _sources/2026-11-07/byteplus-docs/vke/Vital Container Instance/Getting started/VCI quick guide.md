---
title: "VCI quick guide"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-quick-guide"
---

This topic aims to help you understand the basic usage process of Vital Container Instance (VCI) and get started with it.

<span id=".5L2_55So5rWB56iL"></span>
## Usage process

The following figure illustrates the VCI usage process.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d2f9cf22840fc9f59bb7230ea4b484d8.png) </span>


1. Register a BytePlus account and apply for console permissions on Vital Kubernetes Engine (VKE).

   Before you activate VCI, you must register a BytePlus account and apply for VKE console permissions. For more information, refer to [VCI preparations](https://docs.byteplus.com/en/docs/vke/VCI-preparations).

2. (Optional) Create and authorize Identity and Access Management (IAM) users.

   To manage container applications with multiple roles, you must create IAM users and grant them the appropriate product permissions. You can also configure role\-based access control (RBAC) permissions. For more information, refer to [VCI preparations](https://docs.byteplus.com/en/docs/vke/VCI-preparations).

3. Create a cluster whose pod network mode is **VPC\-CNI**.

   Create a **VPC\-CNI** cluster to start using VCI. For more information on how to create a cluster, refer to [Creating a cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

4. Use VCI to deploy a workload (application), view its deployment status, and access the application.

   VCI offers various methods for deploying applications.

   * [Deploying applications by using workloads](https://docs.byteplus.com/en/docs/vke/Using-Vital-Container-Instance-in-the-console)

   * [Deploying applications by using kubectl](https://docs.byteplus.com/en/docs/vke/Using-Vital-Container-Instance-with-kubectl)

5. Manage the lifecycle of the application and its associated resources.

   VCI offers the full lifecycle management feature for applications and their related resources. This feature allows you to view the status and log information of the deployed applications, as well as upgrade, scale, and monitor them.
