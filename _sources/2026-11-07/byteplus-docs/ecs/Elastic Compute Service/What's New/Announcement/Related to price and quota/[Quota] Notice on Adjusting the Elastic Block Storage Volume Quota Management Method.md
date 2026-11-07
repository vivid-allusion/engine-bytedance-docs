---
title: "[Quota] Notice on Adjusting the Elastic Block Storage Volume Quota Management Method"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Notice-on-adjusting-the-elastic-compute-service-volume-quota-management-method"
---

In order to manage volume quotas more granularly, BytePlus Elastic Block Storage will adjust its volume quota management method. These changes will take effect between **October 23 and November 23, 2025**.

<span id="RShtk0vn"></span>
## **Estimated Change Time**

October 23, 2025 \- November 23, 2025 (Beijing, China)

<span id="z8qzd0KG"></span>
## Change Description

In the [Quota Center console](https://console.byteplus.com/quota/productList), you can view capacity quotas for various types of volumes to help you assess resource usage. The changes are explained below.


* **Before the change**: Capacity quotas for different types of volumes were calculated and managed independently by region. Your account had independent volume capacity quotas in each region.

* **After the change**: Capacity quotas for different types of volumes are calculated and managed independently by availability zone and billing method. Your account will have independent volume capacity quotas for each availability zone and billing method.


<span id="V3joe4bw"></span>
## Impacts

After the change, the volume capacity quotas for each availability zone and billing method in your account will be consistent with the pre\-change quotas in the corresponding regions.

For example, the capacity quota for ESSD_PL0 volumes in the Asia Pacific (Johor) region was 64 TiB before the change. After the change, the capacity quota for ESSD_PL0 volumes in each availability zone and billing method in that region will also be 64 TiB.

Log in to the [Quota Center console](https://console.byteplus.com/quota/productList) to view the quotas for each zone and billing method. For more information, see [Managing instance resource quota](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management).
