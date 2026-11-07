---
title: "Downloading backups of deleted instances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Downloading_backups_of_deleted_instances"
---

This topic describes how to download backups of deleted instances for RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

RDS for MySQL allows you to set a backup retention policy for an instance after it is deleted or unsubscribed. You can choose not to retain backups, to create and retain only the final backup, or to create a final backup and retain all backups. If you choose the latter two options, the specified backups are retained as configured and displayed in the Backups of deleted instances list after the instance is deleted or unsubscribed.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* To download instance backups over the public network after an instance is deleted or unsubscribed, ensure that you have enabled "Generate public network download address by default" in the instance's backup download policy. To view or modify the policy, refer to [Modify backup policies](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies).

* Downloading backups of deleted cloud disk instances is currently not supported.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Required

The target backup is the only backup for the deleted instance, and its state is **Recycled**.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar on the upper left, select the region.

3. On the left navigation bar, select MySQL \\> Backups.

4. Click the **Backups of deleted instances** tab at the top of the page.

5. On the **Backups of deleted instances** page, click **Download backup file** in the **Actions** column of the target backup file.

6. In the popped\-up Download backup file window, the download links for the backup file on the private network and the public network are provided, as well as the expiration time of the download links.

   * Click the icon to the right of the download link<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fef15836bf5e7ba39ac57ebcb2edb69.png) </span>to copy the download link.

   * Click the icon to the right of the download link<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_280a389372424f34510abd9e808152bd.png) </span>to download the backup file.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The download link for the backup file is valid for 7 days. The backup file can be downloaded from the link at any time within its validity period. After the download link expires, click <strong>Download backup file</strong> to obtain a new one. The download address is different each time.</div>


* <div data-tips="true" data-tips-type="tip">The backup file cannot be downloaded directly on the current page through the private network address. Copy the download link to download in the private network environment, such as the ECS of the same VPC.</div>
