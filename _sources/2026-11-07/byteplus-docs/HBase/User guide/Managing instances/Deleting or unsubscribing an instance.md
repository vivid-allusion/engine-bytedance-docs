---
title: "Deleting or unsubscribing an instance"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Deleting_or_unsubscribing_an_instance"
---

Table Storage for HBase supports manual instance deletion. This article describes how to delete an HBase instance from the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance must be in the **Running** state. For more information about instance states, see the [Instance status description](https://docs.byteplus.com/en/docs/HBase/Instance_status_description).

* The deletion protection function has been disabled. For more information, see [Disable instance deletion protection](https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection#.5YWz6Zet5a6e5L6L5Yig6Zmk5L-d5oqk).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After deleting or unsubscribing an instance, all data will be completely deleted and cannot be restored. Please operate with caution.

* After canceling your subscription for a yearly or monthly HBase instance, the refund amount will be returned to your account balance. For details on refund calculation rules, please see [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).


<span id=".5Yig6Zmk5oyJ6YeP6K6h6LS55a6e5L6L"></span>
## Delete the pay\-as\-you\-go instance


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select the target instance **Actions** column for  **...**  \> **Delete instance**.

4. In the dialog box that pops up, confirm the instance information to be deleted (such as instance ID and name), and click **Delete**.


<span id=".6YCA6K6i5YyF5bm05YyF5pyI5a6e5L6L"></span>
## Unsubscribe from yearly/monthly subscription

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For instance with yearly/monthly subscription billing types, even if instance <a href="https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection#.5byA5ZCv5a6e5L6L5Yig6Zmk5L-d5oqk">deletion protection is enabled</a>, you can still cancel your subscription through the <a href="https://console.byteplus.com/finance/unsubscribe/">billing platform</a>.</div>



1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select the target instance **Actions** column for  **...**  \> **Unsubscribe instance**.

4. In the pop\-up dialog box, enter the target instance name for secondary confirmation, and then click **OK** to jump to the billing platform.

   You can also directly select the upper right corner **Billing** \> **Unsubscription management**, enter the billing platform, and unsubscribe. For specific steps, see [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

5. On the **Unsubscription** page, confirm information concerning the instance that you want to unsubscribe and amount information, and click **Confirm unsubscription**.

   After confirming the cancellation, the **Unsubscription details** dialog box will pop up automatically. You can view the relevant information of the unsubscribed instance (such as instance ID/name and refund amount) in the pop\-up window. You can also click the order number (starting with **Order**) to go to the order details page.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">By clicking <strong>Confirm unsubscription</strong>, you will immediately apply for unsubscription (the instance status will change to <strong>Deleting</strong>), and you will not be prompted to confirm again. Please proceed with caution.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/HBase/DeleteDBInstance) |Call the DeleteDBInstance interface to delete a pay\-as\-you\-go instance. |
