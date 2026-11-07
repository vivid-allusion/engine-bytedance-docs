---
title: "Billing overview"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Billing_overview"
---

This article describes the billing methods, instance lifecycle, and pricing for Table Storage for HBase.

<span id=".6K6h6LS557G75Z6L"></span>
## Billing method


|Billing method |Description |Applicable scenarios |
|---|---|---|
|Pay\-as\-you\-go |Also known as post\-paid. You are billed by the second based on your actual usage, and fees are deducted hourly from your account. For more details, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/HBase/Pay-as-you-go). |Suitable for short\-term needs with low business volume. Resources can be released immediately after use for flexibility and convenience. |
|Subscription |Also known as prepaid, you pay in advance for a specific duration when creating a new instance. For more details, see [Yearly or monthly subscription](https://docs.byteplus.com/en/docs/HBase/Yearly_or_monthly_subscription). |Suitable for long\-term business scenarios with stable traffic peaks. This option is more cost\-effective than Pay\-as\-you\-go. |


<span id="F791rdvQ"></span>
## Instance life cycle

The instance lifecycle is calculated differently depending on the billing method.


|Billing method |Instance lifecycle |
|---|---|
|Pay\-as\-you\-go |Billing starts after the instance is successfully created and ends when you release it. |
|Subscription |Billing starts when the instance is successfully created and is automatically released upon expiration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When a subscription instance expires, it is not released immediately. A specific retention policy applies. For more details, see <a href="https://docs.byteplus.com/en/docs/HBase/Arrears_and_expiration">Expiration</a>.</div><br> |


<span id=".5Lu35qC8"></span>
## Price

For more information about the pricing of HBase instances, see [Billing items and prices](https://docs.byteplus.com/en/docs/HBase/Billing_items_and_prices).
