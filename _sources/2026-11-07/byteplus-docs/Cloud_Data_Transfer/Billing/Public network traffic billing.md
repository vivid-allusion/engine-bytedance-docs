---
title: "Public network traffic billing"
product: "Cloud Data Transfer"
product_code: "Cloud_Data_Transfer"
source: "https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/Public_Network_Traffic_billing"
---

After Cloud Data Transfer (CDT) is enabled, all existing and new **pay\-by\-data\-transfer** cloud service instances are automatically billed by CDT. Certain line types are eligible for a free traffic quota. Billing starts for a cloud service only after its free quota is exhausted. If CDT is not enabled, see the respective cloud product's billing documentation for billing rules.

## Prerequisites

* You have completed real\-name authentication for your account.

* Your account's available balance is not less than USD 0.

## Billing rules

The billing rules for CDT public network traffic are shown in the table below. The BGP (multi\-line) line supports tiered billing. The usage within each tier is multiplied by the unit price of that tier, and the results are summed to obtain the total price. The unit price varies by tier.

|Cloud product |**Line type** |Tiered billing |Free quota |
|---|---|---|---|
|* Elastic IP Address<br><br>* Bandwidth Package |BGP (multi\-line) |Yes |Yes |

> **tip**

* > BGP (multi\-line) free quota: CDT provides a monthly free quota of 220 GB​ for public network traffic (20 GB/month for China Mainland, 200 GB/month for regions outside China Mainland).

* > When CDT billing is enabled for both Elastic IP Address (EIP) and Bandwidth Package, their traffic can be combined for tiered cumulative billing​.

* > For other line types, see the console for billing rules and resource prices.​

## Resource pricing

BGP (multi\-line) public network traffic supports tiered billing. The traffic tiers are listed in the table below. For the exact fee, see the actual order placed in the console.

|**Traffic tier** |<br>**Traffic price (**USD/GB**)**<br> ||
|---|---|---|
||**China Mainland** |Asia Pacific |
|**0 < Usage ≤ 10 TB** |0.118 |0.100 |
|**10 < Usage ≤ 50 TB** |0.111 |0.070 |
|**50 < Usage ≤ 150 TB** |0.103 |0.065 |
|**150 TB < Usage** |0.096 |0.055 |

## Settlement cycle

* Both the billing cycle and settlement cycle are based on calendar hours.

* Fees are settled at the top of every calendar hour (UTC+8). A bill is generated and fees are deducted accordingly.​ For bill details, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

## Billing example

On March 1, 2026 at 00:00:00, Mr. A applies for a Pay\-by\-data\-transfer EIP in China Mainland. The EIP is located in China (Beijing) and configured with BGP (multi\-line). Mr. A associates this EIP with an Elastic Compute Service (ECS) instance and put into service.

* March 5, 2026: public network traffic of the ECS reaches 36 GB. Mr. A enables CDT billing for the EIP.

* March 10, 2026: Total public network traffic of the ECS reaches 10 TB.

* March 25, 2026: Total public network traffic of the ECS reaches 50 TB.

* March 31, 2026: Total public network traffic of the ECS reaches 55 TB.

CDT provides a monthly free quota of 20 GB/month for public network traffic. Assume the unit price of the EIP traffic is 0.118 USD/GB before CDT is enabled. The traffic fee is calculated as follows: Traffic fee calculation is detailed as follows:

|Billing cycle |Traffic tier |Traffic usage (GB) |Traffic unit price (USD/GB) |Traffic fee (USD) |
|---|---|---|---|---|
|**Before CDT** |||||
|March 1 \- March 5 |\- |36 |0.118 |4.248 |
|**After CDT** |||||
|March 5 \- March 10 |0 < Usage ≤ 10 TB |20 |0 |0.000 |
|||10220 |0.118 |1,206.960 |
|March 10 \- March 25 |10 < Usage ≤ 50 TB |40960 |0.111 |4,546.560 |
|March 25 – March 31 |50 < Usage ≤ 150 TB |5120 |0.103 |527.360 |
|**Traffic fee =​ Cost before CDT + Sum of costs in each tier after CDT = 4.248 + ( 1,206.960 + 4,546.560 + 527.360 ) = 6,285.128 USD** |||||
