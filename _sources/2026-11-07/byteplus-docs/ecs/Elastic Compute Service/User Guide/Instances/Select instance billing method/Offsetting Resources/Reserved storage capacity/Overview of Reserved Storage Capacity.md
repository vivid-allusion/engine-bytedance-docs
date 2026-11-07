---
title: "Overview of Reserved Storage Capacity"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Reserved-storage-capacity-overview"
---

Reserved Storage Capacity (RSC) is a voucher that can be used to offset bills and reserve resources. After purchasing RSC, you can use it to offset EBS bills for your pay\-as\-you\-go instances. RSC also reserves EBS resources for you, ensuring a stable supply.


* If you combine RSC with pay\-as\-you\-go volumes, you will receive discounts and lower costs compared to using pay\-as\-you\-go volumes alone.

* Compared with subscription volumes, RSC provides reserved resources at the time of purchase and can match any pay\-as\-you\-go volume that meets the requirements rather than being limited to a specific volume. This provides greater flexibility.


<span id=".5Z-65pys5qaC5b-1"></span>
## **Basic concepts**


|Term |Description |
|---|---|
|Reserved Storage Capacity (RSC) |A voucher that can be used to reserve resources and offset pay\-as\-you\-go EBS capacity costs. |
|Resource reservation |Before creating a volume, you can purchase RSC vouchers to reserve storage capacity. |


<span id=".55Sf5ZG95ZGo5pyf"></span>
## **Lifecycle**

The following table describes the statuses that RSC undergoes during its lifecycle.


|Status |Description |
|---|---|
|Creating |The state after you purchase an RSC voucher but before it becomes active. |
|Effective |The normal state. In this state, an RSC voucher can offset pay\-as\-you\-go EBS bills. Any unused portion reserves EBS resources equal to the remaining RSC. |
|Expired |The state of an RSC voucher after it expires or is unsubscribed. In this state, it can no longer offset pay\-as\-you\-go EBS bills. |


<span id=".5oq15omj6K-05piO"></span>
## Offset policy

For more information on offset conditions and methods, see [Offset policy](https://docs.byteplus.com/en/docs/ecs/Reserved-storage-capacity?lang=en&TagIDs=2,288,70,69,1,288,93,69#.5oq15omj6K-05piO).

<span id=".5Z-65pys5pON5L2c"></span>
## Basic operations


* [Purchasing Reserved Storage Capacity](https://docs.byteplus.com/en/docs/ecs/Purchase-a-reserved-storage-capacity)

* [Viewing Reserved Storage Capacity usage details](https://docs.byteplus.com/en/docs/ecs/View-reserved-storage-capacity-usage-details)
