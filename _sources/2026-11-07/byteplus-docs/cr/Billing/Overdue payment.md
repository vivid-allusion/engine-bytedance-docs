---
title: "Overdue payment"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/overdue-payment"
---

This topic introduces the impacts of overdue payments on BytePlus Container Registry (CR), as well as how to view overdue payments.

<span id="欠费原因"></span>
## Causes of overdue payments

CR is billed hourly, and the amount in a bill is deducted in real time. If the sum of the balance and coupons in your account is less than the payable amount of your bill, your account has an overdue payment.

<span id="欠费停服说明"></span>
## Impacts of overdue payments

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If you have an overdue payment, your service may be suspended and your resources may be released. <a href="https://console.byteplus.com/finance/renew">Renew your service</a> in a timely manner to avoid potential impacts. For more information on renewal, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-subscription-renewal">Managing Subscription Renewal</a></div>


<div data-tips="true" data-tips-type="danger">.</div>


When you have an overdue payment, the service status of CR changes as follows:


|Overdue Payment Duration |Description |
|---|---|
|＜ 360h |Product features are fully functional, with charges incurred during usage billed as usual. For more information on billing, refer to [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2). |
|≥ 360h |BytePlus sends notifications through SMS and email to remind you of the overdue payment and freezes your resources (which means you can no longer operate the Enterprise Standard Edition instances). Resources are not charged when they are frozen. |
|360h ＜ duration ≤ 1080h |If you have paid the overdue payment under your account, BytePlus automatically unfreezes your resources to enable you to continue to use the product. |
|＞ 1080h |BytePlus sends notifications through SMS and email and releases your resources by deleting the Enterprise Standard Edition instances. Resources cannot be recovered after they are released. |


<span id="查看欠费"></span>
## Viewing overdue payments


1. Log in to [Billing Center](https://console.byteplus.com/finance/overview/).

2. On the **Overview** page, view the overdue amount.
