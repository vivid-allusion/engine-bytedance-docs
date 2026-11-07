---
title: "Pay-as-you-go"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Pay-as-you-go"
---

<span id=".5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5"></span>
## Pay\-by\-data\-transfer

<span id=".6LSt5Lmw5YmN5o-Q"></span>
### Prerequisites


* Your account must complete real\-name authentication before applying for a Vortex IP.

* The total value of your account's available balance and coupons applicable for Vortex IP must not be less than 100.00 USD, and the available balance must not be less than 0. 


<span id=".6K6h6LS55YWs5byP"></span>
### Billing formula

**The fee for pay\-by\-data\-transfer Vortex IP = instance configuration fee + traffic fee**. The formulas for calculating instance configuration fee and traffic fee are as follows:


|Billing item |Calculation formula |
|---|---|
|Instance configuration fee |Instance configuration fee = Vortex IP instance unit price (USD/hour) × usage duration (hours) |
|Traffic fee |Data Transfer Fee (USD) = traffic unit price (USD/GB) × traffic usage (GB) |



* Usage duration: The actual usage time, accurate to the second.

* Usage traffic: The sum of outbound traffic and inbound traffic.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The unit price of the Vortex IP instance and the unit price of traffic shall be subject to the <a href="https://console.byteplus.com/eip/region:eip+ap-southeast-1/vortexips">Vortex IP console</a>.</div>


<span id=".57uT566X5ZGo5pyf"></span>
### Settlement Cycle

Fees are calculated and settled on an hourly basis.

At the beginning of each hour (UTC+8), fees are settled and deducted and bills are generated. For details on bills, refer to [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".6LS555So56S65L6L"></span>
### Billing example

Mr. B applied for one pay\-as\-you\-go, pay\-by\-data\-transfer Vortex IP (service type: Dynamic data center proxy) on May 1, 2024, at 10:30:00.


* 11:00:00 Get started using the Vortex IP to access the target website.

* 17:00:00 The operation ends, and the Vortex IP is released.


Assume that the instance configuration fee of a single Vortex IP was 0.4 USD each per hour, and the unit price of traffic was 2.8 USD per GB. The following table describes the fees in each billing cycle.


|Billing cycle  |Instance configuration fee (USD) |Usage traffic (GB) |Data Transfer Fee (USD) |Pay\-by\-data\-transfer (USD) |
|---|---|---|---|---|
|10:00:00 ~ 11:00:00 |0.4 x0.5 = 0.2 |0 |0 |0.2 |
|11:00:00 ~ 12:00:00 |0.4 x1 = 0.4 |36 |2.8x 36 = 100.8 |101.2 |
|12:00:00 ~ 13:00:00 |0.4 x1 = 0.4 |72 |2.8x 72 = 201.6 |202 |
|13:00:00 ~ 14:00:00 |0.4 x1 = 0.4 |80 |2.8x 80 = 224 |224.4 |
|14:00:00 ~ 15:00:00 |0.4 x1 = 0.4 |40 |2.8x 40 = 112 |112.4 |
|15:00:00 ~ 16:00:00 |0.4 x1 = 0.4 |15 |2.8x 15 = 42 |42.4 |
|16:00:00 ~ 17:00:00 |0.4 x1 = 0.4 |14 |2.8x 14 = 39.2 |39.6 |
|\-\- |\-\- |\-\- |Total |722.2 |
