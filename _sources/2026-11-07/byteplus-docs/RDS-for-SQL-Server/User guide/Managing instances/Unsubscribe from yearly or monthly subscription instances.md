---
title: "Unsubscribe from yearly or monthly subscription instances"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/unsubscribing-subscription-instance"
---

This topic describes how to unsubscribe from a subscription SQL Server instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Subscription instances do not support a 7\-day unconditional unsubscription. For details about the refund rules, see [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

A subscription instance has been created and is in the **Running** state.

<span id=".6K6h6LS56K-05piO"></span>
## Billing information

After successfully unsubscribing from a subscription primary instance or any read\-only instances, the refund will be credited to your account balance. For details about the refund calculation rules, see [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After unsubscribing from an instance, its bound private network address is automatically released and can not be recovered. The Elastic Public IP (EIP) is also automatically disassociated, but it is retained and continues to incur charges. If you no longer need the EIP, release the resource to avoid fees.

* If a primary instance includes read\-only instances, unsubscribing from the primary instance also unsubscribes from the read\-only instances.

* Deleted read\-only instances are immediately cleared. Backup and restore are not supported. If you need to read data, create a new read\-only instance. For detailed steps to create a read\-only instance, see [Creating read-only instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-read-only-instance).


<span id=".5pON5L2c5q2l6aqk"></span>
## **Unsubscribe from a single instance**


1. Log in to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click  **...**  \> **Unsubscribe** in the **Actions** column of the target instance.

4. In the **Warning** dialog, click **OK** to go to the **Unsubscribe** page for the target instance.

5. On the **Unsubscribe** page, click the **Submit order** button.

6. In the **Confirm unsubscribing from the following resources?**  dialog box, confirm the unsubscribe information, and then click **OK** to unsubscribe from the instance.


<span id="ECVwW1Hl"></span>
## Batch unsubscribe from instances


1. Log in to the [Billing center console](https://console.byteplus.com/finance/unsubscribe).

   2. In the left\-side navigation pane, click **Unsubscription management** to go to the **Unsubscription management** page.

   3. Click the **7\-day no reason**, **Regular unsubscription**, or **Unsubscription not supported** tab to view the unsubscription status of the instances in your account.

   4. On the target tab, select multiple instances, and then click **Batch Unsubscription** at the bottom of the page.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can search for the target instances by Instance ID or Instance name.   </div>
