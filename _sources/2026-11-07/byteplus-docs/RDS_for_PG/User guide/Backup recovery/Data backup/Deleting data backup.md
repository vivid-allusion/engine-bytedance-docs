---
title: "Deleting data backup"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Deleting_a_data_backup"
---

To make it easier to manage the use of instance storage space, RDS for PostgreSQL supports deleting user\-created data backups. This article describes the steps to delete a data backup.

<span id="wXyVOkRv"></span>
## Precautions

Only deleting logical data backups is supported.

<span id="0XFVhW4r"></span>
## Prerequisites


* Already created an instance, and the instance is **Running**. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* A logical backup has been created and the status of the backup is **Succeeded**. For more information, see [Creating a backup](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_manual_backup).


<span id="MJ4ZXCnX"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. Under the **Data backup** tab, you can view a list of data backups for your instance.

7. In the Backup list, click  **...**  \> **Delete** in Actions column of the target logical backup.

8. In the pop\-up **Confirm the deletion of selected backup(s**) window, click **Delete**.


<span id="QNVJwAVb"></span>
## Related APIs


|API |Explanation |
|---|---|
|[DeleteBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DeleteBackup) |Call the DeleteBackup interface to delete the backup. |


&nbsp;
