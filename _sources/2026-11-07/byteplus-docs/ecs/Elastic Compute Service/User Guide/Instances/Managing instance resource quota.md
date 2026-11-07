---
title: "Managing instance resource quota"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management"
---

To prevent resource abuse, the platform sets resource quotas for ECS instances under each account by availability zone and billing method. For example, the maximum number of vCPUs or Elastic IPs (EIPs) you can use. This topic describes how to manage ECS resource quotas.

<span id=".6K-E5Lyw6LWE5rqQ6YWN6aKd"></span>
## Evaluating resource quota

Instance creation may fail if available quotas for resources such as vCPUs, volumes, or Elastic IPs (EIPs) are insufficient. Therefore, we recommend that you evaluate the available quotas of resources before creating an instance. Make sure that, under your account, the sum of existing resources and resources to be created does not exceed the corresponding quotas, so that instance creation does not fail due to quota limits. The specific limits are as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the main quota limits involved in creating instances are described here. For other quota limits on ECS\-related resources and resources for which the quotas can be changed, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Limits">Constraints</a>.</div>



|Limit item |Limit description |View/Change quota |
|---|---|---|
|vCPU |Maximum vCPUs or GPUs available for an instance type family configured with a specified billing method within an availability zone |For specific steps, please refer to [Viewing or changing quota](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management#.5p-l55yL5oiW6LCD5pW06YWN6aKd). |
|Volume |The maximum capacity of a volume used in a region. ||
|EIP |The number of EIPs that can be applied for within a region. ||


<span id=".5p-l55yL5oiW6LCD5pW06YWN6aKd"></span>
## Viewing or changing quota

If the default quota of an ECS\-related resource can not meet your business needs, and the resource allows quota change, you can view and change the quota in the following ways.


<Tabs>
<Tab zoneid="XYuh3m7Xr1" title="ECS instance quota">
<TabTitle>ECS instance quota</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view instance quotas by region, availability zone, and billing type. For the specific quota items and applicable instance type families, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management#.RUNT6KeE5qC86YWN6aKd6aG56K-05piO">Quota items based on ECS instance type</a>.</div>



1.  Log in to the [Quota Center console](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs).

2. On the "Product list" page, set the product category to "Compute" and click the "ecs" card.

3. Click on the product card. On the quota list page that appears, you can view or apply for a quota.

   * **View quota**: You can view the quota for each instance type family under the current account and the vCPU quota for all instance type families and current usage based on three dimensions: billing type, region, and availability zone.

   * **Apply for a higher quota **  : In the "Actions" column, click the "Apply" button. Follow the prompts to complete quota application.


</Tab>
<Tab zoneid="uTVoqOXR8e" title="EIP quota">
<TabTitle>EIP quota</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Volume/EIP quotas are general quotas and can only be viewed by region.</div>



1.  Log in to the [Quota Center console](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs).

2. On the "Product list" page, set the product category to "Network" and click the "EIP" card.

3. Click on the product card. On the quota list page that appears, you can view or apply for a quota.

   * View quota: You can view the default quota and current usage of the corresponding resource under the current account by region.

   * Apply for quota: In the "Actions" column, click the "Apply" button. Follow the prompts to complete quota application.


</Tab>
<Tab zoneid="MXG2eclkky" title="Volume quota">
<TabTitle>Volume quota</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view volume quota information by volume type, payment type, region, and availability zone.</div>



1.  Log in to the [Quota Center console](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs).

2. On the "Product list" page, set the product category to "storage" and click the "EBS" card.

3. On the quota list page, you can view or apply for volume quotas.

   * **View quota**: You can view the volume quota and current usage under the current account by volume type, payment type, region, and availability zone.

   * **Apply for a higher quota**: Click "Apply" in the "Actions" column. Follow the prompts to complete quota application.


</Tab>
</Tabs>


<span id=".RUNT6KeE5qC86YWN6aKd6aG56K-05piO"></span>
## Quota items based on ECS instance type

As shown in the following table, the quota center provides quota items based on ECS instance type and the applicable instance type families.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="0">warning</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">When applying for quota increase, you need to find the quota corresponding to the instance type/instance type family to be enhanced based on the following table. Select the corresponding quota item for enhancement. In addition, note whether the vCPU quota for all instance type families is sufficient. If not, an application is required. After the upgrade is completed and the application for increasing quota for a specific type family is approved, the vCPU quota for all instance type families will be automatically changed. No further application is required.</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">After the upgrade is completed, the vCPU quota for all instance type families ≥ Quota of regular vCPUs + Quota of local volume vCPUs + Number of vCPUs corresponding to quota of basic GPUs + Number of vCPUs corresponding to quota of high\-performance GPUs.</div>




|**Quota item** |vCPU quota for all instance type families (formerly vCPU quota) |Quota of regular vCPUs |Quota of local volume vCPUs |Quota of basic GPUs |Quota of high\-performance GPUs |
|---|---|---|---|---|---|
|Quota code |vcpu |general_vcpu |local_volume_vcpu |gpu_basic |gpu_high_performance |
|Scope of the instance type families |All types |* [General-purpose](https://docs.byteplus.com/en/docs/ecs/General-purpose)<br><br>* [Compute-optimized](https://docs.byteplus.com/en/docs/ecs/Computing-optimized)<br><br>* [Memory-optimized](https://docs.byteplus.com/en/docs/ecs/Memory-optimized)<br><br>* [Burstable instance](https://docs.byteplus.com/en/docs/ecs/Burstable-performance-instances)<br><br>* [General-purpose EBM](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM)<br><br>* [Compute-optimized EBM](https://docs.byteplus.com/en/docs/ecs/Compute-optimized-EBM) |* [Local SSD](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based)<br><br>* [Big Data](https://docs.byteplus.com/en/docs/ecs/Big-data-based)<br><br>* [Local SSD EBM](https://docs.byteplus.com/en/docs/ecs/Local-SSD-EBM) |[GPU Accelerated](https://docs.byteplus.com/en/docs/ecs/GPU-Compute) |[HPC-optimized](https://docs.byteplus.com/en/docs/ecs/High_Performance_Computing_Optimized_hpcpni3h) |
