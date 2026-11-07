---
title: "Overview of nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Node-overview"
---

Nodes are a constituent element of a cluster. A cluster consists of one or more master nodes and worker nodes. Worker nodes run the deployed applications. Applications can be deployed dynamically (randomly) or statically (fixedly) to worker nodes.

<span id=".6IqC54K5566A5LuL"></span>
## Introduction to nodes

Vital Kubernetes Engine (VKE) provides managed clusters. The following diagram shows the architecture of a VKE cluster.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_878c0fbc292a71f3e57446637fe33715.png) </span>


* Master nodes

   A master node is the core management unit of a cluster. VKE manages and maintains master nodes of Kubernetes clusters. You only need to purchase and deploy worker nodes to use clusters and workloads. You do not need to worry about cluster management and maintenance.

* Worker nodes

   A worker node is a cloud host or physical machine responsible for running containerized applications. A worker node consists of the following components:

   * kubelet: the agent that interacts with the container runtime and communicates with the API Server to manage containers on the worker node.

   * kube\-proxy: a network proxy that solves access issues between applications on a worker node.

   * Container runtime: a core component that is responsible for pulling container images and managing the entire lifecycle of containers. An example of a container runtime is containerd.


<span id=".6IqC54K555Sf5ZG95ZGo5pyf"></span>
## Node lifecycle

The lifecycle of a node refers to the various states it goes through from creation to deletion (or release). For a description of the node lifecycle and status transitions, see [Resource status description](https://docs.byteplus.com/en/docs/vke/Resource-status-description#.6IqC54K5).

<span id=".6IqC54K56KeE5qC8"></span>
## Node specifications

Node specifications may be added or removed. Instances with a certain specification can also be sold out. We recommend that you check node specifications and instance availability on the **Create node pool** page of the [VKE console](https://console.byteplus.com/vke) before you plan a node pool for a cluster. For ECS specification additions, availability, and other changes, see [Product announcement](https://docs.byteplus.com/en/docs/vke/Product_announcements)s.

<span id=".6IqC54K55LiO5LqR55uY5YWz57O7"></span>
## Nodes and volumes

Volume types available to nodes vary by node specification. For details, see [FAQ](https://docs.byteplus.com/en/docs/vke/How_to_use_cloud_disk_PersistentVolumes_in_a_cluster_with_nodes_of_different_specifications).
