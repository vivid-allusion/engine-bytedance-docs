---
title: "Add-on overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Add-on-overview"
---

You can install various add\-ons in clusters, including **network**, **storage**, **monitoring**, **DNS**, **security**, **image**, and **GPU** add\-ons, to meet your different business requirements. You can deploy, upgrade, or uninstall add\-ons based on your business requirements.

## Viewing add\-ons

You can view the add\-ons provided by Vital Kubernetes Engine (VKE) based on the following descriptions. To view the release records of each add\-on, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/Overview-of-add-on-release-notes).

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, find the cluster for which you want to view add\-ons and click the name of the cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, you can view various add\-ons provided by VKE.

   On the **Addons** page of a VPC\-CNI network model cluster, some add\-ons have the `VCI` label. You can deploy these add\-ons by using the following methods:

   * **Elastic Compute Service (ECS) deployment**: deploys the add\-ons on worker nodes (ECS nodes).

   * **Vital Container Instance (VCI) deployment**: deploys the add\-ons on VCI.

## Usage limits

* You cannot install add\-ons in a Flannel network model cluster when the cluster has no ECS nodes.

* You can install add\-ons with the `VCI` label only on VCI in a VPC\-CNI network model cluster. You cannot install other add\-ons.

* Add\-ons and plug\-ins that are deployed as DaemonSets are not supported on VCI. For more information, see [VCI limits](https://docs.byteplus.com/en/docs/vke/VCI-limits).

## Add\-on introduction

The following table lists various add\-ons provided by VKE.

### Network

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[alb-ingress-controller](https://docs.byteplus.com/en/docs/vke/alb-ingress-controller-add-on) |The alb\-ingress\-controller functions as an ALB Ingress controller add\-on. It allows clusters to create and manage ALB instances. This achieves traffic management and application release based on ALB instances. |Users do not need to be concerned with this. |Required |
|[ingress-nginx](https://docs.byteplus.com/en/docs/vke/ingress-nginx-add-on) |The ingress\-nginx add\-on is an Ingress controller that uses Nginx as a reverse proxy and load balancer.<br><br>> **warning**<br><br><br>> NGINX Ingress support will soon be discontinued. For details, see [\[Product announcement\] NGINX Ingress EOM](https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM).<br> |ECS<br><br>VCI |Optional |
|[apig-controller](https://docs.byteplus.com/en/docs/vke/apig-controller-add-on) |The apig\-controller functions as an APIG Ingress controller add\-on, which allows clusters to create and manage APIG instances for traffic management and application release. |ECS<br><br>VCI |Optional |
|[vpc-cni](https://docs.byteplus.com/en/docs/vke/vpc-cni-add-on) |The vpc\-cni add\-on is a network add\-on of clusters, which supports the VPC\-CNI network model.<br><br>> **tip**<br><br><br>> This add\-on is required in clusters that use the VPC\-CNI network model. The add\-on is not displayed if the cluster uses the Flannel network model.<br> |Users do not need to be concerned with this. |Required |
|[flannel](https://docs.byteplus.com/en/docs/vke/flannel-add-on) |The flannel is a cluster network add\-on that supports the Flannel network model.<br><br>> **tip**<br><br><br>> This add\-on is required in clusters that use the Flannel network model. The add\-on is not displayed if the cluster uses the VPC\-CNI network model.<br> |Users do not need to be concerned with this. |Required |
|[vpc-cni-controlplane](https://docs.byteplus.com/en/docs/vke/vpc-cni-controlplane-add-on) |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The vpc\-cni\-controlplane add\-on is the VPC\-CNI control plane add\-on of clusters, which provides control plane management capability for configuring security groups for pods.<br><br>> **warning**<br><br><br>> This add\-on is required when you create a cluster with the Trunk ENI feature enabled. You cannot modify the configurations of the add\-on after installation.<br> |Users do not need to be concerned with this. |Optional |
|[rdma-device-plugin](https://docs.byteplus.com/en/docs/vke/rdma-device-plugin-add-on) |[Public beta] The rdma\-device\-plugin add\-on is a Remote Direct Memory Access (RDMA) device add\-on, which manages RDMA network interface cards (NICs) and enables pod containers to use RDMA devices. |ECS |Optional |

### Storage

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[csi-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on) |The csi\-fsx is a general\-purpose FSX storage add\-on. It enables container clusters to use file systems that support the FSX client through the standard Container Storage Interface (CSI). |ECS |Optional |
|[fsx-service](https://docs.byteplus.com/en/docs/vke/fsx-service-add-on) |The fsx\-service is a general\-purpose FSX storage add\-on that provides FSX pod lifecycle management for use by the csi\-fsx add\-on. |ECS |Optional |
|[csi-nas](https://docs.byteplus.com/en/docs/vke/csi-nas-add-on) |The csi\-nas add\-on enables container clusters to use the NAS service through the standard CSI. |ECS<br><br>VCI |Recommended |
|[csi-ebs](https://docs.byteplus.com/en/docs/vke/csi-ebs-add-on) |The csi\-ebs add\-on is an add\-on of EBS, which allows container clusters to use the EBS service through the standard CSI. |ECS<br><br>VCI |Recommended |
|[csi-cloudfs](https://docs.byteplus.com/en/docs/vke/csi-cloudfs-add-on) |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The csi\-cloudfs add\-on is an add\-on of CloudFS, which allows container clusters to use CloudFS via the standard CSI. |ECS |Optional |
|[csi-vepfs](https://docs.byteplus.com/en/docs/vke/csi-vepfs-add-on) |The csi\-vepfs is an add\-on of vePFS, which allows container clusters to use the vePFS service through the standard CSI.<br><br>> **tip**<br><br><br>> After the add\-on is uninstalled, running pods can continue to access vePFS until they stop running.<br> |ECS |Optional |
|[snapshot-controller](https://docs.byteplus.com/en/docs/vke/snapshot-controller-add-on) |A storage snapshot add\-on. It supports using storage snapshots in Vital Kubernetes Engine.<br><br>> **warning**<br><br><br>> The snapshot\-controller add\-on requires the csi\-ebs add\-on. You need to install both when setting up snapshot\-controller. Uninstalling csi\-ebs will automatically remove snapshot\-controller.<br> |ECS<br><br>VCI |Recommended |

### Monitoring

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[metrics-server](https://docs.byteplus.com/en/docs/vke/metrics-server-add-on) |The metrics\-server add\-on is a core cluster monitoring add\-on that aggregates key monitoring metrics for resources across the cluster. |ECS<br><br>VCI |Required |
|[node-problem-detector](https://docs.byteplus.com/en/docs/vke/node-problem-detector-add-on) |The node\-problem\-detector add\-on is a node health monitoring add\-on, which is used to detect node anomalies and report the anomalies to kube\-apiserver. |ECS |Optional |
|[log-collector](https://docs.byteplus.com/en/docs/vke/log-collector-add-on) |A log collection add\-on for clusters. It collects cluster logs and sends them to Torch Log Service (TLS). |ECS<br><br>VCI |Optional |
|[event-collector](https://docs.byteplus.com/en/docs/vke/event-collector-add-on) |The event\-collector add\-on collects events from various cluster resources and sends them to TLS. |ECS<br><br>VCI |Optional |
|[prometheus-agent](https://docs.byteplus.com/en/docs/vke/prometheus-agent-add-on) |The prometheus\-agent add\-on is a monitoring add\-on of VMP, which collects and sends metrics of Kubernetes clusters to VMP.<br><br>> **tip**<br><br><br>> VMP officially began charging fees on May 29, 2023. If you install this add\-on in the cluster, additional fees will be incurred. For details, see [Billing model](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go).<br> |ECS<br><br>VCI |Recommended |
|[Prometheus-adapter](https://docs.byteplus.com/en/docs/vke/prometheus-adapter-add-on) |The prometheus\-adapter is an add\-on designed for VMP. It converts Prometheus metrics into the format required by the custom metric API. |ECS<br><br>VCI |Optional |
|[apmplus-opentelemetry-collector](https://docs.byteplus.com/en/docs/vke/apmplus-opentelemetry-collector-add-on) |The apmplus\-opentelemetry\-collector add\-on is an application performance monitoring add\-on, which collects and sends OpenTelemetry data and Prometheus metrics to APMPlus. |ECS |Optional |
|[apmplus-server-agent](https://docs.byteplus.com/en/docs/vke/apmplus-server-agent-add-on) |The apmplus\-server\-agent add\-on collects monitoring data for services and hosts and sends the data to the application performance monitoring service. |ECS |Optional |

### Scheduling

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[scheduler-plugin](https://docs.byteplus.com/en/docs/vke/scheduler-plugin-add-on) |The scheduler\-plugin functions as an expansion scheduler add\-on for clusters, which expands the scheduling capabilities and policies of the native kube\-scheduler.<br><br>> **tip**<br><br><br>> This is a system\-managed add\-on that prevents issues such as add\-on faults and unsatisfactory performance caused by user\-side factors. This reduces user maintenance costs and enhances add\-on stability.<br> |Users do not need to be concerned with this. |Required |
|[vci-virtual-kubelet](https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet-add-on) |The vci\-virtual\-kubelet add\-on achieves the scheduling and use of VCI instances through virtual nodes. Virtual nodes are created by default after the add\-on is deployed.<br><br>> **tip**<br><br><br>> This is a system\-managed add\-on, which prevents issues such as add\-on faults and unsatisfactory performance caused by user\-side factors. This reduces user maintenance costs and enhances add\-on stability.<br> |Users do not need to be concerned with this. |Recommended |
|[cluster-autoscaler](https://docs.byteplus.com/en/docs/vke/cluster-autoscaler-add-on) |The cluster\-autoscaler add\-on automatically scales cluster nodes.<br><br>> **tip**<br><br><br>> This is a system\-managed add\-on, which prevents issues such as add\-on faults and unsatisfactory performance caused by user\-side factors. This reduces user maintenance costs and enhances add\-on stability.<br> |Users do not need to be concerned with this. |Optional |
|[cronhpa](https://docs.byteplus.com/en/docs/vke/cronhpa-add-on) |The cronhpa add\-on is used to achieve the scheduled scaling of workloads. |ECS<br><br>VCI |Optional |
|[katalyst](https://docs.byteplus.com/en/docs/vke/katalyst-add-on) |The katalyst add\-on provides fine\-grained resource management capabilities, such as topology reporting in RDMA scenarios and core binding in Non\-Uniform Memory Access (NUMA)\-aware scheduling.<br><br>> **tip**<br><br><br><br>* > This add\-on is currently in **public beta**.<br><br><br>* > This add\-on can be installed only in clusters of the following versions:<br><br><br>   * > [Kubernetes v1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24): v1.24.10\-vke.12 and later<br><br><br>   * > [Kubernetes v1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26): v1.26.10\-vke.13 and later<br><br><br>   * > Other later Kubernetes versions<br> |ECS |Optional |
|[keda](https://docs.byteplus.com/en/docs/vke/keda-add-on) |The keda add\-on provides an autoscaler driven by Kubernetes events to enhance the capability of elastic scaling.<br><br>> **tip**<br><br><br>> The capabilities provided by the keda add\-on are generally consistent with those provided by the open source community. For details, see the [KEDA project website](https://keda.sh/).<br> |ECS<br><br>VCI |Optional |
|[karpenter](https://docs.byteplus.com/en/docs/vke/karpenter-add-on) |The karpenter add\-on implements event\-driven scale\-out for cluster nodes in real time, which offers improved elastic performance. |ECS |Optional |
|[aibrix](https://docs.byteplus.com/en/docs/vke/aibrix-add-on) |The aibrix functions as a solution suite for generative artificial intelligence (GenAI) inference infrastructure. It provides capabilities such as GPU workload autoscaling, with an emphasis on deep integration with the inference engine to provide advanced features and achieve ultimate optimization. |ECS<br><br>VCI |Optional |

### DNS

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[core-dns](https://docs.byteplus.com/en/docs/vke/core-dns-add-on) |The core\-dns add\-on provides service discovery and DNS resolution services in clusters. |ECS<br><br>VCI |Required |
|[node-local-dns](https://docs.byteplus.com/en/docs/vke/node-local-dns-add-on) |The node\-local\-dns add\-on provides the local DNS cache proxy to enhance the DNS service discovery performance and stability of the cluster. |ECS |Optional |

### Security

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[security-scan](https://docs.byteplus.com/en/docs/vke/security-scan-add-on) |An add\-on that provides security baseline inspection for clusters. After the add\-on is uninstalled, all inspection data is automatically deleted. |ECS |Optional |
|[application-inspector](https://docs.byteplus.com/en/docs/vke/application-inspector-add-on) |The application\-inspector add\-on is used to inspect cluster applications. |ECS<br><br>VCI |Optional |
|[pod-identity-webhook](https://docs.byteplus.com/en/docs/vke/pod-identity-webhook-add-on) |The pod\-identity\-webhook add\-on is an auxiliary add\-on for the IAM Roles for Service Accounts (IRSA) feature, providing automated assistance for using IRSA capabilities in clusters.<br><br>> **tip**<br><br><br>> This is a system\-managed add\-on, which prevents issues such as add\-on faults and unsatisfactory performance caused by user\-side factors. This reduces user maintenance costs and enhances add\-on stability.<br> |ECS |Optional |
|[migrate-plugin](https://docs.byteplus.com/en/docs/vke/migrate-plugin-add-on) |The migrate\-plugin add\-on is used to back up and restore application data in VKE clusters. It can back up container application metadata and PV data to TOS and quickly restore data to a specified cluster based on backup data. |ECS |Optional |
|[varmor](https://docs.byteplus.com/en/docs/vke/varmor-add-on) |The varmor is a container security sandbox add\-on designed for cloud\-native environments. It performs fine\-grained permission management on container runtime behavior. This restricts container access permissions at the kernel level, thereby improving the overall security defense level of clusters. |ECS |Optional |

### Image

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[cr-credential-controller](https://docs.byteplus.com/en/docs/vke/cr-credential-controller-add-on) |The cr\-credential\-controller add\-on enables container clusters to pull private images from CR without credentials when you create applications. |ECS<br><br>VCI |Optional |
|[p2p-accelerator](https://docs.byteplus.com/en/docs/vke/p2p-accelerator-add-on) |[Public beta] The p2p\-accelerator add\-on accelerates concurrent container image pulling on a large scale by using the P2P technology. |ECS<br><br>VCI |Optional |
|[image-accelerator](https://docs.byteplus.com/en/docs/vke/image-accelerator-add-on) |The image\-accelerator add\-on is a container image acceleration add\-on, which achieves container image lazy loading by using Nydus to accelerate image pulling during pod creation. |ECS<br><br>VCI |Optional |

### GPU

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[nvidia-device-plugin](https://docs.byteplus.com/en/docs/vke/nvidia-device-plugin-add-on) |The nvidia\-device\-plugin add\-on is a GPU device management add\-on that enables the use of NVIDIA GPU devices in containers. |ECS |Optional |
|[mgpu](https://docs.byteplus.com/en/docs/vke/mgpu-add-on) |The add\-on for sharing GPU resources among containers by isolating memory and computing power between containers. |ECS |Optional |

### Core

|**Add\-on name** |**Add\-on description** |**Deployment method** |**Installation recommendations** |
|---|---|---|---|
|[cloud-controller-manager](https://docs.byteplus.com/en/docs/vke/cloud-controller-manager-add-on) |The cloud\-controller\-manager is a core network add\-on for clusters. It performs lifecycle management on cloud resources, such as nodes and load balancers.<br><br>> **tip**<br><br><br>> This is a system\-managed add\-on, which prevents issues such as add\-on faults and unsatisfactory performance caused by user\-side factors. This reduces user maintenance costs and enhances add\-on stability.<br> |Users do not need to be concerned with this. |Required |
