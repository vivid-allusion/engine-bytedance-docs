---
title: "Arrears and expiration"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/arrears-and-expiration"
---

When a Document Database for MongoDB instance expires or the account is overdue, you must recharge or renew promptly to unlock the instance. This topic describes the impact of instance expiration or overdue payments.

<span id=".5qyg6LS56K-05piO"></span>
## Arrears

If the available balance in your account (including account balance and vouchers) is less than the bill to be settled, your account will be considered overdue. You will then receive an SMS or email reminding you to top up promptly to settle the overdue bill; otherwise, you will not be able to use Document Database for MongoDB resources normally.

When your account goes into arrears, this has a different impact on MongoDB instances with different billing methods.


<Tabs>
<Tab zoneid="gwRVuy8Iqg" title="Pay-as-you-go instances">
<TabTitle>Pay-as-you-go instances</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


* <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">Bills for Pay\-as\-you\-go instances are generated hourly, and payments are settled in real\-time after the bill is issued. Regardless of whether instance resources are frozen or released, you must settle the fees for bills that have been issued.</div>


* <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">After the account is in arrears, in the instance list, for pay\-as\-you\-go instances, <strong>Overdue</strong> is displayed under <strong>Billing method</strong>. At this time, instances only support delete operation.</div>




|Time in arrears |Impact |
|---|---|
|Within 360 hours (that is, 15 days) |The instance status remains **Running**, and the instance can be used normally. |
|Over 360 hours (that is, 15 days) |The instance status is **Closed**, and the instance is unavailable. You must go to the [Billing center](https://console.byteplus.com/finance/account-overview/) to recharge your account. When the outstanding bill is settled and the amount available in the account is above 0, the instance status will automatically revert to **Running**. |
|720 hours (that is, 30 days) after shutdown |The instance is forcibly deleted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When an instance is deleted, the system automatically initiates a backup to save all data before deletion. You can view backup details of deleted instances on the <strong>Backups of deleted instances</strong> page.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The retention period for backups of deleted instances is 7 days by default. If necessary, we recommend you promptly restore data to a new instance using backups of deleted instances. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/recovery_from_a_deleted_instance">Recovery from deleted instance</a>. Otherwise, after the instance is forcefully deleted and the retention period for backups of deleted instances expires, all nodes and all data will be permanently cleared and unrecoverable.</div><br> |





</Tab>
<Tab zoneid="WP7wfPPuL6" title="Yearly or monthly subscription instances">
<TabTitle>Yearly or monthly subscription instances</TabTitle>

You can still use your purchased subscription MongoDB instances normally even if your account is overdue. However, you cannot purchase new instances or perform renewals before paying outstanding fees.


</Tab>
</Tabs>


<span id=".5Yiw5pyf6K-05piO"></span>
## Expiration


<Tabs>
<Tab zoneid="t6siM3W7vb" title="Pay-as-you-go instances">
<TabTitle>Pay-as-you-go instances</TabTitle>

Only subscription instances will expire. There is no time limit for the pay\-as\-you\-go instances. You only need to ensure that your account has sufficient balance.


</Tab>
<Tab zoneid="dYQLXFXMDs" title="Yearly or monthly subscription instances">
<TabTitle>Yearly or monthly subscription instances</TabTitle>


|Expiration time |Impact |
|---|---|
|Expiration to 12:00 the next day |The instance status remains **Running**, and the instance can be used normally. |
|Within 720 hours (that is, 30 days) after expiration |The instance status is **Closed**, and the instance is unavailable. You need to renew the instance, and the status of the instance will automatically revert to **Running**. For instance renewal methods, refer to [Automatic or manual renewal](https://docs.byteplus.com/en/docs/mongodb/automatic-manual-renewal). |
|720 hours (that is, 30 days) after shutdown |The instance is forcibly deleted. <br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When an instance is deleted, the system automatically initiates a backup to save all data before deletion. You can view backup details of deleted instances on the <strong>Backups of deleted instances</strong> page.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The retention period for backups of deleted instances is 7 days by default. If necessary, we recommend you promptly restore data to a new instance using backups of deleted instances. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/recovery_from_a_deleted_instance">Recovery from deleted instance</a>. Otherwise, after the instance is forcefully deleted and the retention period for backups of deleted instances expires, all nodes and all data will be permanently cleared and unrecoverable.</div><br> |



</Tab>
</Tabs>


&nbsp;
