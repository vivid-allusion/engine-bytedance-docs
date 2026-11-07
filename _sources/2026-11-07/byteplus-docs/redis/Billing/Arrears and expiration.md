---
title: "Arrears and expiration"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/arrear-and-expiration"
---

When a Cache for Redis instance expires or the account is overdue, you must recharge or renew promptly to unlock the instance. This topic describes the impact of instance expiration or overdue payments.

<span id=".5qyg6LS56K-05piO"></span>
## Arrears

If the available balance in your account (including account balance and vouchers) is less than the bill to be settled, your account will be considered overdue. You will then receive an SMS or email reminding you to top up promptly to settle the overdue bill; otherwise, you will not be able to use Cache for Redis resources normally.

When your account goes into arrears, this has a different impact on Redis instances with different billing methods.


<Tabs>
<Tab zoneid="tSlpzC2jxC" title="Pay-as-you-go instances">
<TabTitle>Pay-as-you-go instances</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Bills for Pay\-as\-you\-go instances are generated hourly, and payments are settled in real\-time after the bill is issued. Regardless of whether instance resources are frozen or released, you must settle the fees for bills that have been issued.</div>


* <div data-tips="true" data-tips-type="tip">After a Redis instance enters the Closed state due to overdue payments or expiration, its associated public IP address (EIP) will not be automatically disassociated by the system. Instead, it will be retained and follow the EIP's own lifecycle. The instance's public IP address will only be deleted when the EIP is released or manually disassociated by you. During this period, you can calmly complete renewal or temporary business recovery. The public IP address is typically retained for more than 24 hours.</div>




|Time in arrears |Impact |
|---|---|
|Within 360 hours (that is, 15 days) |**Overdue** is displayed under **Billing method**. The instance status is **Running**, and the instance works normally. |
|Over 360 hours (that is, 15 days) |**Overdue** is displayed under **Billing method**. The instance status is **Closed** and it cannot be used. You must go to the [Billing center](https://console.byteplus.com/finance/account-overview/) to recharge your account. When the outstanding bill is settled and the amount available in the account is above 0, the instance status will automatically revert to **Running**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Billing is suspended for instances whose status is <strong>Closed</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If instance uses additional bandwidth, when the instance enters the <strong>Closed</strong> status, <strong>the additional bandwidth will be automatically released immediately</strong>. If you need to continue using additional bandwidth, you need to wait for the account recharge to be completed and the instance to be restored to <strong>Running</strong> before adding additional bandwidth again. For more details about additional bandwidth, refer to <a href="https://docs.byteplus.com/en/docs/redis/modify-bandwidth">Modifying bandwidth</a>.</div><br> |
|720 hours (that is, 30 days) after shutdown |The instance is forcibly deleted. The system automatically selects the corresponding default backup policy based on the instance type, where:<br><br><br>* Primary\-secondary instance: A final backup will be created by default before deleting the instance, and it will be retained for 7 days after successful creation. It is recommended to download and save it locally promptly. You can view or download backups of deleted instances on the **Backups** page and restore instances based on the backups. For more details, refer to [Restoring deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance).<br><br>* Single node instance: Single node instances do not support persistence and backup functions. No backup will be created by default when deleting, and instance data will be **completely cleared** after deletion. Please proceed with caution. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If an instance is closed due to an overdue account, it will be forcefully deleted even if deletion protection is enabled. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/deletion-protection">Instance deletion protection</a>.</div><br> |





</Tab>
<Tab zoneid="YftFxcbby1" title="Yearly or monthly subscription instances">
<TabTitle>Yearly or monthly subscription instances</TabTitle>

You can still use your purchased subscription Redis instances normally even if your account is overdue. However, you cannot purchase new instances or perform renewals before paying outstanding fees.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If your subscription instance uses additional bandwidth and your account becomes overdue, the <strong>additional bandwidth used by the instance will be immediately and automatically released</strong>, even if the subscription instance is <strong>Running</strong>. If you need to continue using additional bandwidth, you must wait for your account to be recharged, then add additional bandwidth to the instance again. For more details about additional bandwidth, refer to <a href="https://docs.byteplus.com/en/docs/redis/modify-bandwidth">Modifying bandwidth</a>.</div>


* <div data-tips="true" data-tips-type="tip">After a Redis instance enters the Closed state due to overdue payments or expiration, its associated public IP address (EIP) will not be automatically disassociated by the system. Instead, it will be retained and follow the EIP's own lifecycle. The instance's public IP address will only be deleted when the EIP is released or manually disassociated by you. During this period, you can calmly complete renewal or temporary business recovery. The public IP address is typically retained for more than 24 hours.</div>



</Tab>
</Tabs>


<span id="bhAMBfdp"></span>
## Expiration


<Tabs>
<Tab zoneid="LcLrz8MdWg" title="Pay-as-you-go instances">
<TabTitle>Pay-as-you-go instances</TabTitle>

Only subscription instances will expire. There is no time limit for the pay\-as\-you\-go instances. You only need to ensure that your account has sufficient balance.


</Tab>
<Tab zoneid="aG3lvUQtak" title="Yearly or monthly subscription instances">
<TabTitle>Yearly or monthly subscription instances</TabTitle>


|Expiration time |Impact |
|---|---|
|Expiration to 12:00 the next day<br><br> |**Expired** is displayed under **Billing method**, but the instance status is still **Running**. The instance can be used normally. |
|Within 720 hours (that is, 30 days) after expiration |**Overdue** is displayed under **Billing method**. The instance status is **Closed** and it cannot be used. You need to renew the instance, and the status of the instance will automatically revert to **Running**. For specific procedures of instance renewal methods, refer to [Automatic and manual renewal](https://docs.byteplus.com/en/docs/redis/automatic-manual-renewal).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Billing is suspended for instances whose status is <strong>Closed</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If instance uses additional bandwidth, when the instance enters the <strong>Closed</strong> status, <strong>the additional bandwidth will be retained but not billed</strong>. After you complete the renewal operation for instance and the instance is restored to <strong>Running</strong>, the additional bandwidth will also automatically become available again and billing will resume. For more details about additional bandwidth, refer to <a href="https://docs.byteplus.com/en/docs/redis/modify-bandwidth">Modifying bandwidth</a>.</div><br> |
|720 hours (that is, 30 days) after shutdown |The instance is forcibly deleted. The system automatically selects the corresponding default backup policy based on the instance type, where:<br><br><br>* Primary\-secondary instance: A final backup will be created by default before deleting the instance, and it will be retained for 7 days after successful creation. It is recommended to download and save it locally promptly. You can view or download backups of deleted instances on the **Backups** page and restore instances based on the backups. For more details, refer to [Restoring deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance).<br><br>* Single node instance: Single node instances do not support persistence and backup functions. No backup will be created by default when deleting, and instance data will be **completely cleared** after deletion. Please proceed with caution. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When an instance is out of service due to its expiration, the instance is deleted even if deletion protection is enabled. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/deletion-protection">Instance deletion protection</a>.</div><br> |





</Tab>
</Tabs>
