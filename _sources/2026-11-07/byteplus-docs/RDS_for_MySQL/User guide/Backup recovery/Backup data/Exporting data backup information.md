---
title: "Exporting data backup information"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/exporting_data_backup_information"
---

This topic describes how to export the data backup information.

<span id="background"></span>
## Background

To facilitate the management of backup files, RDS for MySQL can export the data backup information as a .csv file. The exported information includes the backup ID, region, backup type, executor, backup method, backup file name, backup size, backup start time, backup end time, and database and table information.

<span id="prerequisites"></span>
## Prerequisites

The instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no project is set, you should select the option <strong>All resources</strong> at this step.   </div>
   

3. On the left navigation bar, click **Instances**.

4. On the **Instances** page, click the name of the target instance.

5. At the top of the page, click the **Backups** tab.

6. Click **Data backup** under the **Basic backup list** sub\-tab to enter the data backup list.

7. On the **Data backup** list page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1d6f112576cdde1dd67659ce4024550.png) </span> button in the upper right corner of the page.

8. In the popped\-up **Export backup list** window, set the **Backup period**. Click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The backup time period is defaulted to the last week.   </div>
