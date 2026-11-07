---
title: "Switching to yearly or monthly subscription"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/switching-to-yearly-or-monthly-subscription"
---

You can change the billing type of a SQL Server instance from volume billing to monthly billing at any time according to your business needs.

<span id="prerequisite"></span>
## prerequisite


* The [instance was created](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) and is **in the running** state.

* The billing type for the instance is [volume billing](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/pay-as-you-go).

* The instance has no outstanding subcontract annual monthly orders.


<span id="precautions"></span>
## Precautions

If an instance has a subcontracted annual monthly subscription that has not been paid for, and you upgrade the specification of the instance, the subcontracted annual monthly subscription will be invalid. You need to void it on the order page first, and then re\-contract the annual and monthly package.

<span id="single-instance-subcontract-annual-monthly-subscription"></span>
## Single instance subcontract annual monthly subscription


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the region to which the instance belongs.

3. In the left navigation bar, click **Instance List**.

4. On the **Instance List** page, click **Subcontract on Demand Year Month** in the Target Instance Action column.

5. On the **per\-volume billing subcontract annual subscription** page, set the following parameter information.

   
   |Parameters |Description |
   |---|---|
   |Purchase Duration |Select the purchase duration for the monthly subscription instance. |
   |Automatic Renewal |Whether to turn on the automatic renewal function. After checking **expiration automatic renewal**, the system will automatically renew the instance before it expires.<br><br>For more information on automatic renewal rules, see [Renewal Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules). |
   |Agreement |Read and tick the Terms of Service. |
   

6. Click **Confirm Order**.

7. On the **Confirm Order Information** Configuration Wizard page, confirm the order information and click **Next**.


<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">After the payment is complete, you can return to the instance list page to see if the billing type of the target instance was successfully converted to the annual subscription.</div>


<span id="batch-subcontracting-annual-monthly-subscription"></span>
## Batch subcontracting annual monthly subscription


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the region to which the instance belongs.

3. In the left navigation bar, click **Instance List**.

4. On the **instance list** page, check the target instance that needs to be subcontracted in batches, and click the **subcontracted year and month** in the lower left corner of the list.

5. On the **per\-volume billing subcontract annual subscription** page, set the following parameter information.



|Parameters |Description |
|---|---|
|Purchase Duration |Select the purchase duration for the monthly subscription instance. |
|Automatic Renewal |Whether to turn on the automatic renewal function. After checking **expiration automatic renewal**, the system will automatically renew the instance before it expires.<br><br>For more information on automatic renewal rules, see [Renewal Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules). |
|Agreement |Read and tick the Terms of Service. |



5. Click **Confirm Order**.

6. On the **Confirm Order Information** Configuration Wizard page, confirm the order information and click **Next**.


<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">After the payment is complete, you can return to the instance list page to see if the billing type of the target instance was successfully converted to the annual subscription.</div>
