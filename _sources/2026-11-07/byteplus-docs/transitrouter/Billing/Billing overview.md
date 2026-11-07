---
title: "Billing overview"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Billing-overview"
---

Transit Router (TR) enables interconnectivity for both cloud and on\-premises resources, within the same region or across different regions. Each type of interconnection scenario consumes distinct TR resources, which in turn involve different billing items and metering methods.

<span id=".6LSt5Lmw6KaB5rGC"></span>
## Purchase prerequisites


* You have completed real\-name authentication for your account before purchasing TR resources.

* When purchasing Pay\-as\-you\-go TR resources, ensure the total value of your account balance (cash balance) and available coupons is equal to or greater than USD 0. 


<span id=".6K6h6LS56aG5"></span>
## Billing item

Different TR resources support different billing items and metering methods, as detailed in the table below.


|Billable resources |Billing item |Metering method |Billing cycle |
|---|---|---|---|
|Attachment |[Attachment fee](https://docs.byteplus.com/en/docs/6979/155973#.5Zyw5Z-f5YaF6LS555So) |Pay\-as\-you\-go |hours |
||[Traffic processing fee](https://docs.byteplus.com/en/docs/6979/155973#.5Zyw5Z-f5YaF6LS555So) |Pay\-as\-you\-go |hours |
|TR bandwidth package |[Cross-regional charges](https://docs.byteplus.com/en/docs/6979/155973#.6Leo5Zyw5Z-f6LS555So) |Subscription |months |


<span id=".5LiN5ZCM57uE572R5Zy65pmv6K6h6LS55qaC5Ya1"></span>
## Billing overview of different scenarios

TR costs vary based on the actual networking scenario. Details are listed in the table below.


|Networking scenario |Intra\-region |Cross\-region |
|---|---|---|
|Interconnect different VPCs |TR cost = Attachment fee + Traffic processing fee |TR cost = Attachment fee + Traffic processing fee + Cross\-region bandwidth fee |
|Interconnect a VPC and an on\-premises data center (the data center is connected via VPN Connect)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In this scenario, fees include not only TR cost but also VPN cost (IPsec instance fee and IPsec traffic fee). For details, see <a href="https://docs.byteplus.com/en/docs/vpn/IPsec-VPN-connection-billing">IPsec\-VPN connection billing</a>.</div><br> |||
|Interconnect a VPC and an on\-premises data center (the data center is connected via Direct Connect)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In this scenario, fees include not only TR cost but also Direct Connect cost (port occupancy fee and outbound traffic fee). For details, see <a href="https://docs.byteplus.com/en/docs/directconnect/Billing-overview">Billing overview for Direct Connect</a>.</div><br> |||


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">By default, the TR <strong>attachment fee</strong> and <strong>traffic processing fee</strong> are charged to the account that creates the network instance. That is, the cross\-account attachment fee is charged to the account that owns the network instance attachment. When a fee payer is designated, cross\-account attachment fees are charged to the specified fee payer account.</div>


* <div data-tips="true" data-tips-type="default">The feature to designate a fee payer for TR is currently in the beta stage and is only available in China (Shanghai). To request a trial, please contact your account manager.</div>
