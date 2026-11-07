---
title: "Guide for beginners"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quick-guide"
---

This topic is intended to help you quickly get started with .

<span id=".5L2_55So5rWB56iL"></span>
## Usage process

The usage process of VKE is shown in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a74c5c313fb5a1862e1f1bd314af39fa.png) </span>


1. Create a BytePlus account and obtain permissions to access the VKE console. Create 

   Before using VKE, you need to create a BytePlus cloud platform account and obtain permissions to access the VKE console. For details, see [Preparations](https://docs.byteplus.com/en/docs/vke/Preparations).

2. (Optional) Create IAM users and grant permissions to them.

   When VKE\-related services are managed by multiple roles, you need to create IAM users and grant the corresponding permissions to them on VKE. You can also configure RBAC permissions. For details, see [Preparations](https://docs.byteplus.com/en/docs/vke/Preparations).

3. Create a cluster.

   Get started with VKE by creating your first cluster. To quickly create a cluster, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-in-the-console#.5q2l6aqk5LiA77ya5Yib5bu66ZuG576k).

4. Deploy workloads (applications), check their deployment status, and access them.

   VKE provides multiple methods of deploying applications:

   * [VKE console](https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-in-the-console): Deploy your container applications to the cluster through the **Workload** module in the console. The **Workload** module provides a visual interface based on Kubernetes\-native capabilities for you to manage various workloads throughout the lifecycle.

   * [kubectl](https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-with-kubectl): Deploy your container applications to the cluster using the kubectl command\-line tool. VKE retains native Kubernetes YAML editing capabilities. You can manage various workloads throughout the entire lifecycle via kubectl to meet your diverse development requirements.

   * [Application templates](https://docs.byteplus.com/en/docs/vke/Deploying-an-application-using-an-application-template): Deploy your container applications to the cluster using the Helm **application templates**. The **application templates** provided by VKE help you quickly deploy and manage Helm applications, greatly simplifying the installation and management of Kubernetes resources.

5. Manage the lifecycle of applications and their associated resources.

   VKE provides the full lifecycle management feature for workloads (applications) and their related resources, including viewing the status and log information of workloads after deployment, as well as performing upgrades, scaling, and monitoring.
