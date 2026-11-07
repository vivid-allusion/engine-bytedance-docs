---
title: "Reserved Instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Reserved-instances"
---

Reserved instances (RIs) are instance vouchers that are billed separately and can be used to reserve resources and offset bills. After you purchase an RI, you can use it to reserve instance resources or offset the costs of compute resources (vCPUs, GPUs, and memory) for your Pay\-as\-you\-go instances (excluding Spot instances). This significantly reduces Pay\-as\-you\-go costs and gives you more flexibility in instance lifecycle management and O&M. This topic describes the billing methods and deduction rules for RIs.

For information on the types, precautions, and operation instruction of Reserved Instances (RI), please refer to [Reserved instances overview](https://docs.byteplus.com/en/docs/ecs/Reserved-instances-overview).

<span id=".6aKE55WZ5a6e5L6L5Yi45Lu35qC8"></span>
## RI pricing

The prices of Reserved Instances vary with specifications. The actual costs are displayed on the [Reserved Instances purchase page in the ECS console](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/ri/create?).

<span id=".6K6h6LS55pa55byP"></span>
## Billing method

RI can not be used separately. It needs to match pay\-as\-you\-go instances and can be used to deduct the bills of compute resources (vCPU and memory) for such pay\-as\-you\-go instances based on the computing power of the voucher. [Learn more](https://docs.byteplus.com/en/docs/ecs/Reserved-instances-match-Pay-as-you-go-instance).

<span id=".6LSm5Y2V5oq15omj6KeE5YiZ"></span>
### Bill deduction rules


* Second\-level billing, with deduction on an hourly basis.

   * Zonal RI can only deduct pay\-as\-you\-go instances in the same availability zone that have the same specification and size.

   * Regional RI can deduct all pay\-as\-you\-go instances in the same region that belong to the same specification family.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Regional RI is currently in Beta. If you need a trial, please contact the account manager to apply.      </div>
      

* If you have both RIs and coupons, the RIs will be used first.

* If you have multiple RIs, the one with an earlier expiration time is used for cost deduction first. If two RIs have the same expiration time, the one that takes effect earlier is used first. If they are the same in all aspects, one RI is randomly selected.


<span id=".5oq15omj56S65L6L"></span>
### Deduction examples

The following examples show the calculation process for using RIs to deduct pay\-as\-you\-go instance bills.


<Tabs>
<Tab zoneid="QLH4Fp8pTq" title="Regional RI">
<TabTitle>Regional RI</TabTitle>

Assume that one user created 2 pay\-as\-you\-go instances of g2i.2xlarge (normalization factor 8) at 13:00:00 on January 16, 2023 in China (Beijing) A. On the same day, the user released the two instances at 13:30:00. Then, the user created another pay\-as\-you\-go instance of g2i.4xlarge (normalization factor 16) in China (Beijing) B at 13:25:00 and released it at 13:55:00.

The user has a valid Regional RI that matches the China (Beijing) region, with instance type of g2i.4xlarge, and the number of instances is 1.

Then:

The actual usage duration of the 3 g2i instances is 1,800 seconds. The total consumption is: normalization factor \* number of instances \* actual usage duration = [ (8 \* 2）+（16 \* 1) ] \* 1,800 = 57,600 (hashrate \* seconds)

The total amount that can be deducted with the RI during the hour from 13:00:00 to 14:00:00 is: normalization factor \* number of instances \* 3,600 seconds = 16 \* 1 \* 3,600 = 57,600 (hashrate \* seconds)

So:

The Regional RI can deduct 100% of the hourly bills of the 3 pay\-as\-you\-go instances.


</Tab>
<Tab zoneid="G0HY7HOxbS" title="Zonal RI">
<TabTitle>Zonal RI</TabTitle>

<span id=""></span>
#### Example 1: RI deduction \> instance usage

Assume that one user created 2 pay\-as\-you\-go instances of g2i.2xlarge (normalization factor 8) at 13:00:00 on January 16, 2023 in China (Beijing) A. On the same day, the user released the two instances at 13:30:00. Then, the user created another pay\-as\-you\-go instance of g2i.2xlarge at 13:25:00 and released it at 13:55:00.

The user has a valid Zonal RI that matches the same availability zone as the instance, with instance type of g2i.2xlarge, and the number of instances is 5.

Then:

The actual usage duration of the three g2i.2xlarge instances is 1,800 seconds. The total consumption during the usage of the instances is: normalization factor \* number of instances \* actual usage duration = 8 \* 3 \* 1,800 = 43,200 (hashrate \* seconds)

The total amount that can be deducted with the Zonal RI during the hour from 13:00:00 to 14:00:00 on January 16, 2023 is: normalization factor \* number of instances \* 3,600 seconds = 8 \* 5 \* 3,600 = 144,000 (hashrate \* seconds)

So:

The RI can deduct 100% of the bills of the 3 pay\-as\-you\-go instances, and the balance after deduction for the 13:00:00~ 14:00:00 hour is: 144,000 \- 43,200 = 100,800 (hashrate \* seconds)

<span id=""></span>
#### Example 2: RI deduction < instance usage

Assume that one user created 2 pay\-as\-you\-go instances of g2i.2xlarge (normalization factor 8) at 13:00:00 on January 16, 2023 in China (Beijing) A. On the same day, the user released the two instances at 13:30:00. Then, the user created another pay\-as\-you\-go instance of g2i.2xlarge at 13:25:00 and released it at 13:55:00.

The user has a valid Zonal RI that is in the same availability zone as the instance, with instance type of g2i.2xlarge, and the number of instances is 1.

Then:

The actual usage duration of the 3 g2i.2xlarge instances is 1,800 seconds. The total consumption during the usage of the instances is: normalization factor \* number of instances \* actual usage duration = 8 \* 3 \* 1,800 = 43,200 (hashrate \* seconds)

The total amount that can be deducted with the RI during the hour from 13:00:00 to 14:00:00 on January 16, 2023 is: normalization factor \* number of instances \* 3,600 seconds = 8 \* 1 \* 3,600 = 28,800 (hashrate \* seconds)

So:

The Zonal RI can only deduct 2/3 of the bills of the 3 pay\-as\-you\-go instances (ie 28,800 hashrate \* seconds), and the remaining 1/3 (i.e. 14400 hashrate \* seconds) is still settled at the pay\-as\-you\-go price.


</Tab>
</Tabs>


<span id=".6K6h6LS56KeE5YiZ"></span>
## Billing rule

<span id=".5LuY5qy-57G75Z6L"></span>
### Payment type

RI supports full prepayment only, which means you pay all fees as a one\-off payment at purchase and no other fees will be incurred during the validity period.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you purchase an RI, it automatically matches your Pay\-as\-you\-go instances every hour and deducts their hourly bills. Regardless of whether the Pay\-as\-you\-go instance costs are deducted, you are still required to pay for the RI based on the payment type within the validity period.</div>


<span id=".6K6h6LS55ZGo5pyf"></span>
### Billing cycle

**Effective time**

You can purchase an RI by month (1 to 9 months) or year (1 to 5 years). After you purchase an RI, it takes effect immediately. The effective time is calculated on the hour. The billing starts from the effective time and ends at 23:59:59 of the expiration date.

For example, you have purchased an RI at 2022\-11\-01 22:45:00, with a validity period of one year. Therefore, the effective time and billing start time of this RI are 2022\-11\-01 22:00:00, and the end time is 2023\-11\-01 23:59:59. If you have a matching instance when you purchase an RI, the RI will be used to deduct the hourly bill from 2022\-11\-01 22:00 to 23:00 until the RI expires.

**Expiration**

After an RI expires, its status changes to **Expired**, and it can no longer be used to deduct bills for pay\-as\-you\-go instances. Reserved resources for which no pay\-as\-you\-go instance has been created will be released. However, the existing pay\-as\-you\-go instance will continue to run normally (and follow the pay\-as\-you\-go settlement rules) without interruption to your business.

<span id=".57ut6LS55ZKM6YCA6K6i"></span>
## Renewal and unsubscription

<span id=".57ut6LS5"></span>
### Renewal

Before an RI expires, you can refer to [ Renewal for reserved instances](https://docs.byteplus.com/en/docs/ecs/Reserved-instances-renewal) and extend its expiration date by renewing it. After you renew the RI, the new billing cycle starts from the expiration date of the last cycle.

<span id=".6YCA6K6i"></span>
### Unsubscription

Currently, RI only supports **regular unsubscription** and does not support **unsubscription in seven days without reasons**. You can make unsubscription in [Billing > Unsubscribe management](https://console.byteplus.com/finance/unsubscribe/). After you unsubscribe the RI, BytePlus will refund part of the amount based on unsubscription rules (refund the order amount paid in cash, excluding the portion deducted with coupons) to your BytePlus account balance. Note that used coupons can not be refunded.  For more information, please refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

**Status of reserved resources and bill deductions after unsubscription**

After an RI is unsubscribed, its status changes from **in effect** to **expired**. At this time, the reserved resources for which no pay\-as\-you\-go instance has been created will be released. However, the existing pay\-as\-you\-go instance will continue to run normally (and follow the pay\-as\-you\-go settlement rules) without interruption to your business. In addition, after the unsubscription, the end time before which the pay\-as\-you\-go instance bill can be deducted with this RI is calculated on the hour. For example, if you unsubscribe an RI at 13:35:00, you can use it to deduct the bill generated before 14:00:00 on the current day.
