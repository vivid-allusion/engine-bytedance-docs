---
title: "Product advantages"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-benefits"
---

VCI provides advantages like extreme elasticity, high performance, zero operations and maintenance (O&M), and ease of use. It helps you quickly build and deploy containerized applications and ultimately enhances business efficiency and quality. This topic describes the advantages of VCI.

<span id=".5YWN6L-Q57u0"></span>
## Zero O&M


* VCI uses fully managed serverless architecture, which saves you from node O&M efforts.

* You need to submit container images, without worrying about the underlying servers or capacity planning. You can focus on business innovation.


<span id=".5p6B6Ie05by55oCn"></span>
## Ultra scalability

<span id=".5by55b6X5b-r"></span>
### Fast scaling

VCI supports autoscaling and load balancing. This support allows you to automatically expand or shrink the scale of VCI instances based on business needs to handle peak and off\-peak traffic. The system also automatically distributes business traffic across different VCI instances via load balancing to improve application performance and availability:


* This efficient scaling can meet the demand for tens of thousands of vCPU cores within minutes and ensures that sufficient computing resources are quickly provisioned when business needs arise.

* It leverages various container image acceleration capabilities provided by Vital Kubernetes Engine (VKE), such as lazy loading of images and P2P\-based image distribution. Additionally, it features unique acceleration mechanisms like image caching. These capabilities ensure that the overall startup time for a pod (with image data up to hundreds of GiB) can be controlled to within ten seconds, significantly improving user efficiency and reducing cloud costs.


&nbsp;

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d026f2372f5db1f9b8bfea510418f75e.png) </span>

<span id=".5by55b6X5Ye6"></span>
### Adequate scaling


* VCI fully integrates computing resource infrastructure of BytePlus to supply computing power, and offers multiple instance families based on different underlying hardware capabilities. These families deliver differentiated computing, storage, and network performance to support a wide range of business applications and scenarios:

   * The general\-purpose CPU instance families provide balanced vCPU, memory, and network capabilities to meet service requirements in most scenarios.

   * The GPU\-accelerated families deliver cost\-effective performance for various AI computing scenarios such as large model training, text and image generation, and task inference.

* Based on sufficient computing resource supply, VCI provides elastic resource priority scheduling strategies. Together with VKE, it supports flexibly scheduling pods to different types of computing resource pools (such as ECS and VCI) via custom resource policies (ResourcePolicy). Scheduling and allocation are performed based on actual business scenarios by using strategies like percentage thresholds and priority control.


<span id=".5by55b6X55yB"></span>
### Cost\-effective scaling

Deploying containerized businesses with VCI reduces overall business costs, as you only pay for the resources actually used:


* Billing is based on the resources actually consumed by pods, such as vCPU, memory, and GPU. The billing duration for VCI instances equals their uptime, which spans from the start of container image download to the stop of pods, with precision down to the second.

* VCI reduces idle resources and improves bin packing efficiency, thereby lowering your computing resource costs.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ee5050fd371a474c9d7e8864ca5cb0e.png) </span>

<span id=".6auY5pWI6ZqU56a7"></span>
## Efficient isolation

Based on MicroVM technology, it provides VM\-level isolation, which contributes to lower resource consumption and higher efficiency.  VCI supports small\-specification, fine\-grained (small\-step) allocation of CPU and GPU resources.


* Built on secure sandbox containers, VCI provides VM\-level security and resource isolation. Each instance runs in a dedicated kernel and does not share infrastructure resources with other workloads or pods.

* VCI is deeply optimized for container runtime environments and offers faster startup speeds and higher operational efficiency than traditional VMs.


<span id=".5LiO5pmu6YCa5a655Zmo5a6e5L6L5LyY5Yq_5a-55q-U"></span>
## Advantages compared with regular container instances

VCI demonstrates outstanding advantages in performance and resource isolation compared with regular container instances.


|Feature for comparison |VCI |Regular container instance |
|---|---|---|
|Kernel |Dedicated kernel. |Shared kernel. |
|Isolation |Hard isolation based on virtualization. |Soft isolation based on namespaces and Cgroups. |
|Scaling |Second\-level autoscaling. |Minute\-level autoscaling. |
