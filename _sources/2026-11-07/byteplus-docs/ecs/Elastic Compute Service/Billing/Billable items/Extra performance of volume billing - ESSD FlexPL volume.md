---
title: "Extra performance of volume billing - ESSD FlexPL volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Extra-performance-of-volume-billing"
---

When you use an ESSD FlexPL data volume with a capacity greater than or equal to 500 GiB, you can purchase additional performance based on your business requirements. This article introduces the billing method, billing method conversion  of volume additional performance.

<span id="precautions"></span>
## Precautions


* The billing method for additional performance remains the same as the ESSD FlexPL data volume and cannot be set separately. For example, the billing method of the data volume is annual and monthly, and the billing method for additional performance is also annual and monthly, and cannot be set to billing by volume.

* Additional performance needs to be billed separately. After purchasing additional performance, the total cost of volume is calculated as follows:

   Total volume cost = system volume cost + data volume cost + additional performance cost

* If the additional performance type changes, the billing unit price will also change, effective immediately.


<span id="billing-method"></span>
## Billing method

Volume extra performance supports per\-volume billing and annual Monthly Flat mode; supports three types: balanced type, IOPS type, and throughput type, among which the balanced type and IOPS type have the same billing formula, as follows:


|Additional performance type |Billing method |Billing formula |Billing unit |
|---|---|---|---|
|Balanced type, IOPS type |Pay\-as\-you\-go |A postpaid model in which you use first and then pay, with billing cycles accurate to the second.<br><br>Fee = Unit Price × IOPS × Billing Hours |USD/IOPS/hour |
||Subscription |A prepaid model, that is, pay first and then use, and the purchase time is based on the month.<br><br>Cost = Unit price × IOPS × Purchase time, the purchase time is in months. |USD/IOPS/Month |
|Throughput type |Pay\-as\-you\-go to |A postpaid model in which you use first and then pay, with billing cycles accurate to the second.<br><br>Cost = Unit price × Throughput × Billing hours |USD/MBps/hour |
||Subscription |A prepaid model, that is, pay first and then use, and the purchase time is based on the month.<br><br>Cost = Unit price × throughput × Purchase time, and the purchase time is expressed in months. |USD/MBps/Month |


<span id="billing-method-conversion"></span>
## Billing method conversion

The additional performance of the volume can only be converted to the billing method with the volume, and separate conversion of the billing method is not supported. Volume billing currently only supports the amount of billing subcontract annual monthly, more information, please see the [Converting from pay-as-you-go to subscription](https://docs.byteplus.com/en/docs/ecs/Converting-from-pay-as-you-go-to-subscription).
