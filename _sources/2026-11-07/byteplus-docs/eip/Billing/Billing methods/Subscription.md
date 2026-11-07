---
title: "Subscription"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Subscription"
---

Elastic IP Addresses (EIPs) support Subscription, a prepaid billing method. This article explains the billing items and bandwidth unit prices for subscription EIPs in detail.

Pay\-by\-bandwidth under Subscription is abbreviated as Subscription.

<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites

You have completed real\-name authentication for your account.

<span id=".6LS555So6K-05piO"></span>
## Fee description

For pay\-by\-bandwidth EIPs, the BytePlus platform charges based on your specified maximum bandwidth.


|Billing item |Region |Maximum bandwidth |Formula |
|---|---|---|---|
|Bandwidth Fee |China (Beijing), China (Shanghai), China (Guangzhou), China (Hong Kong) |1 ~ 2 Mbps |Bandwidth fee = Unit price of bandwidth within 1\-2 Mbps (USD/month per Mbps) × Usage duration (months) × Bandwidth limit (Mbps) |
|||3 ~ 5 Mbps |Bandwidth fee = [Unit price of bandwidth within 1\-2 Mbps (USD/month per Mbps) × 2 (Mbps) + unit price of bandwidth within 3\-5 Mbps (USD/month per Mbps) × (Bandwidth limit \- 2) (Mbps)] × Usage duration (months) |
|||Over 5 Mbps |Bandwidth fee = [Unit price of bandwidth within 1\-2 Mbps (USD/month per Mbps) × 2 (Mbps) + Unit price of bandwidth within 3\-5 Mbps (USD/month per Mbps) × 3 (Mbps) + Unit price of bandwidth over 5 Mbps (USD/month per Mbps) × (Bandwidth limit \- 5) (Mbps)] × Usage duration (months) |
||Asia Pacific |1 ~ 5 Mbps |Bandwidth fee = Unit price of bandwidth within 1\-5 Mbps (USD/month per Mbps) × Usage duration (months) × Bandwidth limit (Mbps) |
|||Over 5 Mbps |Bandwidth fee = [Unit price of bandwidth within 1\-5 Mbps (USD/month per Mbps) × 5 (Mbps) + Unit price of bandwidth over 5 Mbps (USD/month per Mbps) × (Bandwidth limit \- 5) (Mbps)] × Usage duration (months) |


<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource price

You can view the price of EIP instances on the [Pricing calculator](https://www.byteplus.com/en/pricing?product=EIP&tab=2) page. The Pricing calculator provides reference prices. Specific fees are subject to the actual order result in [the EIP console](https://console.byteplus.com/eip/eips).

<span id=".6K6h6LS55ZGo5pyf"></span>
## Billing cycle

For subscription EIPs, billing cycles are settled on a monthly basis (non\-calendar month). You must make full payment for the EIPs when you purchase them.

For example, Mr. X applied for a subscription EIP at 14:12:32 on September 10, 2021. The usage duration of the EIP was two months, and the EIP expired at 23:59:59 on November 10, 2021.

<span id=".6LS555So56S65L6L"></span>
## Fee example

Mr. A applied for a subscription EIP on March 20, 2021. The maximum Internet bandwidth of the EIP was 15 Mbps, and the usage duration of the EIP was two months.

When applying for the EIP, Mr. A was required to pay a total fee of: [ 23.00 (USD/month per Mbps) × 2 (Mbps) + 25.00 (USD/month per Mbps) × 3 (Mbps) + 100.00 (USD/month per Mbps) × 10 (Mbps) ] × 2 (months) = 2242 (USD). The EIP expires at 23:59:59 on May 20, 2021.
