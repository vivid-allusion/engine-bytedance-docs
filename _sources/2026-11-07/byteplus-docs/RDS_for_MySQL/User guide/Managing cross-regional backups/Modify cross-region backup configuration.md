---
title: "Modify cross-region backup configuration"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Modify_cross-region_backup_configuration"
---

This topic describes the procedure for modifying the cross\-region backup configuration for an instance in the cross\-regional backup Instances.

## Precautions

* The cross\-regional backup instances lists instances for which cross\-regional backup is or was enabled To enable cross\-regional backup for an instance where it is not enabled, refer to [Modifying backup policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies).

* Enabling cross\-region snapshot backup and cross\-region Binlog log backup for cloud disk instances will incur additional storage and traffic fees. For more information, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price?lang=en).

* After you modify the backup region, existing backups in the original region are automatically purged upon expiration in accordance with the configured retention policy. Before purging, you can still use these existing backups for cross\-region restoration. New cross\-region backups will be saved to the updated backup region.

## Billing

* Before the existing backups in the original region are purged, they are still billed at the cross\-region backup rates of the original region. Backups generated in the new region are billed at the cross\-region backup rates of the new region. For fee description, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price?lang=en).

* The fees for both regions will be billed in parallel until all existing backups in the original region are completely cleared.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the region.

3. On the left navigation bar, select **MySQL** \> **Backups**.

4. Click the **Cross\-regional backup** tab at the top of the page, and in the cross\-regional backup Instances, click **Cross\-region backup configuration** in the **operation** column of the target instance.

5. In the **Cross\-region backup configuration** page that appears, complete the following settings and click **OK** to complete the cross\-region backup configuration.

   |Parameter |Is it required? |Description |
   |---|---|---|
   |Cross\-region backup copy |Yes |Enable or disable cross\-region backup replication for physical backups. |
   |Cross\-regional backup region |Yes |Select the destination region for cross\-region backup. |
   |Retain the backups until the instance is released |No |Whether to retain backup files for a long time before releasing the instance. After enabling this function, there is no need to set the backup retention days. Off by default. |
   |Number of days to retain cross\-regional backup |No |The length of time for retaining backup files after instance release. The value range is 7 to 3650 days, with a default of 7 days. |
   |Cross\-regional binlog backup |Yes |Enable or disable cross\-region backup replication for binlog backups. |
