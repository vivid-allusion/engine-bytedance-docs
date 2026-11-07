---
title: "Annual and Monthly Subscription"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Annual_and_Monthly_Subscription"
---

This document introduces the annual and monthly billing instructions for BytePlus Flink, including billing methods, purchase duration, billing cycle, and billing items.

<span id="580fb3d3"></span>
## Billing methods

Users create Flink resource pools based on general resources, supporting the creation of resource pools with **annual and monthly** billing methods. The annual and monthly billing method requires prepayment, which offers more favorable prices compared to pay\-as\-you\-go billing.

<span id="af3f8849"></span>
## Purchase duration

When creating an annual and monthly resource pool, the system offers a variety of purchase durations. You can choose the appropriate purchase duration based on the length of service usage.


* **Monthly purchase**: You can choose to purchase for 1 to 11 months.

* **Annual purchase**: You can choose to purchase for 1 to 3 years.


<span id="d727eae6"></span>
## Billing Cycle

The billing cycle for the annual and monthly resource pool is the duration of your purchase (based on UTC+8 time). A billing cycle starts from the creation time of the resource (precise to the second) and ends at 23:59:59 on the expiration date.

For example, if an annual and monthly resource pool is created on August 4, 2023, at 14:00:00, and the purchase duration is for 1 month, the billing cycle would be: August 4, 2023, 14:00:00 to September 4, 2023, 23:59:59.

<span id="5a5a5d0a"></span>
## Billing Items

The basic unit of computational resources for BytePlus Flink is the Compute Unit (CU), where 1 CU = 1 core CPU + 4 GiB memory.

Details of the billing items for the annual and monthly resource pool are as follows:


|**Sales Region** |**Billing Method** |**Billing Items** |**Billing Duration** |**Unit Price (USD/CU/Month)**  |
|---|---|---|---|---|
|China (Hong Kong) |Annual and Monthly Subscription |CU |Actual Purchase Duration |50 |
|Asia Pacific (Johor) |Annual and Monthly Subscription |CU |Actual Purchase Duration |50 |


Billing example: Assuming a purchase duration of 1 month for a 32 CU single availability zone resource pool, the prepayment required would be: 32 CU × 50 USD/CU/month × 1 month = 1600 USD.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This example is for reference only; please refer to the console display for changes in prices and discounts.</div>


<span id="1bf240c8"></span>
## Subscription Cancellation and Refunds

In annual and monthly scenarios, deleting the resource pool signifies cancellation, and the refund amount will be credited back to your account balance.

You can delete the resource pool anytime when it's no longer needed. Simply click the **delete** button behind the resource pool and confirm again to unsubscribe.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44efca407c4d4c07add6923d163ca776~tplv-goo7wpa0wc-image.image) </span>

Refund amount = Amount paid for the order \- Monthly unit price at time of purchase × [Number of days used ÷ (365 ÷ 12)] × Applicable discount

<span id="b52e36f0"></span>
## Expiration Description

You need to pay attention to the billing cycle of the annual and monthly billing method resource pool. If the resource pool expires without renewal, the system will reclaim the resource pool and automatically evict tasks.


* You can choose to enable **automatic renewal** for the resource pool. After enabling automatic renewal, the system will automatically renew the resource pool 7 days before expiration based on the purchase duration.

* You can also choose to manually renew the resource pool before it expires.


For renewal operations, please see [Resource Pool Renewal](https://docs.byteplus.com/docs/flink/Resource_Pool_Renewal).
