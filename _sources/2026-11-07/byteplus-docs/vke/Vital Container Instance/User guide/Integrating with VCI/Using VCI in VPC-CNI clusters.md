---
title: "Using VCI in VPC-CNI clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine"
---

A VKE cluster uses Elastic Compute Service (ECS) instances for pod scheduling by default. Also, it supports using BytePlus Container Instance (VCI) or a hybrid of VCI and ECS for pod scheduling. By using virtual nodes, you can schedule pods to VCI for running, eliminating the need for capacity planning and node O&M and enabling flexible, on\-demand pod scheduling.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* VCI is based on the Virtual Kubelet technology from the Kubernetes community and connects to Kubernetes through virtual nodes.

* Each pod running on a virtual node maps to a VCI.


<span id=".c2VydmVybGVzcy3og73lips="></span>
## Serverless capabilities

VKE has integrated VCI support to provide a more serverless Kubernetes experience.


* VKE provides a managed, maintenance\-free vci\-virtual\-kubelet add\-on and automated creation of virtual nodes. This enables seamless integration with VCI. For details, see [Virtual Kubelet and virtual nodes](https://docs.byteplus.com/en/docs/vke/Virtual-Kubelet-and-virtual-nodes).

* VKE allows you to create a Kubernetes cluster without worker nodes. In this case, the system automatically creates virtual nodes and deploys components in the cluster by using VCI.


<span id=".5L2_55So5rWB56iL"></span>
## Usage process:

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LXZwYy1jbmkt5a655Zmo572R57uc5qih5Z6L55qE6ZuG576k"></span>
### Step 1: Create a VPC\-CNI cluster


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the top navigation bar, select the region closest to your business.

3. In the left navigation bar, click **Cluster**.

4. On the **Cluster** page, click **Create cluster**.

5. In the **Create cluster** dialog box, click **Create now** in the **Custom managed clusters** section.

6. On the **Create cluster** page, configure the cluster according to the prompts on the page. You need to specify some parameters based on the following descriptions. For detailed configuration instructions for other parameters, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   1. **Cluster configuration**

      
      |Parameter |Description |
      |---|---|
      |**Networking** ||
      |Network model |Configure pod networking (CNI) solution for the cluster. In VCI scenarios, you must select **VPC\-CNI**. |
      

      After the configuration is complete, click **Next: Node pool configuration** in the lower\-right corner of the page.

   2. **Node pool configuration (Optional)** 

      Specify configurations based on your business requirements. No hard limits exist for VCI scenarios. After the configuration is complete, click **Next: Addon configuration** in the lower\-right corner of the page.

   3. **Add\-on configuration**

      You need to install the **vci\-virtual\-kubelet** add\-on. Configure other add\-ons based on your business requirements. After the configuration is complete, click **Next: Configuration confirmation** in the lower\-right corner of the page.

6. After confirming the cluster configuration information and reading the terms of service, scroll to the bottom of the page, select **I have read and agree to Vital Kubernetes Engine Specific Terms of Service**, and click **Confirm** in the lower\-right corner of the page to create the cluster.

   It will take 15 to 20 minutes to create a cluster. You can click **Cluster list** to proceed with other configurations, or stay on this page to view the creation progress.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65bel5L2c6LSf6L295oiW6ICFLXBvZC3ml7bkvb_nlKgtdmNpLemDqOe9sg=="></span>
### Step 2: Use VCI for workload or pod deployment

In the VPC\-CNI cluster that is created in the previous step, use VCI to deploy workloads or Pods. For details, see [Creating VCIs](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

<span id=".5omp5bGV6IO95Yqb"></span>
## Extending capabilities

When you create a Pod, you can add a Pod annotation to use more VCI capabilities. For a detailed description, see [Pod annotations](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations).
