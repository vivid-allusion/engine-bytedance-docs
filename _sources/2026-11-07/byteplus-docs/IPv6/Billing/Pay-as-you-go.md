---
title: "Pay-as-you-go"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go"
---

IPv6 Gateway charges IPv6 Internet bandwidth fees for IPv6 addresses with enabled IPv6 Internet bandwidth.

IPv6 Internet bandwidth supports two postpaid metering methods: Pay\-by\-data\-transfer and Pay\-by\-bandwidth\-cap. This topic details both.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Pay\-by\-data\-transfer under Pay\-as\-you\-go is referred to as Pay\-by\-data\-transfer.</div>


* <div data-tips="true" data-tips-type="tip">Pay\-by\-bandwidth\-cap under Pay\-as\-you\-go is referred to as Pay\-by\-bandwidth\-cap.</div>



<span id=".5qaC6L-w"></span>
## Overview

You can disable Pay\-as\-you\-go IPv6 Internet bandwidth at any time. After disabling, the platform issues the bill for the current billing cycle in the next cycle, and automatically deducts payments from the account balance.

<span id=".6LSt5Lmw5YmN5o-Q"></span>
## Prerequisites


* You have completed [enterprise authentication](https://docs.byteplus.com/en/docs/6261/64937) for your account.

* The total value of your account's [available balance](https://docs.byteplus.com/en/docs/6269/100429) and coupons usable for IPv6 Internet bandwidth is not less than USD 100.00, and the available balance must be no less than 0. For details, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".5oyJ5bim5a695LiK6ZmQ6K6h6LS5"></span>
## Pay\-by\-bandwidth\-cap

For Pay\-by\-bandwidth\-cap IPv6 Internet bandwidth, BytePlus platform charges based on your specified maximum bandwidth. When using IPv6 Internet bandwidth, the platform enforces rate limiting based on your maximum bandwidth. Configure the maximum bandwidth based on your actual business needs.

In the metering method of Pay\-by\-bandwidth\-cap, the usage duration for bandwidth fee is the actual usage period, with precision down to the second.

**Cost of Pay\-by\-bandwidth\-cap IPv6 Internet bandwidth = Bandwidth fee**, whose formula is as follows:


|Billing items |Bandwidth tiers |Unit price for BGP (Multi\-ISP) bandwidth (USD/Mbps per hour) |Formula |
|---|---|---|---|
|Bandwidth fee |1\-5 Mbps |0.063 |Bandwidth within 1\-5 Mbps:<br><br>Bandwidth fee = Unit price of bandwidth within 1\-5 Mbps (USD/hour per Mbps) × Usage duration (hours) × Maximum bandwidth (Mbps). |
||Over 5 Mbps |0.25 |Bandwidth over 5 Mbps:<br><br>Bandwidth fee = Unit price of bandwidth within 1\-5 Mbps (USD/Mbps per hour) × Usage duration (hours) × 5 + Unit price of bandwidth over 5 Mbps (USD/Mbps per hour) × Usage duration (hours) × (Maximum \- 5) (Mbps). |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The unit price for IPv6 Internet bandwidth is subject to <a href="https://console.byteplus.com/eip/ipv6s">the IPv6 Gateway console</a>.</div>


<span id=".5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5"></span>
## Pay\-by\-data\-transfer

Pay\-by\-data\-transfer for IPv6 Internet bandwidth charges based on the actual outbound data transferred. For scenarios with large bandwidth fluctuations, Pay\-by\-data\-transfer reduces costs compared to Pay\-by\-bandwidth\-cap.

**The fee for Pay\-by\-data\-transfer IPv6 Internet bandwidth = traffic fee**. The traffic fee is calculated as follows:


|Billing items |Formula |Unit price for BGP (Multi\-ISP) data transfer (USD/Mbps per hour) |
|---|---|---|
|Traffic fee |Data transfer fee = Data transfer unit price (USD/GB) × Outbound data usage (GB) |0.80 USD/GB |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The unit price for IPv6 Internet bandwidth is subject to <a href="https://console.byteplus.com/eip/ipv6s">the IPv6 Gateway console</a>.</div>


<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

Both the billing cycle and the settlement cycle are on an hourly basis.

On the hour (UTC+8), the platform settles fees, issues bills and deducts corresponding payments from your account balance. For details on bills, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".6LS555So56S65L6L"></span>
## Fee example

<span id=".5oyJ5bim5a695LiK6ZmQ6K6h6LS56LS555So56S65L6L"></span>
### Pay\-by\-bandwidth\-cap

On February 10, 2023, at 10:45:00, Mr. A enables Pay\-by\-bandwidth\-cap IPv6 Internet bandwidth for an IPv6 address, specifying ISP as BGP (multi\-ISP) and maximum bandwidth as 105 Mbps.


* At 15:15:00, the service volume decreases. He adjusts the maximum bandwidth to 15 Mbps.

* At 17:00:00, the service ends. He disables IPv6 Internet bandwidth.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bdf83f5e3be2854a54e4d302826ffa01.png) </span>

Assume the unit price for bandwidth within 1\-5 Mbps is 0.063 USD/Mbps per hour, and is 0.25 USD/Mbps per hour for bandwidth over 5 Mbps. The cost for each specific billing cycle is as follows:


|Billing cycle |Bandwidth fee (USD) |Cost (USD) |
|---|---|---|
|10:00:00 \- 11:00:00 |0.063 x 15/60 x 5 + 0.25 x 15/60 x(105 \- 5) = 6.32875 |6.33 |
|11:00:00 \- 12:00:00 |0.063 x 1 x 5 + 0.25 x 1 x (105 \- 5) = 25.315 |25.32 |
|12:00:00 \- 13:00:00 |0.063 x 1 x 5 + 0.25 x 1 x (105 \- 5) = 25.315 |25.32 |
|13:00:00 \- 14:00:00 |0.063 x 1 x 5 + 0.25 x 1 x (105 \- 5) = 25.315 |25.32 |
|14:00:00 \- 15:00:00 |0.063 x 1 x 5 + 0.25 x 1 x (105 \- 5) = 25.315 |25.32 |
|15:00:00 \- 16:00:00 |(0.063 x 15/60 x 5 + 0.25 x 15/60 x(105 \- 5)) + (0.063 x 45/60 x 5 + 0.25 x 45/60 x(15 \- 5)) = 8.44 |8.44 |
|16:00:00 \- 17:00:00 |0.063 x 1 x 5 + 0.25 x 1 x(15 \- 5) = 2.815 |2.82 |
|\- |Total |118.87 |


<span id=".5oyJ5a6e6ZmF5rWB6YeP6K6h6LS56LS555So56S65L6L"></span>
### Pay\-by\-data\-transfer

On February 10, 2023, at 10:30:00, Mr. B enables Pay\-by\-data\-transfer IPv6 Internet bandwidth for an IPv6 address, specifying ISP as BGP (multi\-ISP) and maximum bandwidth as 200 Mbps.


* At 11:00:00, the service starts.

* At 17:00:00, the service ends. He disables IPv6 Internet bandwidth.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d489cf45747d16de3ecef48edf9b70f3.png) </span>

Assume the data transfer fee at that time was 0.80 USD/GB. The cost for each specific billing cycle is as follows:


|Billing cycle |Traffic usage (GB) |Data transfer fee (USD) |Cost (USD) |
|---|---|---|---|
|10:00:00 \- 11:00:00 |0 |0 |0 |
|11:00:00 \- 12:00:00 |36 |0.80 x 36 = 28.80 |28.80 |
|12:00:00 \- 13:00:00 |72 |0.80 x 72 = 57.60 |57.60 |
|13:00:00 \- 14:00:00 |80 |0.80 x 80 = 64.00 |64.00 |
|14:00:00 \- 15:00:00 |40 |0.80 x 40 = 32.00 |32.00 |
|15:00:00 \- 16:00:00 |15 |0.80 x 15 = 12.00 |12.00 |
|16:00:00 \- 17:00:00 |14 |0.80 x 14 = 11.20 |11.20 |
|\-\- |\-\- |Total |205.60 |
