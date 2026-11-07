---
title: "Overview of P2P acceleration"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Overview-of-P2P-acceleration"
---

P2P acceleration is an image distribution capability provided by VKE, suitable for scenarios such as large\-scale concurrent node image pulling, frequent scaling, and large image startup. This topic describes the basic concepts, acceleration modes, and corresponding technical principles of P2P acceleration.

<span id="bOAvHxrO"></span>
## What is P2P acceleration?

<span id="UGp1gSJT"></span>
### Basic concepts

When the size of a container application image reaches several GB or even tens of GB, nodes usually require a long time to download the complete image. Meanwhile, CR is centralized, meaning all nodes in the cluster pull images from CR. In large\-scale clusters or during autoscaling, a large number of nodes pull images concurrently, making CR throughput and its network links prone to performance bottlenecks.

P2P acceleration uses Dragonfly for P2P distribution. It deploys scheduling and caching add\-ons within your cluster and establishes a peer\-to\-peer distribution network inside the cluster to reduce repeated origin requests by reusing data between nodes.   The resources primarily involved in the P2P acceleration solution are described in the following table.


|Resource |Description |
|---|---|
|Scheduler |Deployed within the user cluster and responsible for receiving download information reported by Peers and Seed Peers and returning scheduling results. The scheduler is deployed with multiple replicas to handle scheduling requests within the cluster. |
|Seed Peer |Deployed within the cluster as a cache seed node that caches image data and serves as the egress point for back\-to\-origin CR requests. Seed Peer is deployed with multiple replicas to handle download and back\-to\-origin traffic within the cluster. |
|Peer |Deployed on each cluster node and responsible for obtaining the image data required by the node. Peers on different nodes can transfer cached data to each other over the P2P network. Meanwhile, Peers report download information to the scheduler and determine the data source node based on the scheduling results. |


<span id="hY4aS3PB"></span>
### Key advantages

P2P acceleration changes the approach from "each node downloads from the origin" to "a few nodes download from the origin while reusing data across the cluster". Its main advantages are as follows:


* **Reduced large\-scale distribution time**: Multiple nodes can obtain image data from different Peers in parallel, making this solution suitable for batch scaling, release, and rebuild scenarios.

* **Reduced CR pressure**: The same data is prioritized for reuse within the cluster, reducing repeated origin fetch requests and peak traffic.

* **Improved distribution stability**: Seed Peers can cache image data in advance and provide a stable data source for Peers.


<span id="9HLDzsm4"></span>
## Acceleration modes

<span id="MtMoZXeg"></span>
### Mode comparison

P2P acceleration supports multiple modes from which you can select as needed based on your cluster scale, resource isolation requirements, and startup latency requirements.


|**Mode** |**Data retrieval method** |**Resource deployment** |**Application scenario** |**Main characteristics** |
|---|---|---|---|---|
|Normal mode |Pulls the complete image, prioritizing data retrieval through P2P. |The scheduler and Seed Peer share nodes with business workloads. |P2P can be enabled quickly, with minimal requirements for cluster scale and resource isolation. |Deployment is simple, but acceleration add\-ons share node resources with business workloads. Network bandwidth contention occurs during image distribution, affecting business traffic. |
|Dedicated node pool mode |Pulls the complete image, prioritizing data retrieval through P2P. |The scheduler and Seed Peer are deployed on nodes in the dedicated node pool. |Large\-scale distribution, frequent release, and resource isolation. |The distribution chain is more stable, but additional nodes and cache space are needed. |


<span id="XGRszTvw"></span>
### Normal mode

In normal mode, no dedicated P2P cache node pool is created, The deployment method is relatively simple. Since the scheduler and Seed Peer share node resources with business workloads, this mode is suitable for clusters that need to quickly enable P2P distribution without requiring resource isolation at the moment.

In normal mode, worker nodes handle both business workloads and Peer data caching and transfer tasks. The required images must still be fully pulled before containers start. The cluster contains the scheduler, Seed Peers, and multiple worker nodes, with a Peer running on each worker node. The scheduler handles scheduling, while Peers and Seed Peers together form the P2P distribution network. The technical architecture is illustrated in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd38e9c31c38a66d7de9fe8b8e34cf9e.png) </span>

In normal mode, the image pulling process is as follows:


1. The container runtime on the node initiates a full image pulling request, and the local Peer takes over the download task.

2. The Peer reports the task and download information to the scheduler and requests available data sources.

3. The scheduler prioritizes selecting a download source from Peers or Seed Peers that already have the target data.

4. The current node obtains image data in parallel over the P2P network. When no data is available within the cluster, the Peer or Seed Peer retrieves it from CR.

5. After the download is complete, the current node can also provide other Peers with the cached data.


<span id="q7RnIwFi"></span>
### Dedicated node pool mode

If P2P acceleration is enabled in the cluster and a dedicated P2P cache node pool is created, the scheduler and Seed Peer are scheduled to this dedicated node pool based on node affinity, taints, and tolerations. Regular worker nodes continue to run Peers and business workloads, while dedicated nodes handle scheduling and centralized caching. This mode isolates scheduling and seed caching capabilities from business workloads and is suitable for clusters with a large number of nodes, frequent image distribution, or those that need to plan P2P cache disks and compute resources separately.

In dedicated node pool mode, a cluster has a dedicated cache node pool and a regular worker node pool. The dedicated cache node pool runs the scheduler and Seed Peers, while regular worker nodes run Peers. The two types of nodes form a P2P distribution chain through the intra\-cluster network. CR provides data only when a back\-to\-origin request is needed. The technical architecture is illustrated in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01c4f061a81ac93d67258516d8c8c6f7.png) </span>

In dedicated node pool mode, the image pulling process is as follows:


1. The scheduler triggers Seed Peer preheating to cache target image data on dedicated nodes in advance.

2. When a regular worker node pulls an image, the local Peer requests data sources from the scheduler.

3. The Scheduler assigns sources based on each Peer's data\-holding status and download state.

4. Worker nodes prioritize downloading from Seed Peers or other Peers that have cached the target data. They fall back to CR only when no cache is available.

5. Newly downloaded data remains stored in the Peer cache for reuse by subsequent nodes.
