---
title: "Arrears and expiration"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/arrears_and_expiration"
---

This topic describes what happens to post paid and yearly/monthly subscription RDS for PostgreSQL instances when the account is in arrears or instances expire.

<span id=".5oyJ6YeP6K6h6LS5"></span>
## Pay\-as\-you\-go

Recharge and settle the arrears within 3 days, or you will lose access to the RDS for PostgreSQL resources. After the arrears retention period, resources will be forcibly reclaimed and data cannot be restored. Regardless of whether your instance resources are frozen or released, you are responsible for settling the billed fees.

<span id=".5qyg6LS56K-05piO"></span>
### Arrears description

If the available balance (including account balance and cash coupons) in your account is less than the amount specified in the bill to be settled, your account is deemed to be in arrears and you will receive an SMS or email reminder about the insufficient balance.

The resource states after arrears at each stage are shown in the table below:


|Overdue duration |Note |how to continue using the instances |
|---|---|---|
|Instance overdue for 2 hours |The instance can read and write normally. |The instance can be used normally. It is recommended to [recharge](https://console.byteplus.com/finance/renew/) the account to avoid service impact after overdue exceeds 2 hours. |
|Instance overdue for more than 2 hours |The instance is not available and shut down; in the shut down state, the instance is read\-only and non\-operable. |At this time, you need to recharge your account. Once the overdue bills are settled and the available credit is above zero, the instance state will automatically recover to **running**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The EIP bound to the instance will be automatically released 2 hours after the account becomes overdue. Recharging the account will not restore the binding; you need to re\-enable public network access and bind the EIP again for the instance. For more details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access">Enable public network access</a>.</div><br> |
|7 days after the instance is shut down |The instance was forcibly deleted. A final backup will be created for the instance during deletion and retained for 7 days. |During the retention period of the final backup, recharging the account and settling the overdue bill can restore the instance. You can choose to restore as a pay\-as\-you\-go instance or a subscription instance according to your needs at this time:<br><br><br>* To restore to a pay\-as\-you\-go instance, after recharging and settling the bill, the total account balance (i.e., cash balance) and vouchers must exceed 100.00 USD.<br><br>* To restore to a subscription instance, after recharging and settling the bill, the account balance should exceed the cost of the target subscription period. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the account is in arrears, pay\-as\-you\-go instances in the Instances list will show the <strong>billing method</strong> as <strong>overdue shut down</strong>. The instance supports only the delete operation at this time.</div>


<span id=".5YyF5bm05YyF5pyI"></span>
## Subscription

<span id=".5Yiw5pyf6K-05piO"></span>
### Expiration instruction

Only Subscription instances are affected by expiration; pay\-as\-you\-go instances have no usage time limit, and you only need to ensure your account has sufficient balance.

The resource status at each expiration stage is shown in the following table:


|Expiration time |Impact |how to continue using the instances |
|---|---|---|
|Expired until 12:00 on Day 2 |**Billing method** will show **expired**, but the instance **state** remains Running, and the instance can be used normally. |The instance can be used normally. |
|Within 7 days after expiration |**Billing method** will show **expired**, the instance state will be **shut down**, and the instance will not be available. |[Renewal](https://docs.byteplus.com/en/docs/RDS_for_PG/renewal_management) operation for the instance will automatically restore the instance state to **Running** after completion.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The EIP bound to the instance will be automatically released after the account is overdue for 2 hours. Recharging the account will not restore the binding; you need to re\-enable public network access and associate the EIP to the instance again. For more details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access">Enabling public network access</a>.</div><br> |
|Shut down for 7 days |The instance will be forcibly deleted. A final backup will be created when deleting the instance, and the final backup will be retained for 7 days. |During the final backup retention period, you can restore the instance after recharging the account and settling overdue bills. At this time, you can choose to restore as a pay\-as\-you\-go instance or a subscription instance as needed:<br><br><br>* To restore to a pay\-as\-you\-go instance, after recharging and settling the bill, the total account balance (i.e., cash balance) and vouchers must exceed 100.00 USD.<br><br>* To restore to a subscription instance, after recharging and settling the bill, the account balance should exceed the cost of the target subscription period. |
