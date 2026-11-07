---
title: "Billing details of Cloud DDoS Protection"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Billing_details_of_Cloud_DDoS_Protection"
---

Cloud DDoS Protection is a subscription\-based service billed monthly or yearly. To help you understand and estimate your costs, this document explains the pricing structure in detail. It covers the three main billable items—protection capability, service bandwidth, and the number of protected IP addresses—and provides a pricing example for your reference.

Built on BytePlus’s public cloud infrastructure with reserved bandwidth at its data centers, the product offers robust DDoS protection, with the maximum defense capacity dependent on the overall network capacity of the current data center.

This topic introduces how you will be charged for the use of BytePlus Cloud DDoS Protection service. A pricing example is also provided.

<span id="8b3575a3"></span>
## Billing model

The Cloud DDoS Protection supports monthly or yearly subscriptions. You are charged based on your selection of the items on the purchasing page. 

<span id="49d34b22"></span>
## Billable items

There are three billable items: protection capability, service bandwidth, and the number of protected IP addresses. Your total cost is the sum of these three items.

<span id="2d2d58b3"></span>
### Protection capability

By default, Cloud DDoS Protection provides full protection, defending against attacks up to the overall network capacity of BytePlus.


|**Specification** |**Unit price (per month)**  |
|---|---|
|Full protection |$4,000 |


<span id="5ecbdbd3"></span>
### Service bandwidth

Service bandwidth refers to the volume of clean traffic after filtering by the Cloud DDoS Protection engine, with billing based on this clean traffic volume. Each instance supports up to 20 Gbps of clean traffic bandwidth.


|**Specification (Mbps)**  |**Unit price (per 50 Mbps per month)**  |
|---|---|
|50 |$0 |
|50 ＜ Service bandwidth ≤ 1,000 |$10 |
|1,000 < Service bandwidth ≤ 5,000 |$8 |
|5,000 < Service bandwidth ≤ 20,000<br><br> |$6<br><br>See [Pricing example](https://docs.byteplus.com/docs/byteplus-ddos-protection/Billing_details_of_Cloud_DDoS_Protection#3c0be465) for more details. |


<span id="e69b0640"></span>
### Number of protected IP addresses

The number of protected IP addresses refers to the IPv4 and IPv6 addresses added to an instance for protection, with each instance supporting up to 500 IP addresses.


|**Specification (Quantity)**  |**Pricing (per IP address per month)**  |
|---|---|
|50 |$0 |
|50 ＜ Number of IP addresses ≤ 100 |$20 |
|100 ＜ Number of IP addresses ≤ 300 |$18 |
|300 ＜ Number of IP addresses ≤ 500 |$11 |


<span id="3c0be465"></span>
## Pricing example

For example, assume you configure a one\-month subscription with 1,000 Mbps of service bandwidth and 60 protected IP addresses. The base plan includes 50 Mbps of bandwidth and 50 IP addresses, so you will be charged for the additional 950 Mbps of bandwidth and 10 IP addresses. Therefore, the total monthly cost for your configuration is $4,390, which is the sum of the following items.


* $4,000 for basic specification

* $190 for additional service bandwidth: 950 / 50 \* $10 = $190

* $200 for additional IP addresses: 10 \* $20 = $200
