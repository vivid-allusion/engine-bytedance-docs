---
title: "Snapshot billing"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Snapshot_billing"
---

The snapshot feature of the BytePlus Elastic Block Storage product will begin charging in phases by region starting from 00:00 on July 14, 2025. This document describes the billing method, price, and billing examples for snapshots.

<span id="precautions"></span>
## Precautions

Snapshots only support pay\-as\-you\-go billing, which charges based on capacity and duration. To stop billing, delete all snapshots and unbind the volume and auto\-snapshot policies.

<span id="billing-method"></span>
## Billing method

For details on snapshot pricing, see [Pricing details](https://www.byteplus.com/en/pricing?product=volume&tab=1).


|**Billing method** |**Description** |**Billing unit** |**Related documents** |
|---|---|---|---|
|Pay\-as\-you\-go |A postpaid model where you use services first and pay later, charged by the hour. The billing formula is as follows:<br><br>Snapshot fee = Snapshot unit price × Snapshot capacity × Billing duration |USD/GiB/hour |[Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) |


<span id="billing-examples"></span>
## Billing Examples

Suppose you have 500GiB of snapshots in Asia Pacific (Johor) for a duration of 20 days. The snapshot fee is as follows:

Snapshot fee = 0.000023611 × 24 × 20 × 500 = 5.66664 USD
