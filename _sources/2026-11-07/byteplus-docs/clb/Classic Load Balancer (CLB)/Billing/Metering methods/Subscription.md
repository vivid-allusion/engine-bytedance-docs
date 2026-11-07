---
title: "Subscription"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Billing-04"
---

Subscription is a prepaid metering method, and is applicable to scenarios with long\-term use and relatively stable bandwidth requirements. This can significantly reduce your costs.

<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites

You have completed enterprise real\-name authentication for your account.

<span id=".6K6h6LS56K-05piO"></span>
## Billing description

**Single CLB instance fee = Instance fee + Specification configuration fee + Internet fee**


* **Instance fee** = instance unit price (USD/pc/month) × purchase duration (months)

   The current unit price for CLB instances is 0 USD/pc/month. If the price is adjusted later, see the information published on the respective pages.

* **Specification configuration fee** = specification unit price (USD/pc/month) × purchase duration (months)

   Different specifications have different performance limits. You are advised to select the specifications based on the service traffic, and fees will be charged according to the selected specifications. For more information about specifications, refer to Product specifications.

   The discount for CLB instances varies depending on the purchase duration; please refer to the actual purchase page for specific offers.

* **Internet fee**

   For a subscription public CLB instance, an Internet fee that includes only the bandwidth fee is charged. For the bandwidth unit price and billing details, refer to EIP subscription billing.


<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource pricing

You can view instance unit prices and specification prices in the [Price Calculator](https://www.byteplus.com/en/pricing?product=CLB&tab=2). These prices are for reference only; actual fees are subject to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

<span id=".6LS555So56S65L6L"></span>
## Fee example

Mr. Z purchased one subscription public CLB instance in China (Beijing) Region 2, specification Small I (bandwidth 200 Mbps), for 3 months, with an attached EIP bandwidth of 200 Mbps. The assumed prices at that time are as follows:


* The unit price for a small specification CLB is 54.00 USD/unit/month

* EIP: the unit price for bandwidth of (1–2) Mbps is 23.00 USD/month/Mbps, for (3–5) Mbps is 25.00 USD/month/Mbps, and for bandwidth greater than 5 Mbps is 100.00 USD/month/Mbps.


Therefore, Mr. Z's total fee is: 0 × 3 + 54.00 × 3 + [23.00 × 2 + 25.00 × 3 + 100.00 × (200\-5)] × 3 = 59,025 USD.

<span id=".6K6h6LS55ZGo5pyf"></span>
## Billing cycle

In the subscription billing method, a CLB instance can be purchased on an annual or monthly basis, and the billing cycle is the subscription duration (UTC+8 time).

For example, if you created a subscription CLB instance at 15:13:23 on January 12, 2022 and the subscription duration is 3 months, the expiration date would be 23:59:59 on April 12, 2022.
