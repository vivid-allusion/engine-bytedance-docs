---
title: "Extra performance billing - TSSD_TL0 Volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/extra-performance-billing-tssd-tl0-volume"
---

Additional performance with a TSSD_TL0 volume will be charged. This paper introduces the billing method and the conversion of the billing method for the additional performance cost of the TSSD_TL0 volume.

<span id="precautions"></span>
## Precautions

The billing method for additional performance remains the same as the TSSD_TL0 volume and cannot be set separately. For example, the billing method of the TSSD_TL0 volume is subscription, and the billing method for its additional performance is also subscription, which cannot be set to pay\-as\-you\-go.

<span id="billing-method"></span>
## Billing method

The additional performance of the TSSD_TL0 volume  supports per\-volume billing and monthly subscription models.


|Billing method |Description |Billing unit |Related Documentation |
|---|---|---|---|
|Pay\-as\-you\-go |A postpaid model in which you use first and then pay, with billing cycles accurate to the second.<br><br>Cost = Unit price × Throughput × Billing hours |USD/MBps/hour |[Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) |
|Subscription |A prepaid model, that is, pay first and then use, and the purchase time is based on the month.<br><br>Cost = Unit price × throughput × Purchase time, and the purchase time is expressed in months. |USD/MBps/month |[Subscription](https://docs.byteplus.com/en/docs/ecs/Subscription) |


<span id="billing-method-conversion"></span>
## Billing method conversion

The additional performance of the volume can only be converted to the billing method with the volume, and separate conversion of the billing method is not supported. For volume billing conversion, please see [Converting from pay-as-you-go volumes to subscription](https://docs.byteplus.com/en/docs/ecs/Changing-pay-as-you-go-volumes-to-subscription-volumes) and [Converting from subscription volumes to pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-volumes-to-pay-as-you-go).

<span id="billing-example"></span>
## Billing example

The following table shows the cost calculation process for the throughput SSD cloud disk with additional performance, assuming that 1 system disk and 1 data disk were purchased when the instance was created at 00:00:00 on March 31, 2024, and additional performance was configured for the data disk. The service life is 1 month, and the cloud disk specifications are as follows:


* System disk: Use a throughput SSD cloud disk with a capacity of 40 GiB.

* Data Disk: Uses a throughput SSD cloud disk with a capacity of 500 GiB.

* Extra performance: Configure 500 MB/s of additional throughput for throughput SSD disks.


1 MB/s is equal to 8 MBps. Since the unit price of additional performance is MBps, and the unit of additional performance is MB/s, unit conversion is required when calculating the additional performance cost of throughput SSD cloud disks.


|Billing method |Billing unit price and cycle |Fee (USD) |
|---|---|---|
|Pay\-as\-you\-go |* System volume:0.0003143 USD/GiB/hour<br><br>* Data volume: 0.0003143 USD/GiB/hour<br><br>* Additional performance: 0.0005214 USD/MBps/hour<br><br>* Duration of use: 1 × 30 × 24 = 720 hours |* System volume: 0.0003143 × 40 × 720 = 9.05184<br><br>* Data volume: 0.0003143 × 500 × 720 = 113.148<br><br>* Additional performance: 0.0005214 × 500 × 720 × 8 = 1501.632<br><br>* Total cost: 9.05184 + 113.148 + 1501.632 = 1623.83184 |
|Subscription |* System volume: 0.15 USD/GiB/month<br><br>* Data volume: 0.15 USD/GiB/month<br><br>* Additional performance: 0.375 USD/MBps/month<br><br>* Duration of use: 1 month |* System volume: 0.15 × 40 × 1 = 6<br><br>* Data volume: 0.15 × 500 × 1 = 75<br><br>* Extra performance: 0.375 × 500 × 1 × 8 = 1500<br><br>* Total cost: 6 + 75 + 1500 = 1581 |
