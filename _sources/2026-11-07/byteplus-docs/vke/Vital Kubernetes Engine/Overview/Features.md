---
title: "Features"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Features"
---

VKE deeply integrates next\-generation cloud\-native technologies to provide high\-performance, container\-centric Kubernetes cluster management. It enables the efficient creation of highly available Kubernetes clusters on the cloud and provides visual management for containerized applications across the entire lifecycle. This topic describes the features of VKE in detail.

<span id="TT5CS887"></span>
## Permissions

VKE supports two user authorization methods: Identity and Access Management (IAM) and role\-based access control (RBAC).


|Feature |Description |
|---|---|
|IAM permissions |You can configure different permission policies for different IAM users including the default policy and user\-defined policies when you manage VKE resources. For more information, see [IAM](https://docs.byteplus.com/en/docs/vke/Authorization-overview#.aWFtLeaOiOadgw==). |
|RBAC permissions |You can configure different permissions for users to whom different roles are assigned. The cluster administrator, operation and maintenance administrator, developer, and read\-only user roles are preset in the system. Users can create custom role permissions. For more information, refer to [RBAC](https://docs.byteplus.com/en/docs/vke/Authorization-overview#.cmJhY-aOiOadgw==). |


<span id=".6ZuG576k566h55CG"></span>
## cluster

VKE enables you to quickly create standard Kubernetes clusters in the cloud, scale out clusters, and manage permissions.


|Feature |Description |
|---|---|
|Resource overview |Dashboards that display the total number of clusters, the number of resources within clusters, CPU and memory utilization, and other information are supported. You can use dashboards to monitor and manage cluster resources intuitively. |
|Cluster creation |You can quickly create Kubernetes clusters, choose from a wide range of worker node types in the cloud, and customize cluster settings. The following types of clusters are supported:<br><br><br>* Managed cluster: VKE manages and maintains the control plane of the Kubernetes cluster, and you only need to manage the worker nodes required to run workloads. <br><br>* Cluster template: VKE provides templates for quickly creating clusters. Essentially, these are also managed clusters.<br><br>* Registered clusters allow flexible integration between Kubernetes clusters in any region, on any infrastructure, and on any third\-party cloud with VKE and centralized management and O&M of these clusters. This helps enterprises eliminate direct multi\-cloud connections and improve management efficiency. |
|Cluster upgrade |You can upgrade the Kubernetes version of the cluster control plane and nodes with a few clicks and thus manage system add\-on upgrades in a centralized manner. For more information, refer to [Upgrading a cluster](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster). |


<span id=".6IqC54K55rGg"></span>
## Node pool management

Node pools are introduced in VKE to enable you to easily manage nodes in Kubernetes clusters.


|Feature |Description |
|---|---|
|Node pool creation |You can specify custom basic information, worker node configuration, and system configuration of a node pool. Custom configurations apply to all worker nodes in the node pool. |
|Managed node pool creation |By using node pools as the management unit, VKE helps improve fault management for GPU compute resources and increase node pool resource utilization in a simple and efficient way. |
|Add existing nodes |You can add existing Elastic Compute Service (ECS) instances to a VKE cluster. VKE provides a default node pool (vke\-default\-nodepool) to manage existing nodes. |
|Node pool management |You can manage a node pool throughout the lifecycle from creation to deletion (or removal). For more information on the lifecycle and status transition of a node pool, refer to [Resource status description](https://docs.byteplus.com/en/docs/vke/Resource-status-description#.6IqC54K55rGg). |
|Autoscaler |The autoscaling configuration can be applied globally. Node resources can be dynamically scaled based on the business load level in clusters. |


<span id=".5bqU55So566h55CG"></span>
## Application

You can deploy applications of different types in clusters and manage applications throughout their lifecycle. In addition, applications can be automatically scaled to prevent a single application from being overloaded.


|Feature |Description |
|---|---|
|Application creation |* You can deploy applications of various types including Deployments, StatefulSets, Jobs, CronJobs, and DaemonSets, by using images or templates.<br><br>* You can configure container information for applications, including application images, container ports, environment variables, storage, lifecycles, affinity/anti\-affinity, and health checks. |
|Application lifecycle management |* You can perform operations on applications such as editing, deleting, updating the number of instances, re\-deploying, and updating images.<br><br>* You can view application details, including the overview, instance list, access mode, version history, autoscaling information, events, and logs. |
|Application scheduling |Various application scheduling methods are supported, including node affinity scheduling, node taint\-based scheduling, pod affinity scheduling, and pod anti\-affinity scheduling. |
|Application scaling |Manual scaling, HorizontalPodAutoscaler (HPA), and CronHPA are supported. Among them, HPA performs scaling based on CPU, GPU, and memory metrics. |
|Application release |Applications can be released through a Service and an Ingress, and both canary release and blue\-green release are supported. |
|Application center |* Various application templates are available and you can deploy applications through templates with a few clicks.<br><br>* You can create a Helm application. The source of Helm charts can be the application center, a container registry, or a third\-party registry. |


<span id=".5a2Y5YKo566h55CG"></span>
## Storage

A wide range of storage resources in the cloud is available for VKE to meet various storage requirements.


|Feature |Description |
|---|---|
|Network storage |Various network storage services are available to meet storage requirements in different scenarios. The following types are available:<br><br><br>* Data management center (DMC)<br><br>* EBS<br><br>* Torch Object Storage (TOS)<br><br>* FileNAS<br><br>* EFS<br><br>* [[Beta · apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] vePFS<br><br>* [[Beta · apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Cloud File System (CloudFS)<br><br>* [[Beta · apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Logical Volume Manager (LVM) |
|Storage add\-on |Standard Container Storage Interface (CSI) and add\-ons in the cloud are supported. |
|PersistentVolume (PV) and PersistentVolumeClaim (PVC) |You can manually create a static PV. You can also create a StorageClass (SC) and then create a dynamic PV by using a PVC. |


<span id=".572R57uc"></span>
## Networks

Networks in VKE include container networks, Services, and Ingresses.


|Feature |Description |
|---|---|
|Pod networking |Two Container Network Interfaces (CNIs) are available:<br><br><br>* Flannel: This is an underlay solution (Flannel HostGateway). With Flannel, you can define the pod CIDR block of the container network in Kubernetes clusters.<br><br>* VPC\-CNI: This is an underlay solution implemented based on the elastic network interface (ENI) of a virtual private cloud (VPC). Under the VPC\-CNI network model, VPC subnets can be selected for pod networking. |
|Service |Three Service types including ClusterIP, NodePort, and LoadBalancer are supported. |
|Ingress |The following Layer 7 load balancing features are supported:<br><br><br>* ALB\-Ingress<br><br>* Nginx\-Ingress<br><br>* CLB\-Ingress<br><br>* APIG Ingress |


<span id="gpu"></span>
## GPU

GPU resources in clusters are managed and scheduled. This reduces resource usage costs while meeting the requirements in scenarios such as artificial intelligence (AI) and AI\-generated content (AIGC).


|Feature |Description |
|---|---|
|NVIDIA GPU |NVIDIA GPUs are supported. You can specify the GPU model for a container and request one or more GPUs. |
|mGPU |VKE provides the multi\-container GPU (mGPU) solution to enable GPU sharing across containers:<br><br><br>* The self\-developed mGPU solution enables you to virtualize a single GPU as multiple GPUs to enable GPU sharing across containers.<br><br>* The scheduling policy based on computing power and memory is supported. The minimum scheduling unit for computing power is 5% and that for memory is 1 GiB.<br><br>* Multiple computing power sharing policies are supported, including fixed\-share, guaranteed\-burst\-share, and native\-burst\-share.<br><br>* The multi\-card sharing solution enables a single container to use the computing power and memory resources of multiple GPUs on the same node. |


<span id=".6LCD5bqm"></span>
## Scheduling

VKE provides multiple scheduling policies based on the extension mechanism of the Kubernetes scheduling framework.


|Feature |Description |
|---|---|
|Binpack/Spread scheduling |The scheduling capabilities and policies of the native kube\-scheduler are extended to enable you to configure the Binpack/Spread policy for nodes and GPUs. |
|Job scheduling |VKE offers the following job scheduling capabilities:<br><br><br>* Gang scheduling: This is a scheduling policy in a concurrent system. This policy ensures that all related processes can be started at the same time and no exceptional processes are allowed, that is, All\-or\-Nothing.<br><br>* Capacity scheduling: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] This scheduling policy is implemented by introducing ElasticQuota on the scheduling side based on the extension mechanism of the scheduling framework. The Capacity scheduling policy improves the overall utilization of cluster resources through resource sharing while ensuring that sufficient resources are allocated to users. |
|ResourcePolicy scheduling |You can use a custom ResourcePolicy to define the order in which workload pods are scheduled to different node types. |
|Load\-aware scheduling |Pods are preferentially scheduled to nodes with lower load according to node load statistics to balance loads among nodes. This prevents application or node failures caused by a high load on a single node. |
|NUMA\-aware scheduling |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Based on Katalyst, it improves the resource management capability of Kubernetes, increases resource utilization, reduces costs, and improves load\-based scheduling capability. |
|RDMA topology\-aware scheduling |By sensing the network topology information of GPUs and RDMA devices, the system schedules all Pods in the same Job to nodes and RDMA network interface cards (NIC) that are as close as possible in the topology of the RDMA network. This helps users fully utilize the communication capabilities of the RDMA network. |


<span id=".55uR5o6n5ZKM6L-Q57u0"></span>
## Observability

Cluster\-oriented monitoring and operation and maintenance are necessary to ensure the stable operation of clusters and improve security and reliability. The following features are available:


* **Monitoring of critical metrics**: Cluster monitoring enables you to understand the status of clusters in real time, such as CPU, memory, disk space usage, and traffic. This way, you can identify and solve potential issues promptly.

* **Operation/fault tracing**: You can collect and view cluster logs and events to check the running status of the clusters and applications. If a fault occurs, you can view the logs and events for tracing.

* **Improved security and reliability**: Cluster inspection enables you to determine whether worker nodes and applications are secure, which improves the security and reliability of clusters.

* **Optimized resource utilization**: Cluster monitoring enables you to properly schedule pods as needed to maximize the utilization of cluster resources.



|Feature |Description |
|---|---|
|Event center |Connect to [Torch Log Service (TLS)](https://docs.byteplus.com/en/docs/tls/What_is_TLS) to collect, retrieve, and view global events of clusters. |
|Log center |* Connect to [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS) to collect, search, and view global logs of clusters and perform chart analysis.<br><br>* You can collect and view logs of control plane components in clusters, including etcd, kubelet, apiserver, controller, and scheduler.<br><br>* You can collect and view logs of an Ingress add\-on.<br><br>* You can collect and view the standard output (Stdout), the standard error (Stderr), and the logs in a specified path. You can configure environment variables to collect logs. |
|Basic observability |Basic cloud\-native observability is achieved through VMP. It uses high\-availability collectors deployed in clusters to monitor cluster resources, control plane services, networks, and workloads. |
|Full\-stack observability |Cloud\-native full\-stack observability, built on eBPF, achieves high\-performance, non\-intrusive, full\-stack data collection. It fully supports in\-depth observability at the kernel level and automatically parses application protocols such as HTTP(S), DNS, and gRPC Unary/Streaming when used with the high\-performance application protocol parsing module. It integrates Kubernetes metadata to provide a non\-intrusive full\-stack observability capability at the resource, network, and application layers. |
|Application performance observability |Application Performance Management Plus (APMPlus) can be integrated to provide end\-to\-end application performance monitoring services for applications deployed in clusters. |
|AI profiling |Supports non\-intrusive data collection and analysis by leveraging eBPF and dynamic process injection technologies. It is tailored for Kubernetes container scenarios and can perform online detection on container processes that run GPU tasks. |
|Auditing clusters |You can use API server audit logs to record the daily operations of users in VKE clusters. This can help the cluster administrator conduct security audits on cluster operations and ensure clusters run in a secure and stable manner. |


<span id="F19j9MAt"></span>
## Diagnosis and inspection

VKE provides the diagnosis and inspection feature to help you efficiently perform O&M and management on clusters.


|Feature |Description |
|---|---|
|Diagnosis |Quickly identifies common issues of cluster resources (nodes, node pools, Pods, and Ingresses) and provides fix suggestions. |
|Check and self\-healing |By using the "automated monitoring and repair" mode, it achieves early detection, immediate mitigation, and quick repair of node issues. This reduces downtime from minutes to seconds and significantly improves system robustness. |
|Cluster inspection |Inspection features for cluster resource quotas, utilization, nodes, and common risks. They help you identify risks in VKE clusters. |
|Baseline inspection |Based on security standards, baseline inspection provides security inspection for cluster nodes, enabling the timely detection of insecure configurations in cluster nodes. |
|Application inspection |Based on security standards and container security best practices, application inspection can promptly detect and block unsafe configurations to prevent applications from being attacked or exploited. This ensures the stable and secure operation of your business. |


<span id="Q7A5HUfq"></span>
## Developer services

VKE offers various developer services.


|Feature |Description |
|---|---|
|Native YAML |The native kubectl tool and YAML\-based configuration from the Kubernetes community are supported. |
|OpenAPI |Open APIs are available to developers. For more information, refer to [API reference](https://docs.byteplus.com/en/docs/vke/API-Usage-notes). |
|Terraform |Terraform, an open source tool for automated IT infrastructure orchestration, is supported. The tool is used to efficiently configure and manage basic cloud resources. For more information, refer to [Using VKE through Terraform](https://docs.byteplus.com/en/docs/vke/Overview-of-using-VKE-through-Terraform). |


<span id=".5Liq5Lq655So5oi35Yqf6IO95beu5byC"></span>
## Differences in features for individual users

VKE allows individual users to use its features, but some features are not yet available to individual users. The following table provides detailed descriptions.


|Feature |Availability for individual users |
|---|---|
|Cluster creation |* You can create managed clusters.<br><br>* You cannot create a cluster by using a cluster template. |
|VCI |The VCI service is unavailable to individual users. Therefore, all VCI\-related features of VKE clusters are unavailable to individual users. |
|Network storage |The following types of network storage are unavailable to individual users:<br><br><br>* CloudFS<br><br>* vePFS |
|Ingress |Individual users cannot use the apig\-controller add\-on. Therefore, APIG Ingress is not supported. |
|Computing |Nodes of the High\-Performance Compute GPU Elastic Compute Service type are not supported. |
|Suite |The following VKE suites are unavailable to individual users:<br><br><br>* AIOps suite: does not support check and self\-healing, but supports all other inspection and diagnosis capabilities.<br><br>* Cloud\-native AI suite<br><br>* Batch computing suite |
|Node pool management |Managed node pools are unavailable to individual users. |
|Add\-ons |The following add\-ons managed by VKE are unavailable to individual users:<br><br><br>* vci\-virtual\-kubelet<br><br>* dns\-autoscaler<br><br>* apig\-controller<br><br>* apmplus\-opentelemetry\-collector<br><br>* apmplus\-server\-agent<br><br>* csi\-cloudfs<br><br>* csi\-vepfs<br><br>* mgpu<br><br>* rdma\-device\-plugin<br><br>* batch\-node\-controller<br><br>* batch\-queue\-controller |
|Other features |Other features that are not associated with the features **unavailable to individual users** are available to individual users. |
