---
title: "Description of arrears or expiration"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Description_of_arrears_or_expiration"
---

This section introduces overdue payment for instances of message queue for RabbitMQ, including both pay\-as\-you\-go and subscription instances.

<span id=".5qyg6LS56K-05piO"></span>
## Description of arrears

BytePlus periodically checks if your account balance on the platform is sufficient to cover all your product/service orders and bill payments. If the balance is insufficient or becomes negative, it is considered arrears. When your account becomes overdue, BytePlus will send you notices through various means including, but not limited to, on\-site messages and emails.

Once overdue, please recharge and settle the overdue bills promptly. Otherwise, you will not be able to use resources of message queue for RabbitMQ. Beyond the preservation period for arrears, resources will be compulsorily reclaimed and related data will be unrecoverable. Regardless of whether your instance resources are frozen or released, you should settle the issued bills as per actual.

<span id=".5oyJ6YeP6K6h6LS55a6e5L6L"></span>
### Pay\-as\-you\-go instance

For pay\-as\-you\-go instance, the platform issues hourly bills and settles payments in real\-time upon billing. If the credits in your account (including balance and vouchers) are less than the outstanding balance, it will be considered overdue. You will receive notifications about insufficient balance via SMS or email.

Resource status at various stages after arrears is as follows:


|**Overdue duration** |**Description** |**How to operateHow to operate** |
|---|---|---|
|Within 2 hours of instance overdue |The instance is usable. |Recharge the account. |
|Two hours after the instance is overdue |The instance is unavailable and shut down. In shutdown status, the instance is read\-only and can not be operated on. |Recharge your account till the overdue bills are settled and the account's available credit is greater than 0. Then the instance status will automatically resume to **Running**. |
|Instance shuts down after 7 days |The instance is forcibly deleted. |Unable to retrieve. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Two hours after the account is in arrears, in the instance list, pay\-as\-you\-go instances under <strong>Billing method</strong> will show the phrase <strong>Service suspended due to arrears</strong>. At this point, the instance only supports the operation of Delete.</div>


<span id=".5YyF5bm05YyF5pyI5a6e5L6L"></span>
### Subscription instances

Even if your account is in arrears, you can still use the purchased annual and monthly instances as normal. However, until the arrears are paid off, you can not purchase new instances or renewal existing ones.

<span id=".5Yiw5pyf6K-05piO"></span>
## Expiration description

Only annual and monthly instances are affected by expiration. Pay\-as\-you\-go instances have no usage duration limit. You just need to ensure a sufficient balance in your account.

Resource status at various stages after expiration is as follows:


|**Due time** |**Status** |**How to operate** |
|---|---|---|
|Until 12:00 PM on the 2nd day after expiration |**Billing method** will display **Expired**, but the instance status remains **Running**. The instance can be used normally. |[Renewal](https://docs.byteplus.com/en/docs/rabbitmq/Instance_renewal) the instance. |
|Within 7 days after expiration |**Billing method ** will show **Expired**, the instance status will be **Stopped**, and the instance will be unavailable. |You need to [Renewal](https://docs.byteplus.com/en/docs/rabbitmq/Instance_renewal) your instance. After renewal, the instance status will automatically return to **Running**. |
|Shut down after 7 days |The instance will be forcibly deleted. |Unable to retrieve. |
