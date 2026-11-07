---
title: "Billing for IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/IPsec-VPN-connection-billing"
---

Using IPsec\-VPN (IPsec\-VPN connections attached to a Transit Router (TR)) incurs the IPsec\-VPN connection fee. Currently, the IPsec\-VPN connection supports only Pay\-as\-you\-go. This topic describes the metering method for IPsec\-VPN connections.

<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites


* You have completed [real-name authentication](https://docs.byteplus.com/en/docs/6261/64923) for your account before purchasing VPN Connect\-related resources.

* The total value of both the [available balance](https://docs.byteplus.com/en/docs/6269/100429) in your account and coupons available to IPsec\-VPN connection resources is not less than USD100.00. The available balance must be no less than 0. For detailed actions, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".6K6h6LS55Y2V5Lu3"></span>
## Resource pricing

You can check the billing items and fees related to using VPN Connect on the [Pricing calculator](https://www.byteplus.com/en/pricing?product=VPN&tab=2) page. The amount presented by the pricing calculator is for reference only. Actual charges are based on the final order in [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect).

<span id=".6K6h6LS55YWs5byP"></span>
## Formula

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Billing formulas in this topic only include the billing items on the IPsec\-VPN connection side. For formula details on TR side, see <a href="https://docs.byteplus.com/en/docs/83472/1223945">Transit Router Billing</a>.</div>


* <div data-tips="true" data-tips-type="tip">In the following text, the IPsec instance fee refers to the cost of one IPsec instance. The IPsec traffic fee refers to the cost of outbound traffic, which means you are billed only for the traffic transferred from the VPC to a data center or another VPC.</div>


* **IPsec\-VPN connection fee (USD) = IPsec instance fee (USD) + IPsec traffic fee (USD)** 

   * **IPsec instance fee (USD) = IPsec instance unit price (USD/hour) × usage duration (hours)** 

   * **IPsec traffic fee (USD) = Unit price for IPsec traffic (USD/GB) × Total outbound traffic (GB)** 


<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

In Pay\-as\-you\-go mode, the billing cycle and bill term are both calculated in natural hours. Every hour on the hour (UTC+8), a bill is issued and the corresponding amount is deducted from your account. For more information, see Bill management.

Overdue payments affect resources in Pay\-as\-you\-go mode, whose status changes depending on how long the payments are overdue. For more information, see Arrears.

Example:

An IPsec\-VPN connection associated with a TR was created at 14:37:15 on January 20, 2023, with the following three consecutive billing cycles.


* The first settlement cycle: From 14:00:00 to 14:59:59 on January 20, 2023.

* The second settlement cycle: From 15:00:00 to 15:59:59 on January 20, 2023.

* The third settlement cycle: From 16:00:00 to 16:59:59 on January 20, 2023.


<span id=".6LS555So56S65L6L"></span>
## Billing example

Mr. A creates an IPsec\-VPN connection with an associated TR on May 3, 2023, and transfers 1 GB of traffic to the local via the IPsec\-VPN connection during the period from 10:00:00 to 11:00:00 on the same day.


* Billing items: IPsec instance fee and IPsec traffic fee

* The total fee Mr. A must pay for this period is: IPsec instance fee + IPsec traffic fee = 0.328 USD/hour × 1 hour + 0.8 USD/GB × 1 GB = 1.13 USD.
