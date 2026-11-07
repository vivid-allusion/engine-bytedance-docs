---
title: "Pay-as-you-go"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pay-as-you-go"
---

Vital Container Instance (VCI) charges fees based on the number of instances you use. The pay\-as\-you\-go billing method is flexible, and it allows you to use resources on demand and enable and release them at any time. If you do not have long\-term usage requirements for VCI instances, you can choose this billing method.

<span id="费用计算公式"></span>
## Billing formula

The fee of a VCI instance is calculated based on the following formula:

**Instance fee** = (**Number of vCPUs** × **vCPU unit price** ＋ **Memory size** × **Memory unit price** ＋ **Number of GPUs** × **GPU unit price** + **Temporary storage capacity** × **Storage unit price**) × **Instance running duration**

<span id="按量计费单价"></span>
## Unit prices in the pay\-as\-you\-go billing method


|Instance Family |Resource Type |Unit Price (Billed in Seconds) |Billed in Hours |
|---|---|---|---|
|General purpose u1 |vCPU |USD 0.0000068779/second/core |USD 0.02476044/hour/core |
||Memory |USD 0.0000009058/second/GiB |USD 0.00326088/hour/GiB |
|General purpose n3i |vCPU |USD 0.0000109113/second/core |USD 0.03928068/hour/core |
||Memory |USD 0.000000979/second/GiB |USD 0.0035244/hour/GiB |



|Temporary Storage Space Type |Unit Price |Description |
|---|---|---|
|ESSD |USD 0/hour/GiB |* Currently, 20 GiB of storage space is offered for free.<br><br>* If you want more storage space, [submit a ticket](https://console.byteplus.com/workorder/create). |


<span id="其他资源费用"></span>
## Other resource fees

Using VCI also incurs fees for resources related to IaaS computing, networking, storage, and security as well as cluster management on Vital Kubernetes Engine (VKE). If you use other basic cloud resources, you are required to pay the service fees based on the corresponding billing description. The following table describes the billing information.


|Cloud Resource |Resource Description |Billing Description |
|---|---|---|
|VKE |Used to manage VKE clusters. |[VKE billing rules](https://docs.byteplus.com/en/docs/vke/Billing) |
|Elastic Block Storage (EBS) |Used to implement the block storage solution for cluster application data. |[EBS billing rules](https://docs.byteplus.com/en/docs/ecs/Volume-billing) |
|Virtual Private Cloud (VPC) |Used to build cluster networks and Ingresses for VKE clusters. |[VPC billing rules](https://docs.byteplus.com/en/docs/vpc/Billing) |
|Cloud Load Balancer (CLB) |Used to create load balancing resources for VKE clusters. |[CLB billing rules](https://docs.byteplus.com/en/docs/clb/Billing-01) |
|Elastic IP Address (EIP) |Used to enable communication between related resources and the internet. |[EIP billing rules](https://docs.byteplus.com/en/docs/ecs/Elastic-IP-Address-billing) |
|NAT Gateway |Used to enable communication between cluster nodes and the internet. |[NAT Gateway billing rules](https://docs.byteplus.com/en/docs/natgateway/Billing-overview) |
|Container Registry (CR) |Used to create cloud native artifacts and manage their full lifecycle. |[CR billing rules](https://docs.byteplus.com/en/docs/cr/billing-overview) |
