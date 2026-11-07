---
title: "Downloading binlog backups"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_binlog_backups"
---

This topic describes how to download binlog files.

<span id="prerequisites"></span>
## **Prerequisites**


* An instance has been created and is in the **Running** status. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* There is already a data backup file in the same region.

* The size of the backup file to be downloaded does not exceed 1GB.


<span id="procedure"></span>
## **Procedure**


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no project is set, you should select the option <strong>All resources</strong> at this step.   </div>
   

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Backups** tab.

5. Click **Binlog backup** under the **Basic backup list** sub\-tab to view the list of binlog backup files.

6. Click the **Download backup file** button in the **Actions** column of the target binlog backup file.

7. In the **Download backup file** window, the download links for the backup file on the private network and the public network are provided, as well as the expiration time of the download links.

   * Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fef15836bf5e7ba39ac57ebcb2edb69.png) </span> on the right side of the download link to copy the download link.

   * Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_280a389372424f34510abd9e808152bd.png) </span> on the right side of the download link to download the backup file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The download link for the backup file is valid for 7 days. At any time within the validity period, the backup file can be downloaded through this link. If you forget the download link, you can click the <strong>Download backup file</strong> button to obtain the download link again. If the download link expires, you can click the <strong>Obtain backup</strong> button to obtain it again. The download address obtained each time is different.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The backup file cannot be directly downloaded on the current page through the private network address. Please copy the download link and download it in a private network environment (such as on an ECS in the same VPC).   </div>
   


<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeBinlogFiles](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebinlogfiles) |Call the DescribeBinlogFiles interface to query Binlog backup files. |
|[DownloadBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloadbackup) |Call the DownloadBackup interface to download the backup. |
|[GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_MySQL/getbackupdownloadlink) |Call the GetBackupDownloadLink interface to obtain the backup download link. |
