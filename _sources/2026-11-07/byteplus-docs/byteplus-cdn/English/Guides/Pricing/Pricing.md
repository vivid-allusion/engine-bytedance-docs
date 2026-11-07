---
title: "Pricing"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-pricing"
---

<span id="billing-overview"></span>
# Billing Overview

BytePlus CDN provides flexible pricing with both pay\-as\-you\-go and prepaid savings plan options. This document explains all billable items, such as data transfer and requests, and provides detailed pricing tables for both models. You can use this information to understand your charges and select the most cost\-effective plan for your needs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For high\-traffic or enterprise customers, we offer customized pricing. Please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to learn more about customized pricing.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_451932a0ffac47b5393ddfe1492d8053.png) </span>

<span id="billing-items"></span>
## Billing Items

CDN has the following billing items:


* The number of requests received by the CDN. This refers to the HTTP and HTTPS requests sent by clients (such as browsers) to access your site files.

* The data transferred from CDN to clients.

* The data transferred from CDN to the origin server.

* Log delivery volume (Log Batch Delivery)

* Log delivery volume (Log Streaming)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, CDN does not charge for the number of WebSocket requests. However, during the WebSocket handshake phase, the HTTP request received by the CDN is still billed as an HTTP request.</div>


<span id="billing-method"></span>
## Billing Method

CDN uses a pay\-as\-you\-go billing model, which means you are billed based on actual usage. After you activate the CDN service, you can start using it without any upfront payment.

Additionally, we provide prepaid savings plans. Savings plans can be used to offset charges for data transfer and requests, helping you reduce costs.

<span id="billing-cycle"></span>
## Billing Cycle

By default, CDN is billed on an hourly basis.

<span id="overdue-payments"></span>
## Overdue Payments

As described above, BytePlus CDN uses pay\-as\-you\-go (postpaid) billing settled on an hourly basis, and bills are issued hourly at the end of each billing cycle. If you require monthly settlement, please contact our sales or pre\-sales support team.

In the following situations, your current bill may fail to be charged, resulting in an overdue balance:


* You removed the payment method linked to your account (for example, a credit card) before the bill was issued.

* Your account balance is insufficient to cover the current bill.


For accounts with individual (personal) verification, once a payment becomes overdue, CDN immediately suspends and takes the associated services offline, with no separate notification sent. If your payment is overdue, please settle the outstanding amount promptly; your services are automatically brought back online once the payment is cleared. To avoid being suspended again due to overdue payments and to ensure business continuity, make sure the payment method linked to your account remains valid, or that your account balance is sufficient, so that subsequent bills can be charged normally.

<span id="billing-details-pay-as-you-go"></span>
# Billing Details (Pay\-as\-you\-go)


|**Billing Item** |**Billing Type** |**Price** |
|---|---|---|
|Data transferred from CDN to the client |Billed by traffic |Prices vary based on different billing regions and monthly usage tiers. Please refer to the [table below](https://docs.byteplus.com/en/docs/18/6537#pricing-for-data-transferred-from-cdn-to-the-client-settled-hourly) for details. |
|Data transferred from CDN to the origin server |Billed by traffic |0.06 USD/GB. |
|Number of requests received by CDN |Billed by requests |0.012 USD/10,000 requests. |
|Log delivery volume (Log Batch Delivery) |Billed by log entries |0.001 USD/10,000 entries |
|Log delivery volume (Log Streaming) |Billed by log entries |0.0015 USD/10,000 entries |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For traffic, 1 GB = 1,000 MB.</div>


<span id="pricing-for-data-transferred-from-cdn-to-the-client-settled-hourly"></span>
## Pricing for Data Transferred from CDN to the Client (Settled hourly)

The data transferred from CDN to clients is aggregated and billed based on the region of the CDN node. Data transfer pricing varies by region. Prices in the table below are in **USD/GB**.


|**Traffic Tier** |**Chinese Mainland** |**Europe** |**North America** |**Middle East/Africa** |**South America** |**Asia Pacific Region 1** |**Asia Pacific Region 2** |**Asia Pacific Region 3** |
|---|---|---|---|---|---|---|---|---|
|First 10 TB / Month |0.035 |0.044 |0.044 |0.100 |0.100 |0.060 |0.078 |0.088 |
|Next 40 TB / Month |0.033 |0.036 |0.036 |0.095 |0.095 |0.052 |0.065 |0.075 |
|Next 50 TB / Month |0.028 |0.028 |0.028 |0.085 |0.085 |0.046 |0.060 |0.065 |
|Next 900 TB / Month |0.025 |0.022 |0.022 |0.080 |0.080 |0.042 |0.050 |0.058 |
|Over 1 PB / Month |0.024 |0.019 |0.019 |0.075 |0.075 |0.040 |0.045 |0.054 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Asia\-Pacific Region 1: Includes Singapore, Japan, Thailand, Malaysia, Hong Kong, Macau.</div>


* <div data-tips="true" data-tips-type="tip">Asia\-Pacific Region 2: Includes Philippines, Indonesia, Vietnam, Taiwan.</div>


* <div data-tips="true" data-tips-type="tip">Asia\-Pacific Region 3: Includes South Korea and other countries and regions in the Asia Pacific.</div>



<span id="billing-example"></span>
## Billing Example

From `2023-09-01 00:00:00` to `2023-09-01 01:00:00`, the data transferred within the Chinese Mainland billing region was 9,960 GB, and within the Europe billing region was 3,960 GB. Therefore, the cumulated data transfer in both billing regions falls within the 0~10TB tier for the month. The bill for this time period is calculated as follows:

> 9960 \* 0.035 + 3960 \* 0.044 = 522.84 USD.


Then, from `2023-09-01 01:00:00` to `2023-09-01 02:00:00`, the data transferred within the Chinese Mainland billing region was 100 GB, and within the Europe billing region was 1,000 GB. Therefore:


* The cumulative data transfer for the Chinese Mainland region now enters the 10\-40 TB tier. Of the 100 GB transferred in this period, the first 40 GB is billed at the 0\-10 TB tier rate, and the remaining 60 GB is billed at the 10\-40 TB tier rate.

* The cumulated data transfer in the billing region of Europe still falls within the 0~10TB tier for the month.


The bill for this time period is calculated as follows:

> 40 \* 0.035 + 60 \* 0.033 + 1000 \* 0.044 = 47.38 USD.


<span id="traffic-and-requests-savings-plans-prepaid"></span>
# Traffic and Requests Savings Plans (Prepaid)

CDN provides savings plans for traffic and requests. If you can estimate your monthly data transfer and request volume, we recommend purchasing a savings plan to save costs. The savings plan is valid for 30 days.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For traffic savings plans, 1 GB = 1,000 MB.</div>


<span id="how-savings-plans-work"></span>
## How Savings Plans Work


* During settlement, the CDN prioritizes using available savings plans. If you have multiple available plans, the one with the earliest expiration date is used first.

* If your savings plan capacity is insufficient to cover your usage, any overage is billed at the pay\-as\-you\-go rate.

* A savings plan becomes invalid in the following situations:

   * The savings plan has expired.

   * The quota of the savings plan has been exhausted.


Unused capacity from expired savings plans cannot be transferred to other plans or refunded.

<span id="pricing-of-savings-plans"></span>
## Pricing of Savings Plans

<span id="promotions"></span>
### Promotions

**Free Trial**

Each BytePlus primary account is entitled to one traffic savings plan and one request savings plan for free. The validity period is 30 days.


* The capacity of the traffic savings plan is 1 TB.

* The capacity of the request savings plan is 10,000,000 requests.


<span id="pricing-of-traffic-savings-plan"></span>
### Pricing of Traffic Savings Plan

The prices in the following list are standard rates. The actual price is subject to what is shown on the [purchase page](https://console.byteplus.com/common-buy/CDN%7C%7C7403252517272424710).

The unit of price in the table below is **USD**.


|**Capacity** |**Chinese Mainland** |**Outside Chinese Mainland** |
|---|---|---|
|100 GB |3 |6 |
|500 GB |15 |30 |
|1 TB |30 |60 |
|5 TB |150 |300 |
|10 TB |300 |600 |
|50 TB |1,500 |3,000 |
|100 TB |3,000 |6,000 |
|500 TB |15,000 |30,000 |
|1 PB |30,000 |60,000 |
|5 PB |150,000 |300,000 |
|10 PB |300,000 |600,000 |


<span id="pricing-of-request-savings-plan"></span>
### Pricing of Request Savings Plan

The unit of price in the table below is **USD**.


|**Capacity** |**Chinese Mainland** |**Outside Chinese Mainland** |
|---|---|---|
|1,000,000 requests |1.2 |1.2 |
|10,000,000 requests |12 |12 |
|100,000,000 requests |120 |120 |
|1,000,000,000 requests |1,200 |1,200 |
|10,000,000,000 requests |12,000 |12,000 |
|100,000,000,000 requests |120,000 |120,000 |
