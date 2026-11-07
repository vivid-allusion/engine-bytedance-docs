---
title: "Arrears and expriation"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/arrears-and-expiration"
---

This topic introduces the instructions on arrears or expiration for pay\-as\-you\-go and subscription instances of RDS for SQL Server.

<span id="2CDUuGpf"></span>
## Overdue explanation


* **For pay\-as\-you\-go instances**, please recharge and settle the overdue bills within 7 days, otherwise you will not be able to use the resources of RDS for SQL Server. If the overdue retention period is exceeded, resources will be forcibly reclaimed, and related data will be irrecoverable. Regardless of whether your instance resources are frozen or released, you should settle the fees for the bills that have been issued based on actual usage.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For pay\-as\-you\-go instances, the platform generates hourly bills and processes real\-time payment upon issuance. If your available account balance (including account funds and vouchers) is insufficient to cover the pending bill, the system will record an overdue payment and trigger SMS/email alerts for insufficient balance.   </div>
   

   The status of resources at different stages after the due payment is as follows:

   
   |Time in arrears |Impact |How to operate |
   |---|---|---|
   |Within 360 hours |Overdue is displayed under Billing type. The instance status is Running, and the instance works normally. |[Renew](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/renewal-management) the instance. |
   |Between 360 and 720 hours |Overdue is displayed under Billing type. The instance status is Closed and it cannot be used.Billing is suspended for instances whose status is Closed. |You need go to the [Billing center](https://console.byteplus.com/finance/overview) to recharge your account. When the outstanding bill is settled and the amount available in the account is above 0, the instance status will automatically revert to Running. |
   |Over 720 hours |The instance is forcibly deleted and a final backup is created before deletion. The final backup is retained for 168 hours after it is created, after which the backup is deleted. |During the backup retention period, you can restore the full data backup to a new instance by [Rebuilding an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/rebuilding-instance). |
   

* **For subscription instances**, you can continue using your prepaid SQL Server instance even if your account has overdue payments. However, you cannot purchase new instances or renew until the overdue amount is paid.


<span id="WvA46LNc"></span>
## Expiration explanation

Only subscription instances are affected by expiry. Pay\-as\-you\-go instances do not have a usage duration limit, and you only need to ensure that there is a sufficient balance in the account. The resource status at each stage after expiration is shown in the following table:


|Expiration date |Impact |How to operate |
|---|---|---|
|Expiration to 12:00 the next day |Billing Type will show Expired. The instance status remains Running, and the instance can be used normally. |[Renew](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/renewal-management) the instance. |
|Expiration to 720 hours (30 days) |Billing Type will show Expired. The instance status is closed and it cannot be used. |You need to renew the instance, and the status of the instance will automatically revert to Running. For instance renewal methods, refer to [Automatic and manual renewal](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/renewal-management). |
|Over 720 hours |The instance is forcibly deleted and a final backup is created before deletion. The final backup is retained for 168 hours after it is created, after which the backup is deleted. |During the backup retention period, you can restore the full data backup to a new instance by [Rebuilding an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/rebuilding-instance). |
