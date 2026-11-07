---
title: "Pricing rules"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/pricing-rules"
---

This document describes the pricing rules for the ByteHouse Enterprise Edition.

<span id="计费项单价"></span>
## Unit price per billing item


|Billing Category |Resource Allocation ||Payment Method |Unit Price |
|---|---|---|---|---|
|(Required) Compute and Storage Resources |Generic (1:4) |4 Cores 16 GiB |Pre\-paid (annual and monthly subscriptions) |$280/month |
|||8 Cores 32 GiB ||$560/month |
|||16 Cores 64 GiB ||$1120/month |
|||32 Cores 128 GiB ||$2240/month |
|||64 Cores 256 GiB ||$4480/month |
||Performance (1:8) \- vCore |16 Cores 128 GiB ||$1520/month |
|||32 Cores 256 GiB ||$3040/month |
|||64 Cores 512 GiB ||$6080/month |
||Hot Storage \- GB<br><br><br>* Medium: EBS high\-performance cloud disk |||$0.214 GiB/month |
|(Optional) Storage Capacity |Cold storage \- GB<br><br><br>* Medium: TOS ||On\-demand |$0.001134/GB/hour ($0.034/GB/month) |
|(Optional) Advanced Features |GIS \- vCore ||Pre\-paid (annual and monthly subscriptions) |$0/vCore/month |
||Vector \- vCore |||$0/vCore/month |
||FullText Search \- vCore |||$0/vCore/month |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Local storage capacity starts at 100 GiB, with unlimited cold storage.</div>


* <div data-tips="true" data-tips-type="tip">Storage capacity is calculated in binary, for example, 1 GiB equals 1024 MiB.</div>



<span id="计费示例"></span>
## Billing Example

<span id="93d61c17"></span>
### Cluster Billing Example

ByteHouse cluster unit price = Number of nodes \* (Unit price of computing resources + Unit price of storage resources \* Storage capacity)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Billing is based on the number of nodes (Node Count), not the number of shards (Shard Count). Whether in single or dual copy mode, it does not affect the number of nodes.</div>


**Example:** 

An application for a 4\-node, 8\-core 32GB cluster with 1000 GB of storage, the cluster cost is:

`4 * (560 + 1000 * 0.214) = 3096 dollar/month`

<span id="3db72f35"></span>
### Cold Storage Billing Example

The billing type for cold storage is pay\-as\-you\-go, with daily settlements of the previous day's usage and generation of cost bills.

Calculation Method:

Cold storage cost = Cold data storage unit price × Usage × Duration.

The system retrieves usage values every hour (accurate to 0.01 GiB), and the total of all hourly charges for one day is the total daily cost.

Example:

For a user who subscribes to "Cold Storage", the daily cost settlement method:


|Update time |Dosage |Period cost calculation |Remark |
|---|---|---|---|
|19:00 |2.00 GiB |0.00028 dollar/GiB/hour \* 2 GiB \* 1 hour<br><br>= 0.00056 dollar |Cold storage starts at 18:30 |
|20:00 |20.00 GiB |0.00028 dollar/GiB/hour \* 20 GiB \* 1 hour<br><br>= 0.0056 dollar |Increase storage to 20 GiB |
|21:00 |200.00 GiB |0.00028 dollar/GiB/hour \* 200 GiB \* 1 hour<br><br>= 0.056 dollar |Increase storage to 200 GiB |
|22:00 |200.00 GiB |0.00028 dollar/GiB/hour \* 200 GiB \* 1 hour<br><br>= 0.056 dollar | |
|23:00 |50.00 GiB |0.00028 dollar/GiB/hour \* 50 GiB \* 1 hour<br><br>= 0.014 dollar |Freed 150 GiB of storage space |
|00:00 |100.00 GiB |= 0.028 dollar per GiB per hour \* 100 GiB \* 1 hour<br><br>= 0.028 dollar |Added 50 GiB of storage space |
|**Selected day cumulative charges** ||**0.16016** dollar | |


You can view the daily usage statistics in the "Dosage" column under [billing details](https://console.byteplus.com/finance/bill/detail).
