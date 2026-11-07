---
title: "Pay-as-you-go"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-billing-by-volume"
---

TOS offers pay\-as\-you\-go pricing. This topic describes billing details, including the billing cycle and calculation formulas.

For more information on cost components and prices, see [TOS pricing](https://www.byteplus.com/en/pricing?product=TOS&tab=1).

<span id="e378c7b8"></span>
## Billing cycle

TOS generates bills based on hourly usage.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Bills may not be in real time. For example, you may receive a bill for 6:00–7:00 at 10:30.</div>


<span id="e851102e"></span>
## Billing formula

TOS settles fees on an hourly basis.

The pay\-as\-you\-go billing formula is: Cost = Actual usage × Applicable unit price.

Specifically, the storage cost is calculated as: Cost = Actual usage × Applicable hourly rate.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">As shown in the <a href="https://www.byteplus.com/en/pricing?product=TOS&tab=1">TOS pricing</a>, the storage pricing unit is ¥/GiB/month. In practice, the billing platform converts ¥/GiB/month to ¥/GiB/hour using the following formula: Hourly rate = Monthly rate ÷ 30 (days) ÷ 24 (hours).</div>
