---
title: "ESI FAQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ESI_FAQs"
---


|Category |Question |
|---|---|
|Concept introduction |[What are Elastic Scheduled Instances (ESIs)?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5LuA5LmI5piv5by55oCn6aKE57qm5a6e5L6L77yf) |
|Billing rules |* [Are the ESI prices more favorable than Pay-as-you-go prices?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5by55oCn6aKE57qm5a6e5L6L55qE5Lu35qC855u45q-U5oyJ6YeP6K6h6LS55piv5ZCm5LyY5oOg77yf)<br><br>* [Can I reserve subscription-based instances?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5Y-v5Lul6aKE57qm5YyF5bm05YyF5pyI5a6e5L6L5ZCX77yf) |
|Instance type |[What instance type families support the purchase of ESIs?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5pSv5oyB6LSt5Lmw5by55oCn6aKE57qm5a6e5L6L55qE5a6e5L6L6KeE5qC85peP5pyJ5ZOq5Lqb77yf) |
|Reservation |* [How far in advance can I reserve ESIs?​](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5by55oCn6aKE57qm5a6e5L6L5pSv5oyB5o-Q5YmN5aSa5LmF6aKE57qm77yf)<br><br>* [What is the maximum number of pay-as-you-go instances that can be reserved?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5pyA5aSa5Y-v5Lul6aKE57qm5aSa5bCR5Y-w5oyJ6YeP6K6h6LS55a6e5L6L77yf)<br><br>* [Can I cancel an ESI order?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5Y-v5Lul5Y-W5raI6aKE57qm5ZCX77yf) |
|Instance release |[Will ESIs be interrupted and reclaimed?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5by55oCn6aKE57qm5a6e5L6L5Lya6KKr5Lit5pat5Zue5pS25ZCX77yf) |
|Instance configuration change |* [Do ESIs support change of billing methods?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5by55oCn6aKE57qm5a6e5L6L5pSv5oyB6L2s5o2i6K6h6LS55pa55byP5ZCX77yf)<br><br>* [Can I change instance types of ESIs?](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs#.5by55oCn6aKE57qm5a6e5L6L5Y-v5Lul5pu05pS55a6e5L6L6KeE5qC85ZCX77yf) |


<span id=".5LuA5LmI5piv5by55oCn6aKE57qm5a6e5L6L77yf"></span>
## What are Elastic Scheduled Instances (ESI)?

ESIs are pay\-as\-you\-go instances that support advance reservation. They are applicable for scenarios that require flexibility and ensure stable supply of resources. For details, refer to [Elastic Scheduled Instances (ESI) overview](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview).

<span id=".5pSv5oyB6LSt5Lmw5by55oCn6aKE57qm5a6e5L6L55qE5a6e5L6L6KeE5qC85peP5pyJ5ZOq5Lqb77yf"></span>
## What instance families support the purchase of ESIs?

To see the instance type families that support purchasing ESIs, please refer to [Creating ESIs](https://docs.byteplus.com/en/docs/ecs/Creating_ESIs#.5rOo5oSP5LqL6aG5).

<span id=".5by55oCn6aKE57qm5a6e5L6L55qE5Lu35qC855u45q-U5oyJ6YeP6K6h6LS55piv5ZCm5LyY5oOg77yf"></span>
## Are the ESI prices more favorable than Pay\-as\-you\-go prices?

Compared with Pay\-as\-you\-go, ESI allows you to save the costs of compute resources (vCPU and memory) by approximately 27%. The fees for storage and network are the same as pay\-as\-you\-go prices.

<span id=".5by55oCn6aKE57qm5a6e5L6L5pSv5oyB5o-Q5YmN5aSa5LmF6aKE57qm77yf"></span>
## How far in advance can ESIs be reserved?

For more rules of ESI reservation, refer to [Elastic Scheduled Instances (ESI)](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances#.6aKE57qm5ZKM5Lqk5LuY).

<span id=".5by55oCn6aKE57qm5a6e5L6L5Lya6KKr5Lit5pat5Zue5pS25ZCX77yf"></span>
## Will ESIs be interrupted and reclaimed?

No, they will not be reclaimed. You can manually [delete the instance](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances) after the business ends.

<span id=".5Y-v5Lul6aKE57qm5YyF5bm05YyF5pyI5a6e5L6L5ZCX77yf"></span>
## Can I reserve subscription\-based instances?

No, you cannot reserve subscription\-based instances. Currently, only pay\-as\-you\-go ESIs are available for purchase.

<span id=".5Y-v5Lul5Y-W5raI6aKE57qm5ZCX77yf"></span>
## Can I cancel an ESI order?

Yes, you can cancel an ESI order. After you create an ESI order, you can cancel the order within **30 minutes**. After cancellation, the reservation becomes invalid, and associated instances do not launch during the scheduled delivery period.

<span id=".5by55oCn6aKE57qm5a6e5L6L5pSv5oyB6L2s5o2i6K6h6LS55pa55byP5ZCX77yf"></span>
## Do ESIs support change of billing methods?

No, ESIs do not support changing billing methods.

<span id=".5by55oCn6aKE57qm5a6e5L6L5Y-v5Lul5pu05pS55a6e5L6L6KeE5qC85ZCX77yf"></span>
## Can I change instance types of ESIs?

No, you cannot change instance type for ESIs.

<span id=".5pyA5aSa5Y-v5Lul6aKE57qm5aSa5bCR5Y-w5oyJ6YeP6K6h6LS55a6e5L6L77yf"></span>
## What is the maximum number of pay\-as\-you\-go instances that can be reserved?

The maximum number of instances that can be reserved per order is determined by the vCPU number of the ESI. The maximum vCPU number available per account in an availability zone cannot exceed 300, and the maximum number of instances does not exceed 500. To increase the vCPU quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList).
