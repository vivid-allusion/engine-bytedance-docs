---
title: "Volume billing"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Volume-billing"
---

This topic offers examples on fee calculation and describes the billing methods of volumes and converts to a billing method.

<span id="precautions"></span>
## Precautions

Data volumes and system volumes are billable items. You are charged for these items by unit price, capacity, and usage period. The same volume type may have different prices in different Regions. The price in the console shall prevail.

<span id="billing-methods"></span>
## Billing methods

This service supports the pay\-as\-you\-go billing method and the subscription billing method. For details on the pricing of cloud disks, please refer to the [pricing details](https://www.byteplus.com/en/pricing?product=volume&tab=1).


|Billing methods |Description |Billing Unit |Related Document |
|---|---|---|---|
|Pay\-as\-you\-go |Pay the price after you use the service. The billing cycle is measured in seconds.<br><br>Fee = Unit price of volume × Capacity × Usage period |USD/GiB/hr |[Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) |
|Subscription |Pay the price by month before you use the service.<br><br>Fee = Unit price for capacity × Capacity × Subscription period (months). |USD/GiB/month |[Subscription](https://docs.byteplus.com/en/docs/ecs/Subscription) |


<span id="billing-method-conversion"></span>
## Billing method conversion

You can convert your billing method from pay\-as\-you\-go to subscription. For more information, refer to [Converting from pay-as-you-go volumes to subscription](https://docs.byteplus.com/en/docs/ecs/Changing-pay-as-you-go-volumes-to-subscription-volumes).


* System volume: By default, the billing method of a system volume is convertd when you convert that of its instance.

* Data volume: When you convert the billing method of an instance from pay\-as\-you\-go to subscription, you can select whether to convert the billing method of a data volume attached on the instance from pay\-as\-you\-go to subscription.
