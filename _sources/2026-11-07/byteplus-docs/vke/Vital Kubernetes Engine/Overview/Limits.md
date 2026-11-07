---
title: "Limits"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Limits"
---

This topic describes the limits on using Vital Kubernetes Engine (VKE).

<span id=".6ZmQ5Yi25qaC6L-w"></span>
## Overview of limits

Take note of the following limits before you use VKE:


* Make sure that you complete [real-name verification](https://console.byteplus.com/user/authentication/detail/) before you create VKE clusters.

* You can create pay\-as\-you\-go cloud resources only if the account balance is not 0 after the coupon is deducted.

* After a VKE cluster is created, you cannot perform the following operations:

   * Change the VPC to which the cluster belongs.

   * Change the Container Network Interface (CNI) add\-ons of the container network for the cluster.

   * Change the CIDR block of the container network in the cluster.

   * Uninstall the default system\-required add\-ons in the cluster.

   * Migrate applications between different namespaces.

* Take note of the following limits on basic cloud resources in a VKE cluster:

   * You can only create and add cloud resources that use **pay\-as\-you\-go** as the billing method. Cloud resources that use **subscription** as the billing method are not supported. The billing method is not limited to existing cloud resources.

   * Due to quotas and inventory limits of underlying cloud resources such as Elastic Compute Service (ECS) instances, only part of the nodes may be created when you create or scale out a container cluster.

   * Public IP addresses are limited by the quotas and capacities of line types. Therefore, when you create Load Balancers and NAT Gateway resources of the public network type, you may fail to create the associated resources.

   * When a VKE cluster is deleted, associated pay\-as\-you\-go cloud resources are deleted by default. Some cloud resources may remain because their ownership or permissions are not limited to the cluster itself. In this case, you can delete the remaining resources in the cloud resource console.


<span id=".6ZuG576k6YWN6aKd6ZmQ5Yi2"></span>
## Cluster\-related quotas

The following table displays the default cluster\-related quotas for each BytePlus account (including its IAM users) after VKE is activated. For more information on how to view the detailed cluster resource quotas within the current account, refer to the [View and apply for quotas](https://docs.byteplus.com/en/docs/vke/Limits?TagIDs=2,255#SAoYyaXa) section of this topic.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If your quota has reached the limit and you need to increase it, first check how many Pods are in the Pending state due to insufficient quota.</div>


<div data-tips="true" data-tips-type="warning">If too many Pods are in the Pending state, we recommend deleting those Pods before increasing the quota, or increasing the quota gradually in small increments. Otherwise, a large number of Pending Pods may be scheduled concurrently after the quota is increased, causing a sudden spike in service load and affecting service availability.</div>



|**Limitation item** |**Quota within a single account** |**Method of Applying for More Quota** |
|---|---|---|
|Real\-name verification |Enterprise or individual real\-name verification |None |
|Limit for creating pay\-as\-you\-go resources |The total amount of the account balance and coupons is greater than or equal to USD 0. |None |
|Total number of clusters you can create in a region |* China (Beijing): 4<br><br>* China (Guangzhou): 2<br><br>* China (Shanghai): 2<br><br>* Asia Pacific (Johor): 2<br><br>* Asia Pacific (Jakarta): 2<br><br>* China (Hong Kong): 2 |[Submitting an application in the quota center](https://docs.byteplus.com/en/docs/vke/Limits?TagIDs=2,255#SAoYyaXa) |
|Total number of nodes you can create in a cluster |* China (Beijing): 100<br><br>* China (Guangzhou): 100<br><br>* China (Shanghai): 100<br><br>* Asia Pacific (Johor): 100<br><br>* Asia Pacific (Jakarta): 100<br><br>* China (Hong Kong): 100 |[Submitting an application in the quota center](https://docs.byteplus.com/en/docs/vke/Limits?TagIDs=2,255#SAoYyaXa) |
|Total number of node pools you can create in a cluster |* China (Beijing): 10<br><br>* China (Guangzhou): 10<br><br>* China (Shanghai): 10<br><br>* Asia Pacific (Johor): 10<br><br>* Asia Pacific (Jakarta): 10<br><br>* China (Hong Kong): 10 |[Submitting an application in the quota center](https://docs.byteplus.com/en/docs/vke/Limits?TagIDs=2,255#SAoYyaXa) |
|Total number of kubeconfig certificates that can be generated in a cluster |BytePlus account and its IAM user (respectively):<br><br><br>* Private network KubeConfig: 5<br><br>* Public network access configuration: 5<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The quotas for the BytePlus account and its IAM user are independently allocated and do not affect each other.</div><br> |None |
|Total number of resource labels you can add to a cluster |50 |None |


<span id=".a3ViZXJuZXRlcy3pm4bnvqTop4TmqKE="></span>
## Scale of a Kubernetes cluster

The following table displays the scale of a Kubernetes cluster within one account supported by VKE.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about resource sizes and quantity limits related to large\-scale clusters, see <a href="https://docs.byteplus.com/en/docs/vke/Large-scale_cluster_limits_and_suggestions">Large\-scale cluster limits and suggestions</a>.</div>



|Category |Default scale |Maximum number |Method of applying for the maximum scale |
|---|---|---|---|
|Number of nodes |* VPC\-CNI cluster: 100<br><br>* Flannel cluster: 200 |* VPC\-CNI cluster: 5,000<br><br>* Flannel cluster: 1,000 |Contact the corresponding BytePlus VKE point of contact (POC). |
|Number of pods |3,000 |* With NetworkPolicy enabled: 50,000<br><br>* With NetworkPolicy disabled: 150,000 ||
|Number of ConfigMaps/Secrets |600 |12,000 ||
|Number of PVs/PVCs |2,000 |60,000 ||
|Number of Services |200 |6,000 ||
|Number of custom resources |2,000 |60,000 ||
|etcd capacity |8 GiB |16 GiB ||
|Size of a single ConfigMap, Secret, or custom resource |\- |1 MiB ||
|Total size of each type of etcd object |200 MiB |800 MiB ||


<span id=".6IqC54K55rGg6YWN6aKd6ZmQ5Yi2"></span>
## Node pool quotas

The following table displays the quotas of a single node pool. For more information on how to view the detailed node pool resource quotas within the current account, refer to the [View and apply for quotas](https://docs.byteplus.com/en/docs/vke/Limits?TagIDs=2,255#SAoYyaXa) section of this topic.


|**Limitation item** |**Quota within a single account** |**Method of Applying for More Quota** |
|---|---|---|
|Total number of resource labels that can be added to a node pool |50 |None |
|Total number of ECS instance labels that can be added to a node pool |20 |None |
|Total number of subnets that can be associated with a node pool |8 |None |
|Total number of security groups that can be associated with a node pool |5 (including the default security groups) |None |


<span id=".5L6d6LWW5bqV5bGC5LqR5Lqn5ZOB6YWN6aKd6ZmQ5Yi2"></span>
## Dependent underlying cloud service quotas


|**Category** |**Limitation item** |**Quota within a single account** |**Method of Applying for More Quota** |
|---|---|---|---|
|Computing |Maximum number of ECS instances created at a time |100 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of network interface cards (NICs) that can be mounted on an ECS instance (including one primary NIC) |The number of NICs that can be mounted on an ECS instance varies based on the instance type. For more information, refer to [Instance type and specifications](https://docs.byteplus.com/en/docs/ecs/General-purpose). |None |
|Network |Number of VPCs that can be created for an account in a region |10 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of subnets that can be created in a VPC |100 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of route tables that can be created in a VPC |10 (including one system route table and nine custom route tables) |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of custom route entries that can be created in a route table |200 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of ENIs that can be created for an account in a region |100 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of EIPs that can be created for an account in a region |20 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of security groups that can be created for an account in a region |300 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of rules that can be added to a security group (including inbound rules and outbound rules) |200 |None |
|Block storage |Maximum usage of a cloud disk type available for an account in a region |64 TiB |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
|CLB |Number of CLB instances that you can create |60 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Total number of times that each CLB instance can be associated with a back\-end server |200<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of times that a user repeatedly adds the same back\-end ECS instance (using the same IP address) to different server groups is counted.</div><br> |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of listeners that can be added to a CLB instance |50 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of forwarding rules that can be added to an HTTP or HTTPS listener |50<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default forwarding rule is not counted.</div><br> |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
||Number of access control policy groups that can be associated with a listener |5 |None |


<span id="SAoYyaXa"></span>
## Viewing and applying for quotas

VKE connects to the BytePlus quota center. You can view the resource usage of VKE within your account and apply for higher quotas for some of the resources.


1. Log in to the [Quota Center](https://console.byteplus.com/quota/productList).

2. On the **Product list** page, search for **vke**, and click **vke**.

3. On the page that appears, view quota parameters related to Vital Container Instance (VCI).

   You can apply for a higher quota for a supported resource based on your business requirements.
