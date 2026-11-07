---
title: "Delete or unsubscribe an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_or_unsubscribing_an_instance"
---

You can manually release pay\-as\-you\-go instances or unsubscribe from subscription instances based on your business requirements. This topic describes how to delete or unsubscribe a MySQL instance.

## Prerequisites

* The instance has been created and is in the **Running** or **Stopped** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* (Optional) Deletion protection for the instance is **Disabled**. To disable it, refer to [Set deletion protection for an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Setting_instance_deletion_protection).

   > **tip**

   > You can also disable deletion protection during the deletion or unsubscription process.

## Precautions

* When you delete or unsubscribe from an instance, a final **Full backup** is created and stored in **Backups of deleted instances**. The backup file is retained for 7 days by default, and the actual retention period follows the retention duration configured upon instance deletion. During this period, you can rebuild the instance from **Backups of deleted instances**. For more information, refer to [Rebuilding an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilding_an_instance).

* After the instance is deleted or unsubscribed, all nodes and all data will be completely erased and cannot be recovered. Proceed with caution.

* After the instance is deleted or unsubscribed, the IP resources occupied by the instance will be released and may be used by other systems. Restoring the instance may not obtain the same IP again.

* When deleting an instance, you can reset the backup download policy of the instance. When unsubscribing from an instance, you cannot reset the policy, and the instance backups are automatically retained and cleared according to the settings in the backup policy.

* RDS for MySQL supports downloading backup files of deleted instances. If you need to download instance backups over the public network after deleting or unsubscribing from the instance, ensure that "Generate public network download address" is enabled in the instance's backup download policy. To view or adjust it, refer to [Modifying backup policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies).

* RDS for MySQL charges for the storage space used by basic backups and backups of deleted instances. Set up your backup policy reasonably to prevent excessive storage usage and unexpected fees. For more billing information about backup storage space, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

* Instances that use PrivateLink for connection cannot be deleted or unsubscribed.

* If the instance to be deleted or unsubscribed is part of a Global Active Database instance group, you must first disassociate the instance from the instance group before deleting or unsubscribing it. For details, refer to [Remove secondary instance and instance group](https://docs.byteplus.com/en/docs/RDS_for_MySQL/global_active_database?lang=en#aTPC7J19).

## Delete instance

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. On the left navigation bar, click **Instance list**.

4. Go to the **Instances** page, click the following buttons at the **Actions** column of the target instance:  **…**  \>  **\> Delete instance**.

   > **tip**

   * > If the instance state is **Stopped**, you can directly click **Delete instance** in the **Actions** column for the target instance.

   * > If you have not disabled deletion protection for the instance, hover over **Delete instance**, click **Disable deletion protection** in the pop\-up window, and then click **OK** in the dialog box to disable deletion protection for the instance. Repeat this step to start the instance deletion process again.

5. After configuring the following settings in the dialog box, click **Delete**.

   |Configuration items |Description |
   |---|---|
   |Backup policy |Set the retention policy for backup files after instance release. You can choose:<br><br><br>* **Do not retain backups**: that is, do not keep any backups of the instance after the instance is deleted.<br><br>* **Create a final backup and retain only this backup**: that is, the instance will be backed up and retained before the instance is deleted, and other backups of the instance will be deleted.<br><br>* **Create a final backup and retain all backups**: that is, all backups of the instance are retained after the instance is deleted. |
   |Confirm to delete |Enter the name of the instance to confirm deletion. |
   |Retention period |The retention duration of backup files after instance release. The value range is 7 to 3650 days, with a default of 7 days.<br><br>> **tip**<br><br><br>> Storage for backups of deleted instances is free for 30 days. After 30 days, fees are charged based on backup storage usage. For details on billing rules, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).<br> |

## Unsubscribe instance

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the region where the instance is located.

3. Click **Instances** in the left\-side navigation bar.

4. Go to the **Instances** page, click the following buttons at the **Actions** column of the target instance:  **…**  \> \> **Unsubscribe instance**.

   > **tip**

   > If you have not disabled deletion protection for the instance, hover over **Unsubscribe instance**, click **Disable deletion protection** in the pop\-up window, and then click **OK** in the dialog box to disable deletion protection for the instance. Repeat this step to start the instance deletion process again.

5. In the **Warning** pop\-up window, click **OK** to go to the **Unsubscribe management** page.

6. On the **Unsubscribe management** page, click **Confirm unsubscribe** to complete the unsubscription.

> **tip**

* > Deleting a pay\-as\-you\-go instance is an unsubscription and does not involve a refund.

* > Subscription instances support unconditional unsubscription within seven days. For detailed refund rules, refer to [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

## Related API

|API |Description |
|---|---|
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbinstance1) |Call the DeleteDBInstance API to delete an instance. |

## FAQ

### Does restoration of the RDS for MySQL instance work when backups are not retained upon instance deletion?

If no backup retention is selected when deleting an instance, all backup sets for the instance will be deleted. If you already have other valid backup sets locally, data can be restored from these backup sets; otherwise, data restoration is not possible. It is recommended to select retain backup sets for the backup policy when deleting an instance, and download them locally in a timely manner to avoid being unable to restore the instance due to data loss. Backup sets are retained for 7 days by default. You can customize the retention period based on business requirements. Since storage space occupied by backup sets is billed on a pay‑as‑you‑go basis, you are advised to configure the backup policy properly.
