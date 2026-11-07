---
title: "Viewing data backup progress"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_data_backup_progress"
---

This topic describes how to view data backup progress.

<span id="prerequisites"></span>
## Prerequisites


* The instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* A data backup has been manually created or automatically completed. For more information about how to manually create a backup or configure automatic backup, refer to [Customizing data backup policies](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies) or [Manually creating a data backup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_creating_a_data_backup).


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>All resources</strong> at this step.</div>



3. On the left navigation bar, click **Instances**.

4. On the **Instances** page, click the name of the target instance.

5. At the top of the page, click the **Backups** tab.

6. Click **Data backup** under the **Basic backup list** sub\-tab to enter the data backup list and locate the target backup.

7. In the **Status** column, you can view the progress of the data backup.

   1. If the backup is in progress, the **Status** column will display **In progress** and show the backup progress as a percentage.

   2. If the backup is completed, the **Status** column will display **Backup succeeded**.


<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) |Call the DescribeBackups interface to view the list of backup files. |
