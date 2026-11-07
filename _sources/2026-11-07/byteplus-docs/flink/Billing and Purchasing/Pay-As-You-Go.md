---
title: "Pay-As-You-Go"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Pay-As-You-Go"
---

This article introduces the Pay\-As\-You\-Go billing details for BytePlus Flink, including billing methods and billing items.

<span id="d562c5d2"></span>
## Billing Method

BytePlus Flink currently supports **Pay\-As\-You\-Go**, which is a post\-payment model. Billing is based on the actual amount of resources used.


* Billing is done **per minute**, and any fraction of a minute is billed as one minute.

* The billing cycle is **one hour**. Use totals from the previous hour are calculated and settled, and the actual expense amount is deducted from your account balance. For example, if the billing time is at 9:02, the expenses calculated are for the time from 8:00 to 9:00.


<span id="2ffa9fb8"></span>
## Billing Items

The basic computing unit for BytePlus Flink is the Compute Unit (CU), where 1 CU equals 1 core CPU + 4 GiB of memory.

Real\-time usage is based on the bill.

<span id="9c60b2c8"></span>
## Billing Details


|**Selling Region** |**Billing Method** |**Billing Item (CU)**  |**Billing Duration (Hours)**  |**Unit Price (USD/CU/Hour)**  |
|---|---|---|---|---|
|China (Hong Kong) |Pay\-As\-You\-Go |Actual number of resources used |1 |0.11 |
|Asia Pacific (Johor) |Pay\-as\-you\-go |Actual number of resources used |1 |0.11 |


Assume you used 200 CUs of resources from 8:00 to 9:00. Your incurred cost would be: 200 CUs × 0.11 USD/CU/hour × 1 hour = 22 USD.

<span id="2b80f485"></span>
## Subscription Cancellation and Refunds

In a pay\-as\-you\-go scenario, deleting the resource pool instance signifies unsubscription and does not involve a refund.

You can delete the resource pool instance anytime when it's no longer needed. Simply click the **delete** button behind the resource pool and confirm again to unsubscribe from that resource pool instance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44efca407c4d4c07add6923d163ca776~tplv-goo7wpa0wc-image.image) </span>

<span id="9badcd8a"></span>
## Switch to annual or monthly package

Pay\-as\-you\-go is typically used in scenarios with elastic resource demand, unpredictable resource usage during testing phases, and similar situations. If the actual resource usage is already determined, you can convert the pay\-as\-you\-go resource pool to a subscription\-based resource pool via the console. If the subscription resource pool has sufficient resources, it will not cause any interruptions to tasks.

> Note: Before converting to a subscription resource pool, it is advised to confirm the actual resource usage and leave a margin for peak resource consumption. Avoid insufficient resources leading to task interruptions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3711cd1e366422fb621b3f9e4166d88~tplv-goo7wpa0wc-image.image) </span>

In the following interface, proceed to purchase resources based on actual resource usage to complete the conversion to subscription\-based.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df42f60771164bd08dfc501f6a1e53cf~tplv-goo7wpa0wc-image.image) </span>
