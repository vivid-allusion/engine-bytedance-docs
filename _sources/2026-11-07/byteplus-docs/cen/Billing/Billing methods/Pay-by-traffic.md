---
title: "Pay-by-traffic"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Pay-by-traffic"
---

The inter\-region bandwidth of Cloud Enterprise Network (CEN) supports pay\-by\-traffic billing and has been integrated with [Cloud Data Transfer (CDT)](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/What_is_Cloud_Data_Transfer). CDT is a unified metering and billing product for cloud network transmission services. It can combine billing for multiple network products, simplifying cost management and reducing network costs.

## Prerequisites

You have completed real\-name authentication for your account.

## Billing formula

Cross\-region traffic fee ** = ** Cross\-region traffic unit price × Outbound traffic from the region

* Cross\-region traffic unit price: See [Cross-region traffic billing resource prices](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/Cross-Region_Traffic_billing?l#Ljmjrlhg).

* Outbound traffic from the region: The sum of outbound traffic from both ends of the CEN. When using pay\-by\-traffic billing, traffic is converted in base 1024 (e.g., 1 TB = 1024 GB, 1 GB = 1024 MB).

## Settlement cycle

Billing Cycle & Settlement Cycle: Both are based on calendar hours.

Fees are settled every natural hour on the hour (based on UTC+8), a bill is issued, and the fee is deducted. For bill details, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

## Billing example

Account A created a CEN, loaded VPCs in two regions—China (Beijing) and China (Shanghai)—and set the billing method for inter\-region bandwidth to pay\-by\-traffic. Assume the cross\-region traffic unit price is 0.48 USD/GB. The traffic usage for the month is as follows:

|**Direction** |**Outbound traffic** |
|---|---|
|China (Beijing) → China (Shanghai) |100 GB |
|China (Shanghai) → China (Beijing) |50 GB |

The billing calculation is as follows:

* Outbound traffic from the region = 100 GB + 50 GB = 150 GB.

* Cross\-region traffic fee = 0.48 USD/GB × 150 GB = 72 USD.

Account A needs to pay a cross\-region traffic fee of 72 USD for the month.

###
