---
title: "Billing overview"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/billing-overview"
---

This topic introduces the billing information of Container Registry (CR), including its billable items, billing cycle, and billing method.

<span id="计费说明"></span>
## Billing description

Currently, BytePlus CR Enterprise Standard Edition instances are billed.


* **Enterprise Standard Edition instance**: tailored for enterprise\-level users and medium to large teams. It offers capabilities such as dedicated data storage, dedicated registry service, access control, image acceleration, and OCI artifact management to enterprises for secure managing and large\-scale distribution.


<span id="计费组成"></span>
## Billable items

The following table displays the billable items of CR.


|Billable Item |Description |Document |
|---|---|---|
|Instance fee |The fee incurred by an instance. An instance is billed from the moment it is created until it is successfully stopped or deleted. |[Instance fee](https://docs.byteplus.com/en/docs/cr/instance) |
|Network traffic fee |The fee incurred by the network traffic for pushing or pulling container images and Helm charts. |[Network traffic fee](https://docs.byteplus.com/en/docs/cr/network-traffic) |
|Storage capacity fee |The fee incurred by the storage capacity for managing and storing container images and Helm charts in the instance. |[Storage capacity fee](https://docs.byteplus.com/en/docs/cr/storage) |
|Namespace quota |The fee incurred when the default quota on the number of namespaces is exceeded. |[Namespace quota](https://docs.byteplus.com/en/docs/cr/namespace-quota) |
|OCI artifact repository quota |The fee incurred when the default quota on the number of OCI artifact repositories is exceeded. |[OCI artifact repository quota](https://docs.byteplus.com/en/docs/cr/repository-quota) |
|VPC quota |The fee incurred when the default quota on the number of virtual private clouds (VPCs) is exceeded. |[VPC quota](https://docs.byteplus.com/en/docs/cr/vpc-quota) |


<span id="计费示例"></span>
## Billing examples

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the actual cost required for creating an instance, refer to the calculation result in the <a href="https://console.byteplus.com/cr">console</a>.</div>


<span id="标准配额"></span>
### Within the default quotas

Suppose you created **1** Enterprise Standard Edition instance at 00:00 on April 1, 2022. After 1 month (**30 days**), the total public network outflow traffic used for pushing and pulling images over the public network was **500 MB**, while the total storage capacity used for managing images was **2 TiB**. Then, the total cost in **April** was as follows:


|Instance Fee |Public Network Outflow Traffic Fee |Storage Capacity Fee |Total Cost |
|---|---|---|---|
|USD 277.704 |USD 0.0364 |USD 39.813 |USD 317.5534 |
|= **1 instance** × USD 0.3857/hour/instance ×  **(24 × 30) hours** |= USD 0.0728/GB × (**500** ÷ 1000) GB |= USD 0.01944/GiB/month × (**2** × 1024) GiB × **1 month** |= USD (277.704 + 0.0364 + 39.813) |


<span id="超量配额"></span>
### Beyond the default quotas

Suppose you created **1** Enterprise Standard Edition instance at 00:00 on April 1, 2022. After 1 month (**30 days**), the total public network outflow traffic used for pushing and pulling images over the public network was **500 MB**, while the total storage capacity used for managing images was **2 TiB**. Additionally, you increased the namespace quota to **100**, the OCI artifact repository quota to **5,000**, and the VPC quota to **6**. Then, the total cost in **April** was as follows:


|Instance fee |Public Network Outflow Traffic Fee |Storage Capacity Fee |Total Cost |
|---|---|---|---|
|372.6432 USD |USD 0.0364 |USD 39.813 |USD 412.4926 |
|= 1 instance × (0.3857 + ((**100** \- 50) ÷ 10) × 0.01286 + ((**5000** \- 3000) ÷ 1000) × 0.02571 + USD (**6** \- 5) × 0.01714)/hour/instance × (24 × 30) hours |= USD 0.0728/GB × (500 ÷ 1000) GB |= USD 0.01944/GiB/month × (2 × 1024) GiB × 1 month |= USD (372.6432 + 0.0364 + 39.813) |


<span id="计费周期"></span>
## Billing cycle

CR is billed hourly based on the usage of all resources. For specific amount and billing time, refer to the BytePlus system.

<span id="计费方式"></span>
## Billing method

CR supports pay\-as\-you\-go billing mode. The amount in a bill is calculated by multiplying the usage by the unit price and is directly deducted from the balance of your BytePlus account.

<span id="renewal-rules"></span>
## Renewal rules

Resources subscribed on a yearly or monthly basis within the current mixed billing mode support automatic renewal. For more details, please refer to the [Automatic renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules).
