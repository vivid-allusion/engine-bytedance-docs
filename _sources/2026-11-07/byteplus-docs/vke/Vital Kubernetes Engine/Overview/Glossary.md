---
title: "Glossary"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Terms"
---

This topic describes the glossary of VKE. This helps you quickly understand service knowledge and terms while reading related documents.

<span id="UDvGBOXq"></span>
## Cluster

It corresponds to the [Cluster](https://kubernetes.io/docs/concepts/cluster-administration/) in Kubernetes. It is a collection of computing, storage, and networking resources in VKE. VKE supports the following cluster types:


* Managed cluster: VKE manages and maintains the Master nodes of Kubernetes clusters. You are only required to create and deploy the Worker nodes for running loads in the clusters. This reduces the difficulty and cost of using a Kubernetes container cluster.

* Registered cluster: You can register existing clusters from your on\-premises infrastructure or other cloud vendors with VKE for centralized management. This reduces multi\-cloud operations for business teams and achieves efficient management of business clusters.


<span id="e1x3g3Ua"></span>
## Node pool and node

<span id="nX09HahS"></span>
### Node pool

It aggregates a group of nodes with the same configurations in a cluster. It can automatically scale node resources in a rapid manner, which helps you efficiently manage node resources in a Kubernetes cluster.

Node pools in VKE are classified into the following types:


* Custom node pool: You can specify custom configurations for node pools, such as the node, system, security, advanced, and additional configurations. You can also scale this type of node pool and edit the number of nodes.

   From the management perspective, user\-defined node pools of VKE are classified into the following types:

   * Managed node pool: Managed node pools help improve fault management for GPU computing resources, increase node pool resource utilization, and simplify day\-to\-day O&M.

   * Normal node pool: Normal node pools do not provide inspection or self\-healing capabilities. All other configurations are the same as those of managed node pools.

* Default node pool: This type of node pool is used to manage nodes such as existing ECS instances that are added to a cluster in the VKE console. The configuration capabilities of a default node pool are similar to those of a standard node pool, such as security configuration, advanced configuration, and additional configuration. However, a default node pool does not allow you to perform scaling or edit the node number.


<span id="VQtYpBxB"></span>
### Node

It corresponds to the [Node](https://kubernetes.io/docs/concepts/architecture/nodes/) in Kubernetes and is a basic element composing a VKE cluster. Nodes mainly include Master nodes (control nodes) and Worker nodes (computing nodes/working nodes). Applications are deployed on Worker nodes. They can be randomly deployed on Worker nodes or specified Worker nodes through configuration.

A **node** in VKE generally refers to a **Worker node**.

<span id="3HR35ekk"></span>
### Master node

It is a control node of a cluster. It mainly consists of the following four add\-ons:


* API server: provides a hub for data interaction and communication between modules.

* etcd: serves as a distributed data storage add\-on for storing cluster configurations.

* Controller Manager: implements cluster resource orchestration by defining the expected status of resources, which ensures that the actual status of various resources in the cluster is consistent with the expected status defined by users.

* Scheduler: performs application scheduling. This add\-on schedules containers to a Worker node by configuring node/pod affinity.

   In managed cluster mode, VKE centrally manages and maintains the master nodes of Kubernetes clusters, so you do not need to manage them yourself.


<span id="ejwTTOSP"></span>
### Worker node

It serves as a computing/working node of a cluster, which runs containerized applications. Currently, Worker nodes of VKE are ECS instances and virtual nodes.

A Worker node consists of the following components:


* Kubelet: a proxy add\-on of worker nodes mainly for interacting with container runtimes and working with API servers to manage containers on nodes.

* Kube\-proxy: a network proxy for solving the issues related to access between applications on nodes.

* Container runtime: a container runtime, such as containerd. It is mainly used to pull container images and manage containers through the lifecycle.


<span id="IuDGoQip"></span>
### Virtual node

A virtual node is a non\-physical computing node in a cluster. Your pods are directly scheduled onto VCI resources instead of being scheduled onto your own machines (physical nodes). This way, you do not need to manage machines or scale out nodes.

<span id="h1S7rkX2"></span>
## Network

<span id="P74SrgxZ"></span>
### CNI

It corresponds to the Container Network Interface ([CNI](https://github.com/containernetworking/cni)) resource in Kubernetes. It offers a technical add\-on for implementing a container cluster network solution. The following network models are supported in VKE:


* Flannel: an independent underlay network model based on which a high\-performance network for clusters can be built along with the global routing capabilities of VPCs.

* VPC\-CNI: an underlay network model built based on Elastic Network Interfaces (ENI) on VPC, providing high network performance.


<span id="lXLBAKve"></span>
### Service

It corresponds to the [Service](https://kubernetes.io/docs/concepts/services-networking/service/) in Kubernetes. It provides the VKE exposure capability based on the Layer 4 network. The following types of Services are currently available in VKE:


* ClusterIP: This method exposes a workload to other workloads in the same cluster. This type of service can be accessed by using an `internal domain name in the cluster`.

* NodePort: It opens a static port for the IP address of each node and exposes the service on the static port. An external user can send a request to `Node_IP:Node_Port` to access the service from outside of a cluster.

* LoadBalancer: A workload can be accessed from public networks through a load balancer to guarantee higher reliability. Generally, a load balancer is used for the services that you want to expose from the system to public networks.


<span id="txYHXKvN"></span>
### Ingress

It corresponds to the [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) in Kubernetes. An Ingress is a set of traffic forwarding rules that match and forward traffic based on HTTP and HTTPS. An Ingress can further divide access by domain name and path.

<span id="WPeSALJK"></span>
## Storage

The storage module provides methods for both persistent and temporary storage for Pods in the cluster.


|Term |Description |
|---|---|
|StorageClass |It corresponds to the [StorageClass](https://kubernetes.io/docs/concepts/storage/storage-classes/) in Kubernetes. It provides a standardized way to define and describe the type of a required storage resource. StorageClasses enable dynamic provisioning of PVs. With dynamic PVs, Kubernetes can automatically create storage based on your business requirements. |
|PVs |It corresponds to the [PersistentVolume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) (PV) in Kubernetes. It is a piece of network storage configured in the cluster. PVs are capacity add\-ons, such as Volumes, but have a lifecycle independent of any individual pod that uses a PV. |
|PersistentVolumeClaim |It corresponds to the [PersistentVolumeClaim](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) (PVC) in Kubernetes, which is the consumer of storage resources. It specifies requirements such as storage size and access mode, and Kubernetes automatically matches suitable PVs to meet these requirements.<br><br>The relationship between a PV and a PVC is similar to that between a Pod and a Node: The Pod consumes Node resources, and the PVC consumes PV resources. |


<span id="6l8bs3kh"></span>
## Namespace

It corresponds to the [Namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) in Kubernetes. It is an abstraction of a group of resources and objects. A namespace is used to divide cluster resources for resource isolation.

<span id="kFmqBlSd"></span>
## Workload

It corresponds to Workload in Kubernetes and is used to describe the resources that run business applications. Workloads include Deployments, StatefulSets, DaemonSets, Jobs, and CronJobs.


|Term |Description |
|---|---|
|Deployment |It corresponds to the [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) in Kubernetes. A Deployment can contain one or more pod instances with the same role. This means the pods have the same characteristics except for the names and IP addresses. A Deployment can create or delete pods at any time by using a pod template. |
|StatefulSet |It corresponds to the [StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) in Kubernetes. Similar to a Deployment, a StatefulSet contains one or more pod instances, but each pod has its own states (such as the fixed name, start/stop order, and separate storage). |
|DaemonSets |It corresponds to the [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) in Kubernetes. A DaemonSet ensures that each node in a cluster runs only 1 pod. A DaemonSet is related to a node. If a node is abnormal, a pod is not recreated on other nodes. |
|Job |It corresponds to Jobs in Kubernetes. A Job creates one or more pods to run a one\-time task. It runs only once and ensures that the pods created for the task terminate successfully. |
|CronJob |It corresponds to the [CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) in Kubernetes. A CronJob is used to create repeated scheduled jobs. |
|Pods |It corresponds to the [Pod](https://kubernetes.io/docs/concepts/workloads/pods/) in Kubernetes. It is the minimum computing unit that can be deployed and managed in VKE. A Pod encapsulates one independent IP address, one or more containers and volumes, and policy options that manage how containers run. |
|Container |It corresponds to the [Container](https://kubernetes.io/docs/concepts/containers/) in Kubernetes. It contains a software package including an application and the dependency environment on which the application runs. With a container, you can run programs in a relatively independent environment. |


<span id="h3BkvRqP"></span>
## Image

It corresponds to the [Image](https://kubernetes.io/docs/concepts/containers/images/) in Kubernetes. It is binary data encapsulating an application and all of its software dependencies. Each image has a unique identifier (image ID) based on which the image is identified and container applications are deployed.

VKE supports the deployment of container applications by using public/private container images in BytePlus CR, container images in the private image registries of users, and official Docker Hub images.

<span id="Hm12PUdm"></span>
## Label/Tag

A key\-value pair that identifies the characteristics of an object. In VKE, such key\-value pairs are divided into two categories:


* Tags that users define or that the system or platform adds to various resources.

* Labels, which correspond to Kubernetes labels.


<span id="XOGuVx6K"></span>
## Annotation

It corresponds to the [Annotation](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) in Kubernetes. It is used to describe information on data properties. It provides multiple features, such as storage location identification, historical data, resource retrieval, and file recording.

<span id="v2fppxap"></span>
## Taint

It corresponds to the [Taint](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) in Kubernetes. A taint enables a node to repel pods with specified characteristics.

<span id="5iU6XoPw"></span>
## Toleration

It corresponds to the [Toleration](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) in Kubernetes. Tolerations are applied to pods and allow (but do not require) the pods to be scheduled to nodes with matched taints.

<span id="NNxVchu2"></span>
## ResourceQuota

It corresponds to the [ResourceQuota](https://kubernetes.io/docs/concepts/policy/resource-quotas/) in Kubernetes. It is used in scenarios where multiple teams or users share cluster resources. It limits the total number of resources available to teams or users. For example, it limits the total number of specific types of objects (container and service) that can be created and the number of consumable computing resources (CPU and memory) within a namespace.

<span id="TEaN5We8"></span>
## LimitRange

It corresponds to the [LimitRange](https://kubernetes.io/docs/concepts/policy/limit-range/) in Kubernetes. It is used for appropriate resource allocation and management to improve the utilization and availability of cluster resources.

<span id="10mXvOoj"></span>
## Configuration item


|Term |Description |
|---|---|
|ConfigMap |It corresponds to the [ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap/) in Kubernetes. It can be used to store information that is not sensitive. |
|Secret |It corresponds to the [Secret](https://kubernetes.io/docs/concepts/configuration/secret/) in Kubernetes. It can be used to store sensitive data such as passwords, tokens, and keys. |


<span id="mHgFKfK3"></span>
## Scheduling


|Term |Description |
|---|---|
|Affinity scheduling |It is a scheduling capability that enables the system to select nearby nodes or pod instances for deployment, which achieves nearby routing and reduces network loss. |
|Anti\-affinity |For high reliability, pod instances are deployed in a distributed manner to reduce the impact on applications when a node fails. |
|Node affinity scheduling |It corresponds to the [NodeAffinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) in Kubernetes. It constrains which nodes your pod instances can be scheduled to based on node labels. |
|Pod scheduling based on taints and tolerations |Taints and tolerations work together to ensure that pods are not scheduled to inappropriate nodes. |
|Instance affinity scheduling |It corresponds to the [PodAffinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity) in Kubernetes. Pod instances that need to communicate with each other are deployed to the same TopologyKey to reduce network latency between the businesses of pods. |
|Instance anti\-affinity scheduling |It corresponds to the [PodAntiAffinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity) in Kubernetes. Pod instances are deployed in different TopologyKeys to improve the business stability of pods. |
|TopologyKey |It corresponds to the [TopologyKey](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/) in Kubernetes. It indicates a scope. It is generally specified by labels on a node. It can be a specific node or a region. |


<span id="OeHPAxnz"></span>
## Autoscaler


|Term |Description |
|---|---|
|HPA |It is used in Kubernetes clusters for horizontally scaling pods[](https://kubernetes.io/docs/concepts/workloads/autoscaling/horizontal-pod-autoscale/). It automatically increases and reduces the number of Pods in a Deployment and a ReplicaSet based on CPU and memory utilization. |
|Cluster Autoscaler |The Cluster Autoscaler ([CA](https://kubernetes.io/docs/concepts/cluster-administration/node-autoscaling/#cluster-autoscaler)) adds nodes to a cluster based on the number of resources requested by workload pods within a limit. |


<span id="dh5tFC4k"></span>
##
