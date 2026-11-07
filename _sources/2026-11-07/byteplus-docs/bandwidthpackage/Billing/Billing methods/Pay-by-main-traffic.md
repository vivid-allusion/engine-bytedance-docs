---
title: "Pay-by-main-traffic"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-domain-traffic"
---

This topic describes Pay\-by\-main\-traffic details for Bandwidth Package.

<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites


* You have completed enterprise real\-name authentication for your account.

* Your account's [available balance](https://docs.byteplus.com/en/docs/6269/100429) is not less than USD 100.00. For specific procedure, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".6K6h6LS55YWs5byP"></span>
## Formula

**Bandwidth Package fee = Traffic unit price (USD/GB) × Main traffic (GB).** 

**Main traffic**: Refers to the greater of outbound and inbound traffic within a billing cycle.

<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

Both the billing cycle and the settlement cycle are on an hourly basis.

On the hour (UTC+8), the platform settles fees, issues bills and deducts payments. For details on bills, see [bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource pricing

You can view the price of a Bandwidth Package instance on the [Pricing Calculator](https://www.byteplus.com/en/pricing?product=BandwidthPackage&tab=2) page. The amount presented by Pricing Calculator is for reference only. Specific fees are subject to the amount on the actual order in [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

<span id=".6LS555So56S65L6L"></span>
## Billing example

On July 1, 2023, at 10:30:00, Mr. A creates a Pay\-by\-main\-traffic Bandwidth Package with BGP (multi\-ISP) in China (Beijing), setting the maximum bandwidth to 200 Mbps.


* At 11:00:00, he adds multiple Elastic IP Addresses (EIPs) to the Bandwidth Package.

* At 17:00:00, he removes these EIPs from the Bandwidth Package and releases the package.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ee245f3bbff62550f513463a2564482.png) </span>

Assuming the traffic unit price for Bandwidth Package was 0.80 USD/GB at that time. The cost for each specific billing cycle is as follows:


|Billing cycle |Outbound traffic (GB) |Inbound traffic (GB) |Main traffic (GB) |Pay\-by\-main\-traffic fee (USD) |
|---|---|---|---|---|
|10:00:00 \- 11:00:00 |0 |0 |0 |0 |
|11:00:00 \- 12:00:00 |36 |32 |36 |0.80 x 36 = 28.80 |
|12:00:00 \- 13:00:00 |72 |54 |72 |0.80 x 72 = 57.60 |
|13:00:00 \- 14:00:00 |80 |100 |100 |0.80 x 100 = 80.00 |
|14:00:00 \- 15:00:00 |40 |30 |40 |0.80 x 40 = 32.00 |
|15:00:00 \- 16:00:00 |15 |14 |15 |0.80 x 15 = 12.00 |
|16:00:00 \- 17:00:00 |14 |15 |15 |0.80 × 15 = 12.00 |
