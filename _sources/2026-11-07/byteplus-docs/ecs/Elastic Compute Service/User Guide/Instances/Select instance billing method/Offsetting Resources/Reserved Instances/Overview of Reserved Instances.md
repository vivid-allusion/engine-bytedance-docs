---
title: "Overview of Reserved Instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Reserved-instances-overview"
---

Reserved Instances (RI) is an instance voucher with deduction and reservation capabilities. You can use it to deduct the bills for compute resources (vCPU, GPU, and memory) required by pay\-as\-you\-go instances (excluding spot instances). You can also use it to reserve resources to ensure stable supply.


* If you combine RI with pay\-as\-you\-go instances, it can offer significant price advantages, including discounts, compared to bills from pay\-as\-you\-go instances.

* Unlike subscription instances, RI provides computing power upon purchase instead of specific instances. Without being associated with a specific instance, pay\-as\-you\-go instances that meet the requirements can be matched with RI, which is more flexible than subscription instances.


<span id=".5L2_55So5Zy65pmv"></span>
## Applicable scenarios

For stable elastic scenarios, we recommend that you use RI to significantly reduce your costs.


* Automated operations: In auto scaling (AS) and other automated operation scenarios, RI can help you automatically create or delete instances. RI can adjust resource types and distributions based on factors such as business changes, peaks, and troughs.

* Elastic scenarios: The total resource amount remains relatively stable, but resources must be used flexibly based on business needs. In such scenarios, you can use RI to further reduce costs and improve efficiency.

* Resource locking: For critical elastic workloads or in scenarios with tight resource supply, RI can help you lock resources in advance to avoid availability risks.


<span id=".5Z-65pys5qaC5b-1"></span>
## Concepts


|Term |Description |
|---|---|
|RI |A deduction coupon can not be used alone and must be used with pay\-as\-you\-go instances. RIs can be divided into regional RI and zonal RI. |
|Zonal RI |Resource reservation is supported. In the same availability zone, zonal RI can deduct pay\-as\-you\-go instances that are the same type as that specified in RI. |
|Regional RIs |Resource reservation is not supported. But for all pay\-as\-you\-go instances of the same instance family in the same region, you can flexibly deduct bills with regional RIs. |
|resource reservation |If no instances are available for deduction by zonal RI, the system reserves instance resources for you with the same type and instance quantity in the availability zone, as specified in the RI. |
|Modifies RIs |It means that you can change the attributes of RI, such as number, availability zone, instance type, instance number. For more details, refer to [Modifying Reserved Instances](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances). |
|Normalization factor |It serves to abstractly represent the computing power of instances with different types. For details, refer to [Viewing normalization factor](https://docs.byteplus.com/en/docs/ecs/Check-normalization-factor). |
|Computing power |It refers to the total computing power that RIs can offset. One RI can only offset resource usage equal to its total computing power per hour.<br><br>**Computing power=normalization factor \* instance quantity** |


<span id=".6aKE55WZ5a6e5L6L5Yi457G75Z6L"></span>
## RI types

The platform provides regional RI and zonal RI. The comparison is as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Regional RI is currently in Beta. If you need a trial, please contact your account manager to apply.</div>



|Item |Zonal RI |Regional RIs |
|---|---|---|
|Resource reservation capability |Resource reservation is **supported**. Zonal RI ensures that you can create pay\-as\-you\-go instances of the specified types and quantity within the validity period of RI. |Resource reservation is **not supported**. |
|Availability zone flexibility |Zonal RI supports matching with pay\-as\-you\-go instances in the **same availability zone** as the RI specified zone. |Regional RI allows matching with pay\-as\-you\-go instances in **different availability zones within the same region**. |
|Instance type flexibility |Pay\-as\-you\-go instances of the **same type** as that specified in RI can be matched. |Regional RI can flexibly offset pay\-as\-you\-go instances within the same region that belong to **the same instance family** as the instance family specified in RI. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* About instance quantity:

   The number of instances that an RI can offset or reserve is determined by the number of vCPUs in the instance. By default, in a single availability zone, the total number of vCPUs that can be offset by all RIs owned by an account is no more than 200. To increase your vCPU quota, go to the Quota center. [Learn more](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management).

* About instance type:

   * For details of instance families that support RI, refer to [Buying Reserved instances](https://docs.byteplus.com/en/docs/ecs/Buying-Reserved-instances#.5rOo5oSP5LqL6aG5).

   * For details of RIs that do not support changing instance types, refer to [Modifying Reserved Instances](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances#.5rOo5oSP5LqL6aG5). And for deduction or reservation of these instance types, you can only purchase zonal RIs.

* Regional RI and zonal RI support mutual conversion. For specific actions, refer to [Change Reserved Instances (RI) attribute](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances#.5pON5L2c5q2l6aqk).


<span id=".55Sf5ZG95ZGo5pyf"></span>
## Lifecycle

During the lifecycle, some status of RI are predefined, as listed in the following table:


|Status |State attribute |State description |
|---|---|---|
|Creating |Intermediate state |The status before RI enters **In effect** status after you purchase RI.<br><br>> The status of newly generated target RI after you make the change. |
|Enabled |Stable state |Normal status. You can use RI to deduct pay\-as\-you\-go instances bills. |
|During change |Intermediate state |The status of original RI after you change it. |
|Invalid |Stable state |If one RI is expired or canceled, it enters the **Expired** status.<br><br>> The status of original RI after you change it. |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


|Feature |Documentation |
|---|---|
|Billing methods/deduction rules/unsubscription |[RI](https://docs.byteplus.com/en/docs/ecs/Reserved-instances) |
|Purchasing RI |[Purchasing RI](https://docs.byteplus.com/en/docs/ecs/Buying-Reserved-instances) |
|Matching rules for RI and pay\-as\-you\-go instances |* [Reserved Instances (RI) match rules](https://docs.byteplus.com/en/docs/ecs/Reserved-instances-match-Pay-as-you-go-instance)<br><br>* [Viewing normalization factor](https://docs.byteplus.com/en/docs/ecs/Check-normalization-factor) |
|Modify RI types |[Modify the availability zone of RI](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances) |
|Split one RI with large computing power into multiple RIs with small computing power |[Split RI](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances#.5pON5L2c5q2l6aqk) |
|Merge multiple RIs with small computing power into one RI with large computing power |[Merge RI](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances#.5pON5L2c5q2l6aqk) |
|Renewing Reserved instances |[Renewing Reserved instances](https://docs.byteplus.com/en/docs/ecs/Reserved-instances-renewal) |


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

[Reserved Instances (RI) FAQs](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.6aKE55WZ5a6e5L6L5Yi46Zeu6aKY).
