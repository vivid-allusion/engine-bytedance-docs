---
title: "Pay-as-you-go"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Billing-02"
---

Pay\-as\-you\-go is a billing pattern where you use first and pay later. You can activate and release resources on demand without purchasing a large amount of resources in advance.

<span id=".6K6h6LS55YWs5byP"></span>
## Formula

**Single CLB instance fee = Instance fee + Specification configuration fee + Internet fee**


* **Instance fee** = Instance unit price (USD/pc/hour) × usage duration (hours)

   The current CLB instance unit price is USD 0/pc/hour. If the price adjusts later, please see the announcements on the related pages.

* **Specification configuration fee** = unit price per specification (USD/pc/hour) × usage duration (hours)

* **Internet fee**: The pay\-as\-you\-go public CLB's EIP supports both bandwidth cap and actual traffic billing methods. See [pay-as-you-go billing for EIP](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go) for details.


<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource pricing

You can view the instance unit price and specification unit price in Price Calculator. These unit prices are for reference only; the specific fee should be based on the CLB console.

<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

Both the billing cycle and the settlement cycle are on an hourly basis.

On the hour of each hour (UTC+8), the platform settles fees, issues bills and deducts corresponding payments from your account balance.
