---
title: "Cluster overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-overview"
---

In Vital Kubernetes Engine (VKE), a cluster corresponds to a Kubernetes cluster and is a collection of computing, storage, and network resources in VKE.

<span id="Ghk9Uf0y"></span>
## Cluster type

<span id="scMx4stY"></span>
### Managed cluster

A managed cluster supports three node types: ECS instances, VCI instances, or a combination of both. This provides great node provisioning flexibility in addition to standard Kubernetes functionality such as workload scheduling, orchestration, and observability. VKE automates management and maintenance of master nodes, eliminating the complexity and infrastructure costs of self\-managed Kubernetes. You can focus on worker nodes that run your business workloads.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_184db4d09f6c47f135721ecc4a8e423e.png) </span>

<span id="QHTuu5yL"></span>
### Registered cluster

Registered clusters can be connected to standard Kubernetes clusters across different regions and infrastructures, and can also manage them. Registered clusters can manage the following clusters: local clusters, third\-party public cloud clusters, IDC self\-built clusters, edge clusters, and other Kubernetes clusters that meet Cloud Native Computing Foundation (CNCF) standards, such as Alibaba Cloud ACK, Tencent Cloud TKE, Huawei Cloud CCE, Google Cloud GKE, Amazon EKS, Baidu Cloud CCE, and custom clusters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>] Registered clusters are currently at the beta stage. To use this feature, submit an application.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_083af6841fbdef7f57f390d3ab2360df.png) </span>

<span id="9WrXpNGw"></span>
## Cluster features


|Feature |Managed cluster |Registered cluster |
|---|---|---|
|Cluster management |* Create cluster: You can create a ready\-to\-use Kubernetes cluster by using multiple methods. The cluster has the following configurations: fully managed master nodes, optional network models, public network access, and flexible custom configuration. For more information, see [Creation method overview](https://docs.byteplus.com/en/docs/vke/Cluster_creation_overview).<br><br>* Upgrade cluster: You can manually upgrade the Kubernetes versions of managed clusters. You can also achieve the automatic upgrade of Kubernetes patch versions by configuring an automatic O&M window, which achieves the centralized management of system add\-on upgrades. For more information, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).<br><br>* Delete cluster: You can delete a cluster. If you delete a cluster, resources created in the cluster will be affected, which poses high risks. For more information, see [Deleting clusters](https://docs.byteplus.com/en/docs/vke/Deleting-a-cluster). |* Registered cluster: You can flexibly access and manage Kubernetes clusters in any region or on any infrastructure, and manage and perform O&M on clusters in a centralized manner. This prevents business teams from directly accessing multiple clouds and achieves efficient management.<br><br>* Deregister cluster: If you do not want to manage a registered cluster in VKE, you can deregister the cluster to release resources. Deregistering a cluster does not delete the cluster. This operation only removes the cluster from VKE. |
|Node and node pool |Leverage custom or managed node pools with global scaling capabilities to streamline node management and adapt to diverse operational scenarios. |Node pools do not exist in registered clusters. You can only view and perform basic management operations on infrastructure resources (nodes) and cannot perform creation and deletion operations. |
|Workload/application management |* Lifecycle management: Multiple types of workloads are supported. You can perform operations on workloads throughout the entire lifecycle, such as creation, upgrade, and rollback. You can also configure environment variables, persistent storage, and application log collection.<br><br>* Autoscaler: Multiple types of workload autoscalers are supported, such as HPA, CronHPA, and IHPA. For more information, see [Workload autoscaling overview](https://docs.byteplus.com/en/docs/vke/How-Workload-Autoscaler-works). |* Lifecycle management: You can use machine resources in registered clusters to create workloads in VKE and perform operations on the workloads, such as deployment, update, and deletion.<br><br>* Autoscaler: You can achieve the autoscaling capability of HPA based on CPU and memory utilization by using the console. You can achieve other autoscaling capabilities supported by cloud providers by using YAML.  |
|Authorization management |* Supports IAM permission management for cloud resources, provides various preset policies, and supports user\-defined policies.<br><br>* Supports RBAC permission management for VKE. You can grant permissions on all clusters, specified clusters, or namespaces within your account based on your business requirements.<br><br>* Provides the IRSA mechanism, which supports fine\-grained isolation at the Pod level. |* Supports IAM permission management for cloud resources, provides various preset policies, and supports user\-defined policies.<br><br>* Supports RBAC permission management for VKE. You can grant permissions on all clusters, specified clusters, or namespaces within your account based on your business requirements. |
|Observability |Utilize robust observability through a comprehensive set of metrics and flexible dashboard settings to effectively monitor containerized applications with complex architectures and dynamic resource demands. |Provides monitoring and collection add\-ons, which can collect metrics, send the metrics to VMP for storage, and provide preset monitoring dashboards. |
|Scheduling |Rich scheduling policies meet business requirements in different scenarios, such as online and offline workloads. Examples include task scheduling, topology\-aware scheduling, ResourcePolicy, and CPU Burst, helping maximize resource utilization while ensuring application performance. |Scheduling capabilities depend on the original Kubernetes cluster. VKE does not provide additional scheduling enhancements.<br><br> |
|Storage management |Seamlessly integrate with various storage resources, such as EBS, TOS, and FileNAS to provide container applications with a wide range of persistent storage options. For more information, see [Storage overview](https://docs.byteplus.com/en/docs/vke/Storage-overview). |You can manage storage in registered clusters by using YAML. The storage types and usage methods vary based on different cloud providers. The specific YAML parameters and configurations are subject to the definitions provided by each cloud provider in actual scenarios. |
|Add\-on management |You can install and manage various add\-ons, including add\-ons of the **Network**, **Storage**, **Monitoring**, **DNS**, **Security**, **Image**, and **GPU** types, to meet your different business requirements. |VKE provides the following two add\-ons for the registered cluster:<br><br><br>* prometheus\-agent: This add\-on collects Kubernetes cluster metric data and sends it to VMP.<br><br>* cloud\-controller\-manager: Used for embedding control logic related to cloud vendors and integrating Kubernetes with the cloud platform through an add\-on mechanism. |


<span id="0ZYLMOFI"></span>
## Cluster lifecycle

The lifecycle of a cluster encompasses all possible states that it transitions through, from creation to deletion. For a description of the cluster lifecycle and state transitions, see [Resource status description](https://docs.byteplus.com/en/docs/vke/Resource-status-description#.6ZuG576k).
