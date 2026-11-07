---
title: "Downloading binlog backup in batches"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_binlog_backup_in_batches"
---

This topic describes how to download binlog files in batches.

<span id="prerequisites"></span>
## Prerequisites


* An instance has been created and is in the **Running** status. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* Data backup files in the same region are available.


<span id="precautions"></span>
## Precautions

When downloading binlogs in batch, the total amount of binlogs should not exceed 10GB.

<span id="procedure"></span>
## **Procedure**


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no project is set, you should select the option <strong>All resources</strong> at this step.   </div>
   

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Backups** tab.

5. Click **Binlog backup** under the **Basic backup list** sub\-tab to view the list of binlog backup files.

6. In the binlog backup file list, after checking the target binlog backup file, click **Batch download binlog**.

7. In the popped\-up download backup file window, click **Obtain**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking <strong>Obtain</strong>, the backend will automatically complete the prerequisite work required to obtain the backup file. After completion, you can choose the acquisition method of the backup file as needed.   </div>
   

8. In the popped\-up **Download backup file** window, the download links for the backup file on the private network and the public network are provided, as well as the expiration time of the download links.

   * Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fef15836bf5e7ba39ac57ebcb2edb69.png) </span> on the right side of the download link to copy the download link.

   * Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_280a389372424f34510abd9e808152bd.png) </span> on the right side of the download link to download the backup file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The validity period of the download address is 7 days. At any time within the validity period, the binlog backup file can be downloaded through this link.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The backup file cannot be directly downloaded on the current page through the private network address. Please copy the download link and download it in a private network environment (such as on an ECS in the same VPC).   </div>
