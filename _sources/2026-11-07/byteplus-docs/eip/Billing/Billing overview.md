---
title: "Billing overview"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Billing-overview"
---

Elastic IP Addresses (EIPs) support Subscription and Pay\-as\-you\-go. Each metering method suits different scenarios, with varying payment times and billing items. Choose based on your needs.

<span id=".6K6h6LS557G75Z6L5a-55q-U"></span>
## Billing overview


|Billing method |Advantages |Metering method |Recommended scenarios |Maximum bandwidth (Mbps) |Billing item |Payment time |Settlement cycle |
|---|---|---|---|---|---|---|---|
|Pay\-as\-you\-go |You can enable and release resources as needed at any time without purchasing a large amount of resources in advance. |[Pay-by-data-transfer](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5) |After specifying the bandwidth cap, charges are based on actual Internet **outbound** traffic, regardless of usage duration. Applicable for scenarios with significant short\-term business growth, such as flash sales. |1\-200 |Traffic fee |Postpaid |Fees are settled hourly on each natural hour (UTC+8). |
||||||IP config fee |||
|||[Pay-by-bandwidth](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.6K6h6LS55YWs5byP) |Once the maximum bandwidth is specified, fees are charged based on usage time, regardless of actual traffic. This applies to businesses with temporary resource use and stable bandwidth. |1\-1000 |Bandwidth fee |||
||||||IP config fee |||
|Subscription |Compared with Pay\-as\-you\-go, it is more cost\-effective. |[Subscription](https://docs.byteplus.com/en/docs/eip/Subscription#.6LS555So6K-05piO) |Applicable for long\-term stable business. |1\-1000 |Bandwidth fee |Prepaid |Non\-calendar month |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can convert the <a href="https://docs.byteplus.com/en/docs/eip/Billing-methods-change">metering method</a> anytime according to your business needs. The change takes effect immediately.</div>


* <div data-tips="true" data-tips-type="default">You can increase bandwidth by adding an EIP to a <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/Billing-overview">Bandwidth Package</a>, optimizing resource allocation and reducing costs.</div>



<span id="DrjbgecW"></span>
## Select a billing method


* Select a billing method based on your network usage. We recommend using Pay\-as\-you\-go for EIPs when network usage is below 10%, and Subscription when usage exceeds 10%.

* When selecting bandwidth, we recommend setting EIP's maximum bandwidth 10% to 20% higher than your stable business bandwidth.


<span id="WZpjTL0g"></span>
### Example 1

Mr. A's server traffic is stable at around 8 Mbps daily. He needs to apply for an EIP in China (Beijing) with a one\-month usage duration.

Rate: 8 Mbps = 1 MB/s, so the total monthly traffic = 1 (MB/s) × 30 (days) × 24 (h) × 3600 (seconds/h) = 2,592,000 MB = 2,531.25 GB


|Metering method |Recommended maximum |Fee calculation |
|---|---|---|
|Pay\-by\-data\-transfer |10 Mbps |EIP fee = IP config fee + Traffic fee = [0.02 (USD/hour) × 720 (hours)] + [0.80 (USD/GB) × 2531.25 (GB)] = **2,039.4 USD** |
|Subscription ||EIP fee = [Unit price of bandwidth within 1\-2 Mbps (USD/month per Mbps) × 2 (Mbps) + Unit price of bandwidth within 3\-5 Mbps (USD/month per Mbps) × 3 (Mbps) + Unit price of bandwidth over 5 Mbps (USD/month per Mbps) × (Maximum bandwidth \- 5) (Mbps)] × Usage duration (months) = [23 (USD/month per Mbps) × 2 (Mbps) + 25 (USD/month per Mbps) × 3 (Mbps) + 100 (USD/month per Mbps) × 5 (Mbps)] = **621.00 USD** |


The comparison shows: choosing a **Subscription** EIP is more cost\-effective.

<span id="cX7Z3St8"></span>
### Example 2

Mr. B's server occasionally generates traffic, with bandwidth reaching a peak of 8 Mbps for only 10% of the day (2.4 hours); no internet traffic occurs the rest of the time. He needs to apply for an EIP in the Beijing region with a one\-month usage period.

Rate: 8 Mbps = 1 MB/s. The total monthly traffic usage = 1 (MB/s) × 30 (days) × 2.4 (hours) × 3600 (seconds/hour) = 259,200 MB = 253.13 GB


|Metering method |Recommended maximum |Fee calculation |
|---|---|---|
|Pay\-by\-data\-transfer |10 Mbps |EIP fee = IP config fee + Traffic fee = [0.02 (USD/hour) × 720 (hours)] + [0.80 (USD/GB) × 253.13 (GB)] = **216.90 USD** |
|Subscription ||EIP fee = [Unit price of bandwidth within 1\-2 Mbps (USD/month per Mbps) × 2 (Mbps) + Unit price of bandwidth within 3\-5 Mbps (USD/month per Mbps) × 3 (Mbps) + Unit price of bandwidth over 5 Mbps (USD/month per Mbps) × (Maximum bandwidth \- 5) (Mbps)] × Usage duration (months) = [23 (USD/month per Mbps) × 2 (Mbps) + 25 (USD/month per Mbps) × 3 (Mbps) + 100 (USD/month per Mbps) × 5 (Mbps)] = **621.00 USD** |


It is clear that choosing **Pay\-by\-data\-transfer** for the EIP is more cost\-effective.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When the traffic volume is high, we recommend selecting <strong>Pay\-by\-bandwidth</strong>. You can quickly estimate EIP costs through the <a href="https://www.byteplus.com/en/pricing?product=EIP&tab=2">Pricing calculator</a>.</div>


&nbsp;

<span id="iUzG6K9O"></span>
##
