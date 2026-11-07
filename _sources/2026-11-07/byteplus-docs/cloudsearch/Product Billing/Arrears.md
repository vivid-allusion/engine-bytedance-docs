---
title: "Arrears"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/overdue"
---

If the available credit, including account balance and vouchers, in your account is less than the bill to be settled, your account will be considered in arrears, and you will receive an SMS or email notification of low balance. You can view the arrears details by referring to [Billing management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".5qyg6LS56K-05piO"></span>
## Overdue explanation

Volcengine regularly checks whether your account balance is sufficient to cover all orders and bills for products and services on the platform. If your account balance is insufficient or below zero, it is considered in arrears. When your account is in arrears, Volcengine will send arrears notifications to you through methods including but not limited to internal messages and emails.

After your account is in arrears, your resources will be retained and restricted. After the retention period expires, your resources will be forcibly reclaimed and cannot be restored. Please [recharge](https://docs.byteplus.com/en/docs/6269/100434) and settle the arrears before the deadline (before resource reclamation) to avoid disruption of Cloud Search services. After the bill is settled, the suspended Cloud Search service will automatically start and enter the **Running** status.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If your account is overdue, you must clear all outstanding bills and ensure your available credit (including account balance and vouchers) is at least RMB 100 to create Cloud Search services.</div>


* <div data-tips="true" data-tips-type="tip">Regardless of whether your resources are frozen or released, you should settle billed fees based on the actual amount.</div>



<span id=".5oyJ6YeP6K6h6LS55a6e5L6L"></span>
## **Pay\-as\-you\-go instances**

For pay\-as\-you\-go instances, the platform bills hourly and deducts in real time after billing. If your available credit, including account balance and vouchers, is less than the bill amount to settle, your account will be considered in arrears, and you will receive SMS or email notifications of about insufficient balance.

The following table describes the resource status at each stage after your account is in arrears.


|**Duration of arrears** |**Description** |
|---|---|
|2 hours after account becomes overdue |The **Billing type** becomes **In arrears**. The instance is in the **Suspended** state and cannot be used.<br><br>You need to top up your account in the [Billing center](https://console.byteplus.com/finance/account-overview/). Once you settle the overdue bills and the available credit is greater than 0, the instance status will become **Running**. |
|168 hours (that is, 7 days) after instance suspension |The instance is forcibly deleted. |


<span id=".5YyF5bm05YyF5pyI5a6e5L6L"></span>
## **Subscription instances**

Even if your account is in arrears, you can still use subscription instances you have purchased. However, before settling the overdue bills, you cannot create new instances or renew existing instances.

**Expiration**

Only subscription instances are affected by due status. Pay\-as\-you\-go instances have no usage time limit; you only need to ensure your account has sufficient balance.

The resource status at each stage after due date is shown in the table below:


|**Expiration time** |**Impact** |**Operation** |
|---|---|---|
|12 hours after instance expiration |The instance is suspended and unavailable. |[Renew](https://docs.byteplus.com/docs/cloudsearch/renewal) the instance. |
|7 days after expiration |The instance is forcibly deleted. |Cannot be restored. |
