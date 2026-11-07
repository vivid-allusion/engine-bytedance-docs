---
title: "Overdue payments"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Overdue_payments"
---

This topic describes the impacts of overdue payments for Function Service (FaaS) and how to view overdue payments.

<span id="overdue-payments"></span>
## Overdue payments

BytePlus will check periodically if your account balance is sufficient to pay for the orders/bills of all products/services on the platform. If the available balance in your account, including the cash balance and coupons, is less than the amount of bills to be settled, an overdue payment occurs in your account. In this case, an SMS or email notification is sent to remind you of an insufficient balance. To view the details of overdue payments, refer to [Bill details](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

After an overdue payment occurs, your resources enter a grace period during which your resources are retained and can be used normally. After the grace period expires, your resources are forcibly reclaimed. Once reclaimed, they cannot be recovered.

To ensure uninterrupted use of Function Service resources, add funds to your account at the earliest opportunity and settle the outstanding bills within the specified time before the resources are forcibly reclaimed. After the bills are settled, the function resources that were suspended due to overdue payments automatically restart.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You must settle the actually generated bills, regardless of whether your function resources are frozen or released.</div>


<span id="overdue-payment-and-service-suspension-policies"></span>
## Overdue payment and service suspension policies

Status of resources at each stage after arrears as shown in the table below:


|**Arrear duration** |**Description** |
|---|---|
|Arrear duration ≤ 2 hours |You can normally use the function services, which will issue bills according to your actual usage. |
|Arrear duration ≤ 15 days |The platform will send you related notifications and **suspend the service**. When the function service is suspended, the following impacts occur:<br><br><br>* Only viewing and deleting functions are supported, creating and modifying functions is not supported.<br><br>* Existing functions will no longer process new requests, but functions that are currently running will continue to execute until completion.<br><br>* Scheduled triggers are paused from triggering in the new cycle.<br><br>* The collection of Monitoring Data for the function is paused.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to go to the <a href="https://console.byteplus.com/finance/overview">Billing Center</a> promptly to recharge your account. Once the arrear bill is cleared and the available credit is greater than 0, the function will automatically resume usage.</div><br> |
|Arrear duration 30 days |The platform will send you a related notification and reclaim the resources (delete the functions). **Once resources are reclaimed, they cannot be restored**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to promptly visit the <a href="https://console.byteplus.com/finance/overview">Billing Center</a> to top up your account. Only when the account is refilled to a non\-arrear state can you recreate functions.</div><br> |
