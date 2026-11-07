---
title: "Overdue payments"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-overdue-payments"
---

This topic describes the impacts of overdue payments for Vital Container Instance (VCI) and how to view overdue payments.

<span id=".5qyg6LS55Y6f5Zug"></span>
## Reason for overdue payments

VCI instances are billed on an hourly basis, and the amounts are deducted in real time after a bill is generated. If the available balance in your account, including the cash balance and coupons, is less than the amount of bills to be settled, an overdue payment occurs in your account. In this case, an SMS or email notification is sent to remind you of an insufficient balance. To view the details of overdue payments, refer to [Bill details](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".5qyg6LS55YGc5pyN6K-05piO"></span>
## Overdue payment and service suspension policies

After an overdue payment occurs, your resources enter a grace period during which your resources are retained and can be used normally. After the grace period expires, your resources are forcibly reclaimed. Once reclaimed, they cannot be recovered. To ensure uninterrupted use of VCI resources, add funds to your account at the earliest opportunity and settle the outstanding bills within the specified time before the resources are forcibly reclaimed.

After the bills are settled, the instances that were suspended due to overdue payments automatically restart and enter the **Running** state.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When your account has an overdue payment, ensure that the available balance in your account, including the cash balance and coupons, is equal to or greater than USD 0 after the outstanding bills are settled. Otherwise, you cannot create any instances.</div>


You must settle the actually generated bills, regardless of whether your instance resources are frozen or released.

The following figure illustrates the impacts of an overdue payment in your account on the running and billing status of VCI instances.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7c2dc691df2d88250cf16ed0afa69c08.png) </span>

<span id=".5qyg6LS56YeK5pS-6K-05piO"></span>
## Resource release due to overdue payments


* Suspension time: 2 hours after an overdue payment occurs in your account

* Release time: 15 days and 2 hours (362 hours) after an overdue payment occurs in your account
