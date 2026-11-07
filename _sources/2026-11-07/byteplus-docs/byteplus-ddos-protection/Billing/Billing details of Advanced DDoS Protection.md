---
title: "Billing details of Advanced DDoS Protection"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing"
---

BytePlus Advanced DDoS Protection offers two instance types, each with a distinct billing model: a prepaid model for public network resources and a mixed prepaid/pay\-as\-you\-go model for domains on BytePlus CDN. This document provides a detailed breakdown of the billable items, pricing structures, and calculation examples for both instance types to help you understand and estimate your costs.

<span id="48869650"></span>
# Billing model

BytePlus Advanced DDoS Protection supports two types of instances. One type is for public network resources and can be used regardless of where your origin server is hosted. This type of instance supports an annual or monthly prepaid billing model. The other type is designed for domains on BytePlus CDN, enabling one\-click activation of DDoS protection for these domains. This type of instance supports a mixed billing model of annual or monthly prepaid and pay\-as\-you\-go.

<span id="9ab2df2d"></span>
# Basic specifications

Advanced DDoS Protection instances have basic specifications that are fixed at the time of purchase. The basic specifications contain the following items.


|**Instance type** |**Public network service** |**BytePlus** **CDN service** |
|---|---|---|
|Provisioning mode |DNS resolution |Associated with CDN |
|Protective resource |An exclusive IP |BytePlus CDN |
|Protection capability |Full protection |Full protection |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">If the DDoS attacks on your protected services impact our scrubbing center infrastructure, the center may implement blackholing. This can affect your services through measures like rate limiting or traffic blocking.</div>


<span id="f2ab4483"></span>
# Billable items

The billing items for different types of instances vary. This section explains the billing items, modes, and prices for the two instance types.

<span id="a309ceab"></span>
##  Instances for public network service

Public network service instances have three billable items: service bandwidth, number of protected ports, and number of protected domains.

<span id="3b9d1699"></span>
### Service bandwidth

You are charged for the actual traffic forwarded to and from the instance. This includes both traffic to your origin server and response traffic to clients. We recommend selecting a service bandwidth that is greater than both your typical back\-to\-origin traffic and response traffic.

If the actual bandwidth usage of your business consistently surpasses the service bandwidth you have allocated, it may lead to service disruptions due to potential packet loss. Therefore, we recommend choosing a bandwidth tier that meets your business requirements to avoid service disruptions.


|**Specification (Mbps)**  |**Pricing (USD/month)**  |
|---|---|
|50 |$10,000 |
|100 |$12,000 |
|200 |$13,700 |
|300 |$17,000 |
|500 |$21,000 |
|800 |$29,000 |
|1000 |$30,000 |
|2000 |$51,000 |


<span id="fbd4c48a"></span>
### Number of protected ports

The number of protected ports refers to the quantity of ports that the Advanced DDoS Protection instance can add for forwarding TCP or UDP rules.

Each instance allows you to add up to 50 port forwarding rules. If you require more rules, you can purchase additional capacity. Each additional block of 5 ports costs an extra $100 per month.


|**Specification (Quantity)**  |**Pricing (USD/month)**  |
|---|---|
|≤ 50 |$0 |
|＞50<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">The part exceeding 50 will be charged.</div><br> |$100 for every 5 additional ports |


For example, if you need 60 port forwarding rules, you will be charged for 10 additional rules, since the basic plan covers 50. Therefore, the total monthly cost for 60 port forwarding rules would be $200, which is calculated as (60 \- 50) / 5 \* $100.

<span id="837262a7"></span>
### Number of protected domains

The number of protected domains refers to the quantity of domains that the Advanced DDoS Protection instance can add for protection.

Each instance protects 50 domains for free, and more domains can be added if needed. Each additional block of 5 domains costs an extra $100 per month.


|**Specification (Quantity)**  |**Pricing (USD/month)**  |
|---|---|
|≤ 50 |$0 |
|＞50<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">The part exceeding 50 will be charged.</div><br> |$100 for every 5 additional domains |


For example, if you need to protect 60 domains, you will be charged for 10 additional domains, since the basic plan covers 50. Therefore, the total monthly cost for protecting 60 domains would be $200, which is calculated as (60 \- 50) / 5 \* $100.

<span id="19920f25"></span>
### Pricing example

You want to buy one instance of public network service for one month. The billable items are as follows.


|**Item** |**Specification** |
|---|---|
|Service bandwidth |1000 Mbps |
|Number of protected ports |100 ports |
|Number of protected domains |100 domains |



* Service bandwidth: $30,000.

* Number of protected ports: (100 \- 50) / 5 \* $100 = $1,000.

* Number of protected domains: (100 \- 50) / 5 \* $100 = $1,000.


Your total monthly expense is $30,000 + $1,000 + $1,000 = $32,000.

<span id="a45d9633"></span>
## Instances for BytePlus CDN service

If your domains use BytePlus CDN services, you can activate an Advanced DDoS Protection instance for BytePlus CDN to protect your domains against attacks. This type of instance includes an instance subscription fee, a domain quota fee, and a pay\-as\-you\-go data transfer fee.

<span id="e67e17be"></span>
### Subscription

The subscription fee for an Advanced DDoS Protection instance is $3,000 per month, payable on a yearly or monthly prepaid basis. Upon subscribing, you gain access to all the features of the instance.

<span id="2d800086"></span>
### Number of protected domains

The number of protected domains refers to the quantity of domains that the Advanced DDoS Protection instance can add for protection.

Each instance protects 50 domains for free, and more domains can be added if needed. For every additional 5 domains, an extra $100 should be paid for each month.


|**Specification (Quantity)**  |**Pricing (USD/month)**  |
|---|---|
|≤ 50 |$0 |
|＞50<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">The part exceeding 50 will be charged.</div><br> |$100 for every 5 additional domains |


For example, if you have 60 domains to be protected, you will be charged for the extra 10 domains as only 50 domains are covered by the basic plan. Therefore, the total monthly cost for protecting 60 domains would be $200, which is calculated as (60 \- 50) / 5 \* $100.

<span id="e509e3ac"></span>
### Data transfer out usage

The data transfer out usage fee is billed on a pay\-as\-you\-go basis. It is charged hourly for the data transferred out from BytePlus CDN. This section describes the bandwidth limitations and pricing for data transfer out.

<span id="6053abe4"></span>
#### Bandwidth limitation

During a monthly billing cycle, the Advanced DDoS Protection instance limits the bandwidth based on the volume of data transfer out. If the actual bandwidth consistently exceeds the bandwidth limit, packet loss may occur. To adjust the bandwidth limit, you can [submit a ticket](https://console.byteplus.com/workorder/create).

The corresponding bandwidth limits for cumulative monthly data transfer volumes are shown in the table below.


|**Data transfer out usage (TB)**  |**Bandwidth (Mbps)**  |
|---|---|
|0 ≤ Transferred data < 100 |50 |
|100 ≤ Transferred data < 500 |100 |
|500 ≤ Transferred data < 1000 |200 |
|1000 ≤ Transferred data < 2000 |300 |
|Transferred data ≥ 2000 |500 |


Let's assume that you have 80 TB of data transferred out from BytePlus CDN. The available bandwidth is limited to 50 Mbps. If your actual bandwidth consistently exceeds 50 Mbps, packet loss may occur.

<span id="22c369c4"></span>
#### Pricing details

The table below lists pricing details corresponding to different volumes of data transfer out usage.


|**Data transfer out usage (TB)**  |**Pricing (USD/GB/hour)**  |
|---|---|
|0 < Transferred data ≤ 100 |$0.0400 |
|100 < Transferred data ≤ 500 |$0.0320 |
|500 < Transferred data ≤ 1000 |$0.0240 |
|Transferred data ＞ 1000 |$0.0160 |


If 2 TB of data is transferred out from BytePlus CDN in one hour, the cost is calculated as follows: 2000 GB \* $0.0400 = $80.

<span id="1485c636"></span>
### Pricing example

Assume you purchase one Advanced DDoS Protection instance for the BytePlus CDN service for one month. The billable items are as follows.


|**Item** |**Specification** |
|---|---|
|Subscription |\- |
|Number of protected domains |100 domains |
|Data transfer out usage |80 TB |



* Subscription: $3,000.

* Number of protected domains: (100 \- 50) / 5 \* $100 = $1,000.

* Data transfer out usage: 80,000 GB \* $0.0400 = $3,200.


Your total upfront cost is $3,000 + $1,000 = $4,000. Additionally, you will be charged $3,200 at the end of the month for the 80 TB of data transfer usage.
