---
title: "Modifying the data backup name"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Modifying_the_data_backup_name"
---

RDS for MySQL supports modifying data backup names. This topic describes the procedure.

<span id="CHvNQ3kA"></span>
## Prerequisites

An instance has been created and has local or cross\-region data backups.

<span id="f3NiIhuA"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the target instance name.

5. At the top of the page, click the **Backups** tab.

6. On the **Data backup** tab, click **Data backup** on the **Basic backup list** or **Cross\-regional backup list** tab to go to the data backup list for the current or a cross\-region.

7. In the data backup list for the current or a cross\-region, click Edit next to the target backup name, enter a backup name in the text box that appears, and click **OK**. The backup name must meet the following rules:

   * It cannot start with a hyphen (\-).

   * It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).

   * The length must be between 1 and 128 characters.
