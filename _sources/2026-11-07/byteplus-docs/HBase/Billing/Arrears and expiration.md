---
title: "Arrears and expiration"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Arrears_and_expiration"
---

This topic describes what happens to post paid HBase instances when the account is in arrears. 

<span id="MzbW9KRO"></span>
## Pay\-as\-you\-go instances

Recharge your account and settle overdue bills within 3 days, or else you cannot use HBase resources. After the arrears retention period, resources are forcibly reclaimed and related data cannot be recovered. Regardless of whether your instance resources are frozen or released, you should settle the fees that have been billed.

<span id="5GXDO5lm"></span>
### Arrears

The platform issues bills on an hourly basis for instances in the pay\-as\-you\-go billing method, and settlement and deduction are conducted in real time after the bills are issued. If the available balance (including account balance and cash coupons) in your account is less than the amount specified in the bill to be settled, your account is deemed to be in arrears and you will receive an SMS or email reminder about the insufficient balance.

The following table shows the resource statuses at each stage when your account is in arrears:


|**Time in arrears** |**Impact** |
|---|---|
|Within 360 hours (that is, 15 days) |**Overdue** is displayed under **Billing method**. The instance status is **Running**, and the instance works normally. |
|Over 360 hours (that is, 15 days) |**Overdue** is displayed under **Billing method**. The instance status is **Closed** and it cannot be used. You must go to the [Billing center](https://console.byteplus.com/finance/overview) to recharge your account. When the outstanding bill is settled and the amount available in the account is above USD 0.00, the instance status will automatically revert to **Running**.<br><br>The EIP bound to the instance is automatically released after the account has been in arrears for 2 hours. Recharging the account does not restore the EIP. You need to enable public access to the instance again to bind the EIP.  |
|720 hours (that is, 30 days) after shutdown |The instance is forcibly deleted and a final backup is created before deletion. The final backup is retained for 168 hours after it is created, after which the backup is deleted. |


<span id="IqLyNpor"></span>
## Yearly/monthly subscription instances

<span id="SVxTU7Tx"></span>
## Expiration

Only yearly/monthly subscription instances are affected by expiration. There is no limit on the usage duration for pay\-as\-you\-go instances, and you only need to ensure that your account has sufficient balance.

The following table shows the resource status at each stage after expiration:


|Expiration time |Impact |
|---|---|
|Expiration to 12:00 the next day |**Expired** is displayed under **Billing method**, but the instance status is still **Running**. The instance can be used normally. |
|Within 720 hours (that is, 30 days) after expiration |**Expired** is displayed under **Billing method**. The instance status is **Closed** and it cannot be used. You need to renew the instance, and the status of the instance will automatically revert to **Running**. For instance renewal methods, refer to [Renewal management](https://docs.byteplus.com/en/docs/HBase/Renewal_management). |
|720 hours (that is, 30 days) after shutdown |The instance will be forcibly deleted. By default, no data backup will be retained during deletion, and the instance will be unable to be restored. |
