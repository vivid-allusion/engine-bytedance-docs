---
title: "Pay-by-bandwidth"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-bandwidth"
---

This topic describes Pay\-by\-bandwidth details for Bandwidth Package.

<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites


* You have completed enterprise real\-name authentication for your account.

* The sum of both your [available balance](https://docs.byteplus.com/en/docs/6269/100429) and the coupons applicable to the Bandwidth Package is not less than USD 100.00, and the available balance must be no less than 0. For specific procedure, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".6K6h6LS55YWs5byP"></span>
## Formula

**Bandwidth Package fee = Bandwidth unit price (USD/hour per Mbps) × Maximum bandwidth (Mbps) × Usage duration (hours)** 


* **Maximum bandwidth:**  2\-5000 Mbps

* **Usage duration:**  Starts from the order creation time, with precision down to the second.


<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

Both the billing cycle and the settlement cycle are on an hourly basis.

On the hour (UTC+8), the platform settles fees, issues bills and deducts payments. For details on bills, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource pricing

You can view the price of a Bandwidth Package instance on the [Pricing Calculator](https://www.byteplus.com/en/pricing?product=BandwidthPackage&tab=2) page. The amount presented by Pricing Calculator is for reference only. Specific fees are subject to the amount on the actual order in [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

<span id=".6LS555So56S65L6L"></span>
## Fee example

On January 1, 2022, at 10:15:00, Mr. A created a Pay\-by\-bandwidth Bandwidth Package with BGP (multi\-ISP), setting the maximum bandwidth to 100 Mbps.

He adjusted the maximum bandwidth to 10 Mbps at 12:45:00, and released the Bandwidth Package at 13:00:00.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_12b30bd2c953b6a9a57f889bb662d799.png) </span>

Assuming the bandwidth unit price was 0.25 USD/hour per Mbps. The cost for each specific billing cycle is as follows:


|Billing cycle |Pay\-by\-bandwidth fee (USD) |
|---|---|
|10:00:00 \- 11:00:00 |0.25 x 100 x 45/60 = 18.75 |
|11:00:00 \- 12:00:00 |0.25 x 100 x 1 = 25.00 |
|12:00:00 \- 13:00:00 |0.25 x 100 x 45/60 + 0.25 x10 x 15/60 = 19.38 |
