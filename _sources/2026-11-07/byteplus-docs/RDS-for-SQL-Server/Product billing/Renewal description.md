---
title: "Renewal description"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/renewal-management"
---

You can manually renew your subscription instances before it expires to avoid business disruptions.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and is in the **Running** state. For more information, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* The instance's billing type is [Subscription](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/yearly-or-monthly-subscription).


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**

Pay\-as\-you\-go instances do not expire and do not need to be renewed. Subscription instances have an expiration date. Failure to renew a subscription instance upon expiration will lead to business interruptions and even data loss.

<span id=".57ut6LS55pa55byP"></span>
## **Renewal methods**

RDS for SQL Server supports the following two renewal methods.


* **Automatic renewal**: You can enable automatic renewal function when creating a new subscription instance to avoid service disruptions due to expiration. Once enabled, the system automatically renews the instance before it expires. Ensure your account has a sufficient balance.

* **Manual renewal**: you can manually renew the instance at any time before it expires.


<span id="cSjtJTYe"></span>
## Automatic Renewal

BytePlus supports automatic renewal. After enabling it, the system will automatically deduct the renewal fee from your account balance 7 days before the due date. If you have available coupons in your account, the system will use them first for renewal.


1. Log in to the [Billing Center Console](https://console.byteplus.com/finance/account-overview/).

2. In the left navigation pane, click **Renewal Management**.

3. On the **Manual renewal** tab of the Renewal Management page, in the **Actions** column for the resource you want to renew, click **Enable auto\-renewal**.

4. On the **Auto\-renewal** page, select the duration for each automatic renewal and preset the number of renewals in the lower\-left corner, and then click the **Enable** button in the lower\-right corner.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not select <strong>preset auto\-renewal times</strong>, auto\-renewal will be permanently enabled. The System will perform an automatic renewal based on the single auto\-renewal duration before each resource expires. For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules">Renewal management</a>.   </div>
   

<span id=".5omL5Yqo57ut6LS5"></span>
## Manual renewal


1. Log in to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the region of the instance.

3. In the left navigation pane, click **Instances**.

4. There are two ways to perform manual renewal:

   * Method 1: On the Instances page, in the **Actions** column of the target instance, click  **...**  \> ** Renewal** button.

   * Method 2: Click the target instance name. In the **Billing information** section, click **Renewal** next to **Billing type**.

5. On the Renewal Management page, confirm the information for the instance you want to renew.

6. Select a renewal duration, and then click **Go to Pay**.

7. Confirm the amount, click **Next**, and then pay the fee.
