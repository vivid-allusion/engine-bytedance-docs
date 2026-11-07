---
title: "Reserved Storage Capacity"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Reserved-storage-capacity"
---

Reserved Storage Capacity (RSC) is a voucher that can be used to offset bills and reserve resources. After purchasing RSC, you can use it to offset your pay\-as\-you\-go EBS bills. RSC also reserves EBS resources for you, ensuring a stable supply. This topic mainly describes the billing method and offset policy for RSC.

For more information, see [Overview of Reserved Storage Capacity](https://docs.byteplus.com/en/docs/ecs/Reserved-storage-capacity-overview).

<span id=".6K6h6LS55pa55byP"></span>
## Billing method

RSC is prepaid. All fees are paid upfront. You can purchase it for one to nine months or one to three years.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Prices depend on the specifications you choose. For exact pricing, refer to the prices displayed in the <a href="https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance">ECS console</a> at the time of purchase.</div>


* <div data-tips="true" data-tips-type="tip">RSC automatically matches your pay\-as\-you\-go volume capacity every hour and offsets the hourly bills for that capacity.</div>



<span id=".5pyJ5pWI5pyf"></span>
## **Validity period**

RSC takes effect immediately after purchase, and billing begins at that time. Its validity period depends on how long it was purchased for, and it will automatically expire after that period ends. Specifically:


* **Effective time**: RSC takes effect at the start of the hour before the purchase time, rounded down to the previous full hour.

* **Expiration time**: The default expiration time is 23:59:59 on the same day of the target month. If the target month does not have that date, the expiration time defaults to 23:59:59 on the last day of that month.

   For example, you purchase RSC on June 1, 2024, at 22:45:00 for one year. The effective time, billing start time, and expiration time are June 1, 2024, at 22:00:00, June 1, 2024, at 22:00:00, and June 1, 2025, at 23:59:59, respectively.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once your RSC voucher has expired, its status will change to "Expired." You will no longer be able to offset pay\-as\-you\-go volume bills, and any unused reserved resources will be released. However, any pay\-as\-you\-go volumes created with the expired voucher will remain available and continue to be billed as usual, with no interruption to your business.</div>


<span id=".5oq15omj6K-05piO"></span>
## Offset policy

You can use RSC vouchers to offset your pay\-as\-you\-go EBS bills within their validity period. The offset conditions and calculation methods are as follows:

<span id=".5oq15omj5p2h5Lu2"></span>
### Offset conditions


|Category |Condition |
|---|---|
|Resource type |Offsetting is only available for pay\-as\-you\-go EBS bills. |
|Region and availability zone |Offsetting is only available for EBS resources in the same region and availability zone as the RSC voucher. |
|Volume specifications |Only volumes with the same specifications as the RSC voucher are eligible for offsetting. For example, an ESSD PL0 RSC voucher cannot offset bills for ESSD FlexPL volumes. |


<span id=".5oq15omj5pa55byP"></span>
### Offset methods

The RSC reset cycle is one hour. After purchasing an RSC voucher, you have a fixed amount of reserved capacity available for offset each hour during its validity period. Any unused portion of the reserved capacity automatically expires at the end of the hour and does not roll over to the next hour.

RSC is billed by the second and offsets bills on an hourly basis. The formula for hourly reserved capacity is as follows:

Hourly reserved capacity = Reserved capacity × 3,600 s

**Offset from future cycles**

The offset from future cycles is automatically triggered if the actual capacity exceeds the hourly reserved capacity. This method uses reserved capacity from future cycles in chronological order until the total remaining capacity reaches zero.

There is an upper limit to the total offset within a reset cycle. The total offset amount — the sum of the current and future offsets — cannot exceed twice the hourly reserved capacity. If the actual capacity exceeds your purchased RSC, you will be billed for the difference on a pay\-as\-you\-go basis. The formula for the total offset amount per hour is as follows:

Total offset amount per hour = 2 × Reserved capacity × 3,600 s

The offset method varies depending on the situation within a cycle. The details are as follows:


|**Actual capacity** |**Offset method** |
|---|---|
|Actual capacity ≤ Reserved capacity |The reserved capacity for the current cycle can offset the actual capacity entirely. Any unused portion automatically expires. |
|Reserved capacity < Actual capacity ≤ 2 × Reserved capacity |The reserved capacity for the current cycle is fully offset by the actual capacity. Meanwhile, reserved capacity from future cycles is used in advance. |
|2 × Reserved capacity < Actual capacity |The reserved capacity for the current cycle is fully offset by the actual capacity. Meanwhile, reserved capacity from future cycles is used in advance. Any capacity that exceeds twice the hourly reserved capacity is billed on a pay\-as\-you\-go basis. |


<span id=".5oq15omj56S65L6L"></span>
### **Examples**

**Example 1: Actual capacity ≤ Reserved capacity**

Suppose that on June 24, 2024, at 9:24:00, you purchase 50 GiB of ESSD PL0 RSC for one month. At 9:10:00 on June 24, 2024, you create a 20 GiB ESSD PL0 volume that you have not released since. The offset details for the 9:00:00–9:59:59 hour are as follows:


* Hourly reserved capacity available before expiration: 50 GiB × 3,600 s = 180,000 GiB·s

* Volume capacity during this hour: 20 GiB × 50 min × 60 s = 60,000 GiB·s

* Remaining reserved capacity for this hour: 180,000 GiB·s – 60,000 GiB·s = 120,000 GiB·s


The purchased RSC fully offsets the actual volume capacity. The unused portion (120,000 GiB·s) automatically expires and does not roll over to the next hour.

**Example 2: Reserved capacity < Actual capacity ≤ 2 × Reserved capacity**

Suppose that on June 24, 2024, at 9:24:00, you purchase 50 GiB of ESSD PL0 RSC for one month. You then create the following volumes:


* At 9:00:00 on June 24, 2024, you create a 50 GiB ESSD PL0 volume and release it at 9:30:00.

* At 9:40:00 on June 24, 2024, you create an 80 GiB ESSD PL0 volume.


The offset details for the 9:00:00–9:59:59 hour are as follows:


* Hourly reserved capacity available before expiration: 50 GiB × 3,600 s = 180,000 GiB·s

* Volume capacity during this hour: 50 GiB × 30 min × 60 s + 80 GiB × 20 min × 60 s = 186,000 GiB.s

* Shortfall after offset against the reserved capacity for this hour: 186,000 GiB.s − 180,000 GiB.s = 6,000 GiB.s

* Offset against the reserved capacity for the next hour: 180,000 GiB.s − 6,000 GiB.s = 174,000 GiB.s


Based on the above calculations, the actual volume capacity for this hour is 186,000 GiB.s. The reserved capacity for this hour is 180,000 GiB.s. The 6,000 GiB.s shortfall is deducted in advance from the 10:00:00–10:59:59 hour's reserved capacity. After this deduction, 174,000 GiB.s remain for future offsets in the 10:00:00–10:59:59 hour.

**Example 3: 2 × Reserved capacity < Actual capacity**

Suppose that on June 24, 2024, at 9:24:00, you purchase 50 GiB of ESSD PL0 RSC for one month. You then create the following volumes:


* At 9:00:00 on June 24, 2024, you create a 100 GiB ESSD PL0 volume and release it at 9:30:00.

* At 9:40:00 on June 24, 2024, you create a 200 GiB ESSD PL0 volume.


The offset details for the 9:00:00–9:59:59 hour are as follows:


* Hourly reserved capacity available before expiration: 50 GiB × 3,600 s = 180,000 GiB·s

* Volume capacity during this hour: 100 GiB × 30 min × 60 s + 200 GiB × 20 min × 60 s = 420,000 GiB.s

* Shortfall after offset against the reserved capacity for this hour: 420,000 GiB.s − 180,000 GiB.s = 240,000 GiB.s

* Shortfall after offset against the reserved capacity for the next hour: 240,000 GiB.s − 180,000 GiB.s = 60,000 GiB.s


Based on the above calculations, the actual volume capacity for this hour is 420,000 GiB.s. The reserved capacity for this hour is 180,000 GiB.s. The reserved capacity for the next hour (10:00:00–10:59:59) is used in advance to offset an additional 180,000 GiB.s. However, the total offset within a reset cycle cannot exceed twice the hourly reserved capacity. Consequently, the remaining 60,000 GiB.s cannot be offset by future reserved capacity. Instead, it is billed on a pay\-as\-you\-go basis.

<span id=".57ut6LS544CB6YCA6K6i5ZKM5Y2H57qn"></span>
## **Unsubscription and upgrade**

<span id=".6YCA6K6i"></span>
### **Unsubscription**

Currently, only **regular unsubscription** is supported for RSC. **Unsubscription in seven days without reasons** is not supported. You can submit an unsubscription request under [Billing center > Cancel subscription](https://console.byteplus.com/finance/unsubscribe/). After you unsubscribe, BytePlus will refund a portion of the amount you paid (minus coupon deductions, if applicable) to your BytePlus account, according to the cancellation rules. Used coupons are not refundable. For more information, see [Unsubscription](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

**Reserved resources and bill offset after unsubscription**

After you unsubscribe from an RSC voucher, its status changes from "Effective" to "Expired". Any unused reserved resources are released immediately. However, any pay\-as\-you\-go volumes created with the expired voucher will remain available and continue to be billed as usual, with no interruption to your business.

Even after you unsubscribe, the voucher can still offset pay\-as\-you\-go volume bills up to the next full hour. For example, if you unsubscribe at 13:35:00, the voucher can still offset bills before 14:00:00 on the same day.

<span id=".5Y2H57qn"></span>
### Upgrade

Although RSC cannot be upgraded, it supports stackable purchases. These purchases are equivalent to upgrading the capacity of a single reservation.

Suppose you purchase two 50 GiB RSC vouchers in the same region and availability zone, one at 10:30:00 and the other at 10:40:00 on January 31, 2024, with a one\-month duration. The effective time for both vouchers is 10:00:00 on January 31, 2024, and they expire at 23:59:59 on February 28, 2024. During the vouchers' validity period, 100 GiB of reserved capacity is applied every hour to offset volume charges. If the offset from future cycles is triggered, up to 200 GiB of volume charges can be offset per hour.
