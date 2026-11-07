---
title: "Specifications and pricing"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/specifications-and-pricing"
---

This document primarily introduces the pricing and specifications of ByteHouse Cloud Data Warehouse Edition.

<span id="be354a8b"></span>
## Billing items

<span id="cadb49e9"></span>
### Computational resources

The virtual warehouse includes various configurations; detailed billing items are as follows:


| |Pricing unit |||Post\-paid<br><br>($0.14/core/h) |Pre\-paid (Annual and monthly package prices)<br><br>($70 core/month) |
|---|---|---|---|---|---|
|(Required) Basic Service |Type |Model |Configuration |||
||Generic |XS |4 cores 16 GiB, 200 GiB cache |0.56 |280 |
|||S |8 cores 32 GiB, 200 GiB cache |1.12 |560 |
|||M |16 cores 64 GiB, 200 GiB cache |2.24 |1120 |
|||L |32 cores 128 GiB, 200 GiB cache |4.48 |2240 |
|||XL |64 cores 256 GiB, 200 GiB cache |8.96 |4480 |
|||Customized size (N\*XL) |N\*XL |N\*8.96 |N\*4480 |
||Performance |XL PLUS |64 cores 512 GiB, 1000 GiB cache |12.006 |6000 |
|||Customized size (N\*XL) |N\*XL+ |N\*12.006 |N\*6000 |
||Storage |GiB, starting from 100 GiB. ||Post\-paid, $0.034/GiB/Month ||
|(Optional)<br><br>Private server |8 cores and 32 GiB, starting from 2 nodes |||$1.12/node/hour |$560/node/month |
||16 cores and 64 GiB, starting from 2 nodes |||$2.24/node/hour |$1120/node/month |
||32 cores and 128 GiB, starting from 2 nodes |||$4.48/node/hour |$2240/node/month |
||64 cores and 256 GiB, starting from 2 nodes |||$8.96/node/hour |$4480/node/month |
|(Optional)<br><br>Virtual warehouse local disk |Starting from 100 GiB, with a step size of 100 GiB (The minimum specifications and step sizes vary for different virtual warehouses). |||$0.0005 GiB/hour |$0.214/GiB/month |
|(Optinal)<br><br>Distributed cache |Starting from 10500 GiB, with a step size of 3500 GiB. |||Not supported |$0.214/GiB/month |
|(Optional)<br><br>Advanced Features |GIS\- vCore |||(Discount) $0/vCore/hour |(Discount)<br><br>$0/vCore/month |
||Vector \- vCore |||(Discount) $0/vCore/hour |(Discount)<br><br>$0/vCore/month |
||FullText Search \- vCore |||(Discount) $0/vCore/hour |(Discount)<br><br>$0/vCore/month |


<span id="计费示例"></span>
## Billing example

<span id="按量计费"></span>
### Post\-paid solution for virtual warehouses

**Example 1:**  A service uses one S model compute resource and one L model compute resource, analyzing 3 TiB of data. The S model compute resource is used effectively for 12 hours per day, and the L model compute resource is used effectively for 6.5 hours per day. The costs are calculated based on 30 days per month.


* Daily computing cost = (1 × 1.12 × 12) + (1 × 4.48 × 6.5) = 42.56 (dollar)

* Monthly storage cost = 3 × 1024 × 0.034 (dollar)= 104.448 (dollar)


Total monthly cost = 42.56 × 30 + 104.448 = 1381.248 (dollar)

**Example Two:**  A company's data department purchases 10 M model computing resources and analyzes 5 TiB of data. Each M model computing resource has an effective usage time of 8 hours per day. Cost calculation is based on a 30\-day month.


* Daily computing cost = 10 × 2.24 (dollar) × 8 (hours) = 179.2 (dollar)

* Monthly storage cost = 5 × 1024 × 0.034 (dollar) = 174.08 (dollar)


Total monthly cost = 179.2 × 30 + 174.08 = 5550.08 (dollar)

<span id="包年包月"></span>
### Pre\-paid package for virtual warehouses

**Example 3:**  A business applies for an M model virtual warehouse for monthly usage with 1000 GiB of storage, and the cost is calculated based on 30 days per month. The calculation shows:

Total monthly cost: 1120 + (0.034 × 1000) = 1154 (dollar)
