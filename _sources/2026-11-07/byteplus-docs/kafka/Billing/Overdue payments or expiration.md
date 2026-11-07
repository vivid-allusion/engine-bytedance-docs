---
title: "Overdue payments or expiration"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/overdue"
---

This topic describes the overdue payments rules of pay\-as\-you\-go Kafka instances.

<span id="欠费说明"></span>
## Overdue payments

If you have overdue payments, add funds to your BytePlus account and settle the bill at the earliest opportunity. Otherwise, you cannot use your Message Queue for Kafka resources. After the grace period expires, the corresponding resources are reclaimed and the relevant data cannot be recovered. You must pay the fees on the generated bill, regardless of whether your instance resources are frozen or released.

<span id="按量计费实例"></span>
### Pay\-as\-you\-go instances

For pay\-as\-you\-go instances, the system generates bills by hour and deducts the corresponding amount from your BytePlus account. Overdue payments are recorded if the available balance, including the cash balance and vouchers, in your BytePlus account is insufficient to cover the bill. In such a case, you will receive a text message or email that reminds you of insufficient balance.

The following table describes the resource status in each stage of overdue payments.


|**Overdue Period** |**Description** |**What to Do** |
|---|---|---|
|Within 2 hours after an overdue payment occurs |The instance can be used as expected. |Add funds to your BytePlus account. |
|Beyond 2 hours after an overdue payment occurs |The instance is unavailable and suspended. In this state, the instance is read\-only and not operable. |Add funds to your BytePlus account. After you settle the bill and the available balance in your BytePlus account becomes greater than 0, the instance status automatically restores to **Running**. |
|7 days after instance suspension |The instance is deleted forcibly. |You cannot recover the instance. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After your account has an overdue payment, an <strong>Arrears shutdown</strong> message appears in the <strong>Billing Method</strong> column of a pay\-as\-you\-go instance in the instance list. At this point, the instance only supports delete operations.</div>
