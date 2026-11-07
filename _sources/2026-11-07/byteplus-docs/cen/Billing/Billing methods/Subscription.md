---
title: "Subscription"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Subscription"
---

Subscription is a billing method applicable to scenarios with long\-term use and relatively stable bandwidth requirements. This billing method can significantly reduce your expenses.

## Prerequisites

You have completed real\-name authentication for your account.

## Billing formula

|Bandwidth |Billing formula |
|---|---|
| 0 Mbps＜bandwidth ≤100 Mbps |Cost of a single bandwidth package = Unit Price (USD/Mbps/month) for 0\-100 Mbps × Bandwidth (Mbps) × Purchase Duration (months) |
|100Mbps＜bandwidth ≤1000Mbps |Cost of a single bandwidth package = [Unit Price (USD/Mbps/month) for 0\-100 Mbps × 100 + Unit Price (USD/Mbps/month) for 100\-1000 Mbps × (Bandwidth \- 100)] × Purchase Duration (months) |
|bandwidth＞1000Mbps |Cost of a single bandwidth package = [Unit Price (USD/Mbps/month) for 0\-100 Mbps × 100 + Unit Price (USD/Mbps/month) for 100\-1000 Mbps × 900 + Unit Price (USD/Mbps/month) for \>1000 Mbps × (Bandwidth \- 1000)] × Purchase Duration (months) |

## Resource pricing

You can view the unit price of bandwidth on the [Price calculator](https://www.byteplus.com/en/pricing?product=CEN&tab=2). Please note that this price is for reference only, and the final cost will be displayed in the [Bandwidth package console](https://console.byteplus.com/cen/cenBandwidthPackage).

## Billing cycle

The CEN Subscription bandwidth package can be purchased on a yearly or monthly basis. The billing cycle corresponds to the purchase duration (based on UTC+8 time).

For example: If a Subscription bandwidth package is created on January 1, 2022, at 15:13:23 with a purchase duration of 3 months, its expiration time will be April 1, 2022, at 23:59:59.
