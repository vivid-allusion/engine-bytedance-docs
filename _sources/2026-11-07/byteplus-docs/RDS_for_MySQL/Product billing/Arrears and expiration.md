---
title: "Arrears and expiration"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/arrears_and_expiration"
---

This topic describes what happens to post paid and yearly/monthly subscription RDS for MySQL instances when the account is in arrears or instances expire. 

<span id="pay-as-you-go"></span>
## Pay\-as\-you\-go instances

Recharge your account and settle overdue bills within 3 days, or else you cannot use RDS for MySQL resources. After the arrears retention period, resources are forcibly reclaimed and related data cannot be recovered. Regardless of whether your instance resources are frozen or released, you should settle the fees that have been billed.

<span id="arrears"></span>
### Arrears

The platform issues bills on an hourly basis for instances in the pay\-as\-you\-go billing method, and settlement and deduction are conducted in real time after the bills are issued. If the available balance (including account balance and cash coupons) in your account is less than the amount specified in the bill to be settled, your account is deemed to be in arrears and you will receive an SMS or email reminder about the insufficient balance.

The following table shows the resource statuses at each stage when your account is in arrears:


|**Time in arrears** |**Impact** |
|---|---|
|Within 360 hours |**Overdue** is displayed under **Billing method**. The instance status is **Running**, and the instance works normally. |
|Over 360 hours |**Overdue** is displayed under **Billing method**. The instance status is **Closed** and it cannot be used. You must go to the [Billing center](https://console.byteplus.com/finance/overview) to recharge your account. When the outstanding bill is settled and the amount available in the account is above USD 0.00, the instance status will automatically revert to **Running**.<br><br>The EIP bound to the instance is automatically released after the account has been in arrears for 2 hours. Recharging the account does not restore the EIP. You need to enable public access to the instance again to bind the EIP. For more information, refer to [Enabling internet access](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access). |
|Over 720 hours |The instance is forcibly deleted and a final backup is created before deletion. The final backup is retained for 168 hours after it is created, after which the backup is deleted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set the <strong>Backup retention policy after instance release</strong> policy to <strong>Do not retain backups</strong>, no backup will be created for the instance.</div><br> |


<span id="yearly-monthly-subscription-instances"></span>
## Yearly/monthly subscription instances

<span id="expiration"></span>
## Expiration

Only yearly/monthly subscription instances are affected by expiration. There is no limit on the usage duration for pay\-as\-you\-go instances, and you only need to ensure that your account has sufficient balance.

The following table shows the resource status at each stage after expiration:


|**Expiration Time** |**Impact** |**What to Do** |
|---|---|---|
|Expiration to 12:00 the next day |**Expired** is displayed under **Billing method**, but the instance status is still **Running**. The instance can be used normally. |[Renew](https://docs.byteplus.com/en/docs/RDS_for_MySQL/renewal_management) the instances. |
|Over 720 hours after shutdown |The instance is forcibly deleted. The system automatically selects the corresponding default backup policy based on the instance type.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set the <strong>Backup retention policy after instance release</strong> policy to <strong>Do not retain backups</strong>, no backup will be created for the instance.</div><br> |\- |
