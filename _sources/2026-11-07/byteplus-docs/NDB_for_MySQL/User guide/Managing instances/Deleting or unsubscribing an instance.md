---
title: "Deleting or unsubscribing an instance"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_or_unsubscribing_an_instance"
---

You can delete a pay\-as\-you\-go instance or unsubscribe from a subscription instance based on your business needs. This article describes how to delete or unsubscribe from the NDB for MySQL instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The deletion protection function has been disabled. For more information, see [Disable instance deletion protection](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Instance_deletion_protection#.5YWz6Zet5a6e5L6L5Yig6Zmk5L-d5oqk).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This operation will delete all primary node and read\-only nodes under the instance and cannot be restored. Please operate with caution.

* When deleting an instance, you can choose whether to keep the full backup of the instance. If you keep the full backup, you can restore the instance based on the backup file in the **Backups of deleted instances**, or completely destroy the deleted instance backup. For more information, see [Backup and recovery overview](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Backup_and_recovery_overview).


<span id=".5Yig6Zmk5Zy65pmv"></span>
## Delete scene


|Delete scene |Backup retention policy |Actions |
|---|---|---|
|Deleting or unsubscribing an instance |* When you manually delete or unsubscribe from a normally running instance, the system automatically creates a final backup by default and keeps it in the **Backups of deleted instances** list.<br><br>* When you manually delete an instance that failed to create, no backup is retained. |You can restore an instance from a preserved backup file. For activity details, see [Managing backups of deleted instances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Backups_of_deleted_instances). |
|Arrears or due are automatically deleted |For more details, see [Arrears and expiration](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Arrears_and_expiration). ||


<span id=".5Yig6Zmk5oyJ6YeP6K6h6LS55a6e5L6L"></span>
## Delete the pay\-as\-you\-go instance


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select the target instance **Actions** column for  **...**   **\> Delete instance**.

4. Confirm the instance information in the dialog box that pops up, and the **Backup strategy** defaults to **Create and retain a final backup**.

5. Click **Delete**.


<span id=".6YCA6K6i5YyF5bm05YyF5pyI5a6e5L6L"></span>
## Unsubscribe from yearly/monthly subscription


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select the target instance **Actions** column for  **...**   **\> Unsubscribe instance**.

4. In the pop\-up dialog box, enter the target **instance name** for secondary confirmation, and then click **OK** to jump to the billing platform.

   You can also directly select the upper right corner **Billing \> Unsubscription management**, enter the billing platform, and unsubscribe. For specific steps, see [Unsubscribe management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

5. On the **Unsubscription** page, confirm information concerning the instance that you want to unsubscribe and amount information, and click **Confirm unsubscription**.

   After confirming the cancellation, the **Unsubscription details** dialog box will pop up automatically. You can view the relevant information of the unsubscribed instance (such as instance ID/name and refund amount) in the pop\-up window. You can also click the order number (starting with **Order**) to go to the order details page.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">By clicking <strong>Confirm unsubscription</strong>, you will immediately apply for unsubscription (the instance status will change to <strong>Deleting</strong>), and you will not be prompted to confirm again. Please proceed with caution.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBInstance) |Call the DeleteDBInstance to delete a pay\-as\-you\-go instance. |
