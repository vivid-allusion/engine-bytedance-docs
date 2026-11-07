---
title: "Creating a binlog backup manually"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_backing_up_binlog"
---

This topic describes the process of manual binlog backup.

<span id="prerequisites"></span>
## **Prerequisites**

The instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id="procedure"></span>
## **Procedure**


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>All resources</strong> at this step.</div>



3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Backups** tab.

5. Click **Binlog backup** under the **Basic backup list** sub\-tab, and then click **Manually backup binLog** to complete the creation of binlog backup.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The binlog backup list is displayed in chronological order from earliest to latest by default. Newly created log backups will be displayed at the end of the log backup list.   </div>
   

<span id="next-steps"></span>
## Next Steps

[Downloading binlog backups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_binlog_backups)

<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[CreateBinlogBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createbinlogbackup) |Call the CreateBinlogBackup interface to create a log backup. |
