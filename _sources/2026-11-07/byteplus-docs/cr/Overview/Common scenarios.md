---
title: "Common scenarios"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/common-scenarios"
---

This topic introduces the use scenarios of Container Registry (CR).

<span id="oci-制品生命周期管理"></span>
## Lifecycle management of OCI artifacts

CR delivers the capabilities to manage Open Container Initiative (OCI) artifacts, such as container images and Helm charts, throughout their lifecycles. The capabilities include building, uploading, downloading, and deleting the OCI artifacts.


* [OCI artifact repository management](https://docs.byteplus.com/en/docs/cr/oci-artifact-management)


<span id="ai-训练加速"></span>
## AI training acceleration

AI container images are large. The size of an individual image can reach or exceed 10 GB. Therefore, container image pulling is slow and easy to fail. Large AI container images can be automatically converted to CR Enterprise Edition images, and the converted images can be loaded and uncompressed online as needed. The whole process significantly reduces the time from container creation to image pulling and improves the distribution performance.


* [Creating a conversion rule for image lazy loading](https://docs.byteplus.com/en/docs/cr/p2p-acceleration-overview)


<span id="大规模集群应用部署"></span>
## Application deployment in large clusters

In large Vital Kubernetes Engine (VKE) clusters with on\-demand scalability, slow image pulling possibly occurs. In the implementation of the CR Enterprise Edition and the Peer to Peer (P2P) acceleration capability of VKE, the bandwidth between cluster nodes can be reused. This accelerates the distribution among nodes in the large cluster, saves the download time, and improves the distribution performance.


* [Overview of P2P acceleration](https://docs.byteplus.com/en/docs/cr/p2p-acceleration-overview)


<span id="镜像迁移备份"></span>
## Image backup and migration

Many customers use the service of multiple public cloud providers and have their private data centers. This poses challenges to container image distribution, backup, and migration with the prevalence of containerized microservice applications. CR Enterprise Edition helps you effortlessly and seamlessly replicate local images to BytePlus CR. CR works with VKE to realize container image pulling on the internal network while ensuring timely application startup and scalability.


* [Replicating images across platforms](https://docs.byteplus.com/en/docs/cr/replicate-images-across-platforms)
