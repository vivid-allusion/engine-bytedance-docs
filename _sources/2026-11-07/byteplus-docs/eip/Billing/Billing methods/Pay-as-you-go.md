---
title: "Pay-as-you-go"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Pay-as-you-go"
---

Elastic IP Address (EIP) supports Pay\-as\-you\-go billing, which includes two metering methods: Pay\-by\-bandwidth and Pay\-by\-data\-transfer. This topic details these two metering methods.


|Billing Type |Billing Description |Peak Billing Description |
|---|---|---|
|Pay\-by\-bandwidth |For Pay\-by\-bandwidth EIPs, the platform charges based on the specified maximum bandwidth. When using an EIP, the platform limits the rate for your specified bandwidth. Configure the maximum bandwidth based on the actual business requirements. |Peak bandwidth is a committed metric. In scenarios where bandwidth resource contention occurs frequently, peak bandwidth is guaranteed and remains unaffected by rate limiting. |
|Pay\-by\-data\-transfer |For Pay\-by\-data\-transfer EIPs, the platform charges based on your actual usage of outbound traffic. For scenarios with large bandwidth fluctuations, Pay\-by\-data\-transfer reduces costs compared to Pay\-by\-bandwidth. |Peak bandwidth serves only as the maximum upper limit and is not a committed metric. In scenarios where bandwidth resource contention occurs frequently, peak bandwidth may be subject to rate limiting. |


<span id="CChd9jWK"></span>
## Pay\-by\-bandwidth

<span id=".6LSt5Lmw5YmN5o-Q"></span>
### Prerequisites


* You have completed enterprise authentication for your account.


<span id=".6K6h6LS55YWs5byP"></span>
### Billing formulas

In Pay\-by\-bandwidth, the usage duration for the IP config fee and the bandwidth fee starts from the moment that the order is created, with precision down to the second.

**Fee for a Pay\-by\-bandwidth EIP = IP config fee + Bandwidth fee**. The formulas for IP config fee and Bandwidth fee are as follows:


|Billing item |Formula |
|---|---|
|IP config fee |IP config fee = EIP instance unit price (USD/hour) × Usage duration (hour).<br><br><br>* If an account's EIP quota in a region is less than 1000 (inclusive), the account is exempt from IP config fees for EIP instances associated with cloud resources in that region. That is, the EIP instance unit price is 0.<br><br>* The default EIP quota for a single account in a single region is 20. If you need to increase the quota, go to the Quota center to apply for a quota increase. |
|Bandwidth fee |Bandwidth within 1\-5 Mbps:<br><br>Bandwidth fee = Unit price of bandwidth within 1\-5 Mbps (USD/hour per Mbps) × Usage duration (hour) × Maximum bandwidth (Mbps). |
||Bandwidth over 5 Mbps:<br><br>Bandwidth fee = Unit price of bandwidth within 1\-5 Mbps (USD/hour per Mbps) × Usage duration (hour) × 5 + Unit price of bandwidth over 5 Mbps (USD/hour per Mbps) × Usage duration (hour) × (Maximum \- 5) (Mbps). |


<span id=".57uT566X5ZGo5pyf"></span>
### Settlement cycle

Both the billing cycle and the settlement cycle are on an hourly basis.

On the hour (UTC+8), the platform settles fees, issues bills, and deducts payments. For bill details, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".6LS555So56S65L6L"></span>
### Billing example

On January 1, 2022, at 10:45:00, Mr. A applies for a Pay\-by\-bandwidth EIP in China (Beijing) with BGP (multi\-ISP), setting the maximum bandwidth to 105 Mbps.


* At 11:00:00, he associates this EIP with an Elastic Compute Service (ECS) instance and enabled service.

* At 15:15:00, the service volume decreases. He adjusted the maximum bandwidth to 15 Mbps.

* At 17:00:00, service ends. The EIP was disassociated with the ECS instance and released.


Assume that the IP config fee per EIP is 0.02 USD/hour, the unit price of bandwidth within 1\-5 Mbps is 0.063 USD/hour per Mbps, and the unit price of bandwidth over 5 Mbps is 0.25 USD/hour per Mbps. Fees for each billing cycle are as follows:


|Billing cycle |IP config fee (USD) |Bandwidth fee (USD) |Pay\-by\-bandwidth (USD) |
|---|---|---|---|
|10:00:00\-11:00:00 |0.02 x (15/60) = 0.005 |0.063 x 15/60 x 5 + 0.25 x 15/60 x (105 \- 5) = 6.32875 |6.33 |
|11:00:00\-12:00:00 |Associated; 0 |0.063 x 1 x 5 + 0.25 x 1 x (105 \- 5) = 25.315 |25.32 |
|12:00:00\-13:00:00 |Associated; 0 |0.063 x 1 x 5 + 0.25 x 1 x (105 \- 5) = 25.315 |25.32 |
|13:00:00\-14:00:00 |Associated; 0 |0.063 x 1 x 5 + 0.25 x 1 x (105 \- 5) = 25.315 |25.32 |
|14:00:00\-15:00:00 |Associated; 0 |0.063 x 1 x 5 + 0.25 x 1 x (105 \- 5) = 25.315 |25.32 |
|15:00:00\-16:00:00 |Associated; 0 |(0.063 x 15/60 x 5 + 0.25 x 15/60 x (105 \- 5)) + (0.063 x 45/60 x 5 + 0.25 x 45/60 x (15 \- 5)) = 8.44 |8.44 |
|16:00:00\-17:00:00 |Associated; 0 |0.063 x 1 x 5 + 0.25 x 1 x (15 \- 5) = 2.815 |2.82 |
|\-\- |\-\- |Total |118.92 |


<span id=".5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5"></span>
## Pay\-by\-data\-transfer

<span id=".6LSt5Lmw5YmN5o-Q"></span>
### Prerequisites


* You have completed real\-name authentication for your account before applying for an EIP.


<span id=".6K6h6LS55YWs5byP"></span>
### Billing formulas

In Pay\-by\-data\-transfer, the usage duration for the IP config fee starts from the moment that the order is created, with precision down to the second.

**Fee for a Pay\-by\-data\-transfer EIP = IP config fee + Data transfer fee**. The formulas for IP config fee and Data transfer fee are as follows:


|Billing item |Formula |
|---|---|
|IP config fee |IP config fee = EIP instance unit price (USD/hour) × Usage duration (hour).<br><br><br>* If an account's EIP quota in a region is less than 1000 (inclusive), the account is exempt from IP config fees for EIP instances associated with cloud resources in that region. That is, the EIP instance unit price is 0.<br><br>* The default EIP quota for a single account in a single region is 20. If you need to increase the quota, go to the quota center to apply for an increase. |
|Data transfer fee |Data transfer fee = Data transfer unit price (USD/GB) × Data usage (GB). |


<span id=".57uT566X5ZGo5pyf"></span>
### Settlement cycle

Both the billing cycle and the settlement cycle are on an hourly basis.

On the hour (UTC+8), the platform settles fees, issues bills, and deducts payments.

<span id=".6LS555So56S65L6L"></span>
### Billing example

On January 1, 2022, at 10:30:00, Mr. B applies for a Pay\-by\-data\-transfer EIP in China (Beijing) with BGP (multi\-ISP), setting the maximum bandwidth to 200 Mbps.


* At 11:00:00, he associates this EIP with an ECS instance and enabled the service.

* At 17:00:00, service ends. The EIP was disassociated with the ECS instance and released.


Assume that the IP config fee per EIP is 0.02 USD/hour and the unit price of data transfer is 0.80 USD/GB. Fees for each billing cycle are as follows:


|Billing cycle |IP config fee (USD) |Data usage (GB) |Data transfer fee (USD) |Pay\-by\-data\-transfer (USD) |
|---|---|---|---|---|
|10:00:00\-11:00:00 |0.02 x (30/60) = 0.01 |0 |0 |0.01 |
|11:00:00\-12:00:00 |Associated; 0 |36 |0.80 x 36 = 28.80 |28.80 |
|12:00:00\-13:00:00 |Associated; 0 |72 |0.80 x 72 = 57.60 |57.60 |
|13:00:00\-14:00:00 |Associated; 0 |80 |0.80 x 80 = 64.00 |64.00 |
|14:00:00\-15:00:00 |Associated; 0 |40 |0.80 x 40 = 32.00 |32.00 |
|15:00:00\-16:00:00 |Associated; 0 |15 |0.80 x 15 = 12.00 |12.00 |
|16:00:00\-17:00:00 |Associated; 0 |14 |0.80 x 14 = 11.20 |11.20 |
|\-\- |\-\- |\-\- |Total |205.61 |


<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource price

You can view the EIP instance price on the [Pricing calculator](https://www.byteplus.com/en/pricing?product=EIP&tab=2) page. The amount presented by Pricing calculator is for reference only. Specific fees are subject to the amount on the actual order in [the Elastic IP console](https://console.byteplus.com/eip/eips).

<span id=".5YWx5Lqr5bim5a695YyF6K6h6LS56K-05piO"></span>
## Bandwidth Package billing notes

When the EIP is added to or removed from a Bandwidth Package, billing on the EIP side changes as follows:


|Billing item |Add to Bandwidth Package |Remove from Bandwidth Package |Related metering method |
|---|---|---|---|
|IP config fee |No impact |No impact |Pay\-by\-bandwidth, Pay\-by\-data\-transfer |
|Bandwidth fee |No charge |Charge |Pay\-by\-bandwidth |
|Data transfer fee |No charge |Charge |Pay\-by\-data\-transfer |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For the EIP applied via the Bandwidth Package console, <a href="https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5">Pay\-by\-data\-transfer</a> becomes effective after you remove the EIP from the Bandwidth Package instance.</div>


* <div data-tips="true" data-tips-type="tip">After you add the EIP to the Bandwidth Package instance, the original maximum bandwidth invalidates.</div>


* <div data-tips="true" data-tips-type="tip">After you remove the EIP from the Bandwidth Package instance, its previous billing method and maximum bandwidth become effective.</div>
