---
title: "Viewing data backup progress"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_data_backup_progress"
---

This topic describes how to view data backup progress.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Already created an instance, and the instance is **Running**. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* Manual backup has been completed, or an automatic data backup has been completed. For more information about creating backups manually or configuring automatic backups, refer to [Customizing data backup policy](https://docs.byteplus.com/en/docs/RDS_for_PG/customizing_backup_policies) or [Creating a data backup manually](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_manual_backup).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Choose **PostgreSQL** \> **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. In the backup list under the **Data backup** tab, locate the target backup.

7. In the **Status** column, you can view the progress of the data backup.

   * If a backup is in progress, the **Status** column shows **In progress** and the backup progress as a percentage.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You need to manually refresh the list to view the latest backup progress.      </div>
      

   * If the backup is complete, **Succeeded** will display in the **Status** column.
