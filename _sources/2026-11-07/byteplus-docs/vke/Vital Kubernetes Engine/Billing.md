---
title: "Billing"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Billing"
---

In Vital Kubernetes Engine (VKE), you can create the following type of container cluster: managed VKE cluster. For more information, refer to the following billing description:

<span id=".6K6h6LS56aG5"></span>
## Billable items

<span id=".6ZuG576k5omY566h6LS555So"></span>
### Fees of cluster management

For managed VKE clusters, the master nodes (control plane) are fully created and managed by VKE. You are free from O&M and management on the master nodes of Kubernetes clusters. To use this type of cluster, simply create worker nodes. This way, you can focus more on your business. VKE offers multiple characteristics, such as ease of use, low cost, and high availability. Therefore, in terms of this cluster type, VKE charges you for cluster management. For more information, refer to Billing for cluster management.

<span id=".5LqR5Z-656GA6LWE5rqQ6LS555So"></span>
### Fees of basic cloud resources

VKE clusters integrate with various resources and capabilities of the BytePlus IaaS layer in multiple aspects, such as computing, networking, storage, and security. This simplifies processes related to Kubernetes clusters such as deployment and scaling. This way, you can focus on the development and management of container applications. When you use VKE, you are charged for the created basic resources on which VKE depends. For more information, refer to Billing for basic cloud resources.

<span id=".6ZuG576k5omY566h6K6h6LS5"></span>
## Billing for cluster management

Managed VKE clusters charge you for cluster management. The following table displays the billing information:


|Cluster Type |Cluster Description |Billing Method |Billing Cycle |
|---|---|---|---|
|Managed VKE |You are free from the creation, O&M, and management of the master nodes of clusters. To use this type of cluster, simply create worker nodes. This way, you can focus more on your business. VKE offers multiple characteristics, such as ease of use, low cost, and high availability. |Pay\-as\-you\-go.<br><br>You are charged USD 0.09 per hour for each cluster instance. |The service is billed by hour. |


<span id=".5LqR5Z-656GA6LWE5rqQ6K6h6LS5"></span>
## Billing for basic cloud resources

The use of VKE covers the resources of multiple aspects on the IaaS side, such as computing, networking, storage, and security. You are charged for the created basic resources in use. If you use other basic cloud resources, you are required to pay the service fees based on the corresponding billing description. The following table describes the billing information.


|Cloud Resource Name |Required |Resource Description |Billing Description |
|---|---|---|---|
|Elastic Compute Service (ECS) |Yes |It is used to create nodes for VKE clusters. |[Elastic Compute Service (ECS) billing description](https://docs.byteplus.com/en/docs/ecs/Billing-overview) |
|Virtual Private Cloud (VPC) |Yes |It is used to build a cluster network and an Ingress for VKE clusters. |[Virtual Private Cloud (VPC) billing description](https://docs.byteplus.com/en/docs/vpc/Billing) |
|Cloud Load Balancer (CLB) |Yes |It is used to create load balancing resources for VKE clusters. |[Cloud Load Balancer (CLB) billing description](https://docs.byteplus.com/en/docs/clb/Billing-01) |
|Application Load Balancer (ALB) |Optional |It is used to create application load balancing resources for VKE clusters. |[Application Load Balancer (ALB) billing description](https://docs.byteplus.com/en/docs/clb/Billing-rules) |
|Elastic IP Address (EIP) |Optional |It is used to implement communication between related resources and public network. |[Elastic IP Address (EIP) billing description](https://docs.byteplus.com/en/docs/ecs/Elastic-IP-Address-billing) |
|NAT Gateway |Optional |It is used to implement communication between cluster nodes and public network. |[NAT Gateway billing description](https://docs.byteplus.com/en/docs/natgateway/Billing-overview) |
|Container Registry (CR) |Recommended |It is used to create cloud native artifacts and manage the full lifecycle. |[Container Registry (CR) billing description](https://docs.byteplus.com/en/docs/cr/billing-overview) |
|Vital Container Instance (VCI) |Optional |It seamlessly integrates with VKE to offer the Kubernetes orchestration capability. |[Vital Container Instance (VCI) billing description](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview) |
|Torch Log Service (TLS) |Recommended |It is used to collect container logs of clusters. |[Torch Log Service (TLS) billing description](https://docs.byteplus.com/en/docs/tls/billable_items) |
|Torch Object Storage (TOS) |Optional |It is used to create a TOS volume. It is mounted under a path of a container. |[Torch Object Storage (TOS) billing description](https://docs.byteplus.com/en/docs/tos/docs-billing-overview) |
|FileNAS |Optional |It is used to persistently store containers. It is mounted on a container during workload creation. |[FileNAS billing description](https://docs.byteplus.com/en/docs/nas/Billing-overview) |
|Elastic Block Storage (EBS) |Yes |It is also known as a volume, offering data storage space to clusters for supporting the running of operating systems, logs, and daily work. |[Elastic Block Storage (EBS) billing description](https://docs.byteplus.com/en/docs/ecs/Volume-billing) |
|Vital Managed Service for Prometheus (VMP) |Optional |It is used to monitor cluster resources. |[VMP billing description](https://docs.byteplus.com/en/docs/vmp/billing-overview) |


<span id=".KirmrKDotLnlgZzmnI3or7TmmI4qKg=="></span>
## **Overdue payment and service suspension policies**

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">The system notifies you of the risk of service suspension and resource release if you have overdue payments. Top up your account balance promptly to avoid any impact on your service.</div>


The service status changes as follows when you have overdue payments in VKE:


* If an overdue payment exists for less than or equal to two hours, you can normally use your BytePlus service and are billed according to your actual usage.

* If an overdue payment exists for over two hours, BytePlus sends you a notification and freezes resources. You cannot operate your cluster and pay\-as\-you\-go resources in the cluster.

* Within 720 hours after resources are frozen, cluster resources are automatically unfrozen if you top up your account balance. In this case, you can continue to use VKE normally.

* If resources are frozen for more than 720 hours, BytePlus sends you a notification and releases resources. This means it destroys your cluster. Resources cannot be restored once released. To continue to use VKE, buy resources again.


<span id=".Kirmn6XnnIvmrKDotLkqKg=="></span>
### **Viewing overdue payments**


1. Log in to the [Billing center](https://console.byteplus.com/finance/overview).

2. On the **Overview** page, view the overdue amount.
