---
title: "Billing overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/billing-overview"
---

This article mainly introduces the billing methods, billing items, and billing rules of ByteHouse (Cloud Data Warehouse Edition).

<span id="3d2d8c37"></span>
## Cost composition

The current ByteHouse Cloud Data Warehouse product costs consist of **calculate** and **storage** two parts.


* **Cluster computing power**: The calculation group can be purchased in two ways: **pay\-as\-you\-go** (postpaid) and **annual and monthly subscription** (prepaid).

* **Storage capacity**: All are **pay\-as\-you\-go** (postpaid).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Pay\-as\-you\-go</strong>, also known as postpaid. This billing method supports users paying after usage, determining charges by multiplying actual consumption by the unit price per hour. Users can settle the charges after the daily bill is issued.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Annual and monthly packages</strong>, also known as prepaid. It is a prepaid billing method that can significantly save costs at the time of payment, suitable for scenarios where business traffic is relatively stable and used long\-term.</div>



<span id="4c625552"></span>
## Billing Method


|Billing items |Description of billing items |Billing method ||
|---|---|---|---|
|Cluster computing power |The computing resources allocated to the group are used to perform actions like searches. |Pay\-as\-you\-go (postpaid) |Postpaid costs are calculated based on actual hourly push usage, and there is no need to purchase resources in advance. Compute unit cost = unit price of different compute units × duration used, and cluster compute power cost = total of all compute unit costs under the account. |
|||Annual and monthly subscription (prepayment) |Prepayment costs are accumulated by multiplying the purchase duration by the number of units by the monthly unit price of the compute unit. |
|Storage capacity |Used to measure data imported into the ByteHouse service and provide high\-performance querying, with a minimum storage resource requirement of 100GiB. |Pay\-as\-you\-go (postpaid) |Costs are based on actual hourly push volumes, averaged daily for storage.<br><br>Storage costs = storage unit price × storage space × duration used. |


For detailed cost calculation, please refer to [Specifications and pricing](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing).
