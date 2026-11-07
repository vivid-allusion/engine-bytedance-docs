---
title: "Reserved Instances (RI) matching rules"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Reserved-instances-match-Pay-as-you-go-instance"
---

Reserved Instance coupons must be matched to Pay\-as\-you\-go instances before they can be used for bill deduction. This article mainly describes the matching rules between Reserved Instance coupons and Pay\-as\-you\-go instances, excluding spot instances.

<span id=".5Yy56YWN6KeE5YiZ"></span>
## Matching rules

After purchasing Reserved Instances (RI), the RI will automatically match Pay\-as\-you\-go instances that meet the conditions within the validity period. Manual matching is not supported. After a successful match, Reserved Instances (RI) check eligible Pay\-as\-you\-go instances every hour and apply deductions to the bill for instance resources (vCPU, GPU, and memory) according to the compute capacity specified on the RI.

The match conditions for regional RIs and zonal RIs differ. The following attributes determine whether a Reserved Instance (RI) can successfully match a Pay\-as\-you\-go instance.


|Comparison criteria |Zonal RI |Regional RI |
|---|---|---|
|Region and AZ |Only pay\-as\-you\-go instances within the **same region and availability zone** can be matched. |Availability zone flexibility allows you to match Pay\-as\-you\-go instances across **different availability zones within the same region**. |
|Instance type |Only Pay\-as\-you\-go instances with the **same specification and size** as the Reserved Instances (RI) can be matched. |Supports instance type flexibility, allowing flexible deduction for all instances in the **same instance family** as the Reserved Instances (RI). |
|Resource reservation |**Supports** resource reservation, allowing you to reserve a specified number and type of instances within the validity period to ensure that instances can be successfully created at any time in the designated availability zone. |**Does not support** resource reservation. |


<span id=".5Yy56YWN56S65L6L"></span>
## Matching example


<Tabs>
<Tab zoneid="eSPKc6aEaV" title="Zonal RI matching example">
<TabTitle>Zonal RI matching example</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">According to the matching rules, the Zonal RI and Pay\-as\-you\-go instances to be matched must meet the following conditions:</div>



* <div data-tips="true" data-tips-type="default">The region and the availability zone are the same.</div>


* <div data-tips="true" data-tips-type="default">The instance types are the same.</div>



Hourly matching examples of Zonal RIs and pay\-as\-you\-go instances are shown in the following table.


|**Scenarios** |**Reserved Instances (RI)**  |**Pay\-as\-you\-go instances** |**Effect of deduction** |
|---|---|---|---|
|100% match |One Reserved Instance (RI) voucher within its validity period, with the following attributes:<br><br><br>* China (Beijing) 2 availability zone A<br><br>* ecs.g2i.2xlarge<br><br>* Number of instances: 5 |Five pay\-as\-you\-go instances with the following configuration:<br><br><br>* China (Beijing) 2 availability zone A<br><br>* ecs.g2i.2xlarge |One Reserved Instance (RI) can be fully matched with five Pay\-as\-you\-go instances, and each RI deducts 100% of the bill for five Pay\-as\-you\-go instances per hour. |
|Partial match and<br><br>Resource reservation |A Reserved Instance (RI) coupon within its validity period, with the following attributes:<br><br><br>* China (Beijing) 2 availability zone A<br><br>* ecs.g2i.2xlarge<br><br>* Number of instances: 5 |Configuration for three pay\-as\-you\-go instances:<br><br><br>* China (Beijing) availability zone A<br><br>* ecs.g2i.2xlarge |Reserved Instances (RI) were successfully applied as a deduction to the bills for three pay\-as\-you\-go instances. In addition, two ecs.g2i.2xlarge instances will be reserved for you during the validity period of the coupon, ensuring that you can successfully create two Pay\-as\-you\-go instances at any time in China (Beijing) availability zone A. |
|Resource reservations |A Reserved Instance (RI) that is within its validity period has the following attributes:<br><br><br>* China (Beijing) 2 availability zone A<br><br>* ecs.g2i.2xlarge<br><br>* Instance count: 5 |No pay\-as\-you\-go instances of the same specification. |The Reserved Instance coupon is idle, but during its validity period, five ecs.g2i.2xlarge instances will be reserved for you, ensuring that you can create five Pay\-as\-you\-go instances at any time in Availability Zone A in China (Beijing). |
|Match failed |One Reserved Instance coupon within the validity period, with the following attributes:<br><br><br>* China (Beijing) 2 availability zone A<br><br>* ecs.g2i.2xlarge<br><br>* Number of instances: 2 |Two Pay\-as\-you\-go instances.<br><br><br>* The configuration of the first instance is as follows:<br><br>   * China (Beijing) 2 availability zone A<br><br>   * ecs.g2i.xlarge<br><br>* The configuration of the second instance is as follows:<br><br>   * China (Beijing) 2, Availability Zone B<br><br>   * ecs.g2i.2xlarge |2 pay\-as\-you\-go instances failed to match for the following reasons:<br><br><br>* The specifications of the first instance do not match those of the Reserved Instances (RI).<br><br>* The availability zone of the second instance does not match that of the Reserved Instances (RI).<br><br><br>Therefore, the Reserved Instances (RI) will remain unused, and the two pay\-as\-you\-go instances will continue to be billed on a pay\-as\-you\-go basis. |



</Tab>
<Tab zoneid="FsrS0xPE8f" title="Regional RI matching example">
<TabTitle>Regional RI matching example</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">According to the matching rules, the Regional RI and Pay\-as\-you\-go instances to be matched must meet the following conditions:</div>



* <div data-tips="true" data-tips-type="default">If the region is the same, matching across availability zones within the same region is supported.</div>


* <div data-tips="true" data-tips-type="default">The usage of Reserved Instances (RI) for different instance types within the same instance family can be evaluated based on computing power.</div>



Examples of hourly matching between Regional RI and pay\-as\-you\-go instances are shown in the following table.

> For instructions on how to view the normalization factor for an instance type, refer to[View normalization factor](https://docs.byteplus.com/en/docs/ecs/Check-normalization-factor).



|**Scenarios** ||**Regional RI** |**Pay\-as\-you\-go instances** |**Effect of deduction** |
|---|---|---|---|---|
|100% match |Match large\-denomination vouchers to small\-denomination instances |A Regional RI within its validity period, with the following attributes:<br><br><br>* All zones in China (Beijing) 2<br><br>* ecs.g2i.8xlarge<br><br>* Number of instances: 1<br><br>* normalization factor: 32 |Three pay\-as\-you\-go instances.<br><br><br>* The configuration of the first instance is as follows:<br><br>   * China (Beijing) 2 availability zone B<br><br>   * ecs.g2i.4xlarge<br><br>   * Normalization factor: 16<br><br>* The configuration of the remaining two instances is as follows:<br><br>   * China (Beijing) 2 availability zone A<br><br>   * ecs.g2i.2xlarge<br><br>   * Normalization factor: 8 |Hourly computing capacity of Reserved Instances (RI) and instances (that is, number of instances multiplied by the normalization factor) is as follows:<br><br><br>* Reserved Instances (RI): 1\*32=32<br><br>* The first Pay\-as\-you\-go instance: 1\*16=16<br><br>* The remaining 2 Pay\-as\-you\-go instances: 2\*8=16<br><br><br>Therefore, Reserved Instances (RI) are a perfect match for three Pay\-as\-you\-go instances. One RI can deduct 100% of the hourly bill for three Pay\-as\-you\-go instances. |
||Match small\-denomination vouchers to large\-denomination instances |One Regional RI within its validity period, with the following attributes:<br><br><br>* China (Beijing) all zones<br><br>* ecs.g2i.2xlarge<br><br>* Number of instances: 4<br><br>* normalization factor: 8 |A Pay\-as\-you\-go instance with the following configuration:<br><br><br>* China (Beijing) 2, Availability Zone B<br><br>* ecs.g2i.8xlarge<br><br>* Normalization factor: 32 |The per\-hour computing power for Reserved Instances (RI) and instances (that is, the number of instances multiplied by the normalization factor) is as follows:<br><br><br>* Reserved Instances (RI): 4\*8=32<br><br>* 1 pay\-as\-you\-go instance: 1\*32=32<br><br><br>Therefore, a Reserved Instance coupon (RI coupon) corresponds exactly to one pay\-as\-you\-go instance, and each RI coupon deducts 100% of the hourly bill for one pay\-as\-you\-go instance. |
|Partial match |Matching large\-denomination coupons with small\-denomination instances |One Regional RI within its validity period. Attributes are as follows:<br><br><br>* China (Beijing) cross\-availability zone<br><br>* ecs.g2i.8xlarge<br><br>* Instance count: 1<br><br>* normalization factor: 32 |The configuration for one pay\-as\-you\-go instance is as follows:<br><br><br>* China (Beijing) 2 availability zone B<br><br>* ecs.g2i.4xlarge<br><br>* Normalization factor: 16 |The per\-hour computing capacity of Reserved Instances (RI) and instances (that is, the number of instances multiplied by the normalization factor) is as follows:<br><br><br>* Reserved Instances (RI): 1\*32=32<br><br>* 1 Pay\-as\-you\-go instance: 1\*16=16<br><br><br>Therefore, the Reserved Instances (RI) were not fully utilized, with 50% of the deduction capacity remaining; the fees for pay\-as\-you\-go instance resources were fully deducted. |
||Match a small\-denomination voucher to a large\-size instance |One Regional RI within its validity period, with the following attributes:<br><br><br>* China (Beijing) all zones<br><br>* ecs.g2i.2xlarge<br><br>* Number of instances: 1<br><br>* Normalization factor: 8 |One pay\-as\-you\-go instance with the following configuration:<br><br><br>* China (Beijing) 2 availability zone B<br><br>* ecs.g2i.8xlarge<br><br>* Normalization factor: 32 |The per\-hour computing capacity of Reserved Instances (RI) and instances (that is, the number of instances multiplied by the normalization factor) is as follows:<br><br><br>* Reserved Instances (RI): 1\*8=8<br><br>* 1 pay\-as\-you\-go instance: 1\*32=32<br><br><br>Therefore, the Reserved Instances (RI) are fully utilized and can only deduct one quarter of the pay\-as\-you\-go instance bill. The remaining portion is still settled at the pay\-as\-you\-go price. |
|Match failed ||A Regional RI within its validity period, with the following attributes:<br><br><br>* All zones in China (Beijing) 2<br><br>* ecs.g2i.8xlarge<br><br>* Number of instances: 1 |2 Pay\-as\-you\-go instances,<br><br><br>* The configuration of the first instance is as follows:<br><br>   * China (Beijing) availability zone B<br><br>   * ecs.c2i.8xlarge<br><br>* Configuration for the second instance is as follows:<br><br>   * China (Shanghai) availability zone A<br><br>   * ecs.g2i.8xlarge |Both pay\-as\-you\-go instances failed to match. The reasons are as follows:<br><br><br>* The instance family of the first instance does not match the Reserved Instances (RI).<br><br>* The region of the second instance does not match the region of the Reserved Instances (RI). |



</Tab>
</Tabs>


&nbsp;
