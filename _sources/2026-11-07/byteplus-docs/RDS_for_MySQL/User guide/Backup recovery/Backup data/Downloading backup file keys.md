---
title: "Downloading backup file keys"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_backup_file_keys"
---

RDS for MySQL supports encrypting backup files. If the encrypted backup file is downloaded to local use, the backup file needs to be decrypted. This topic introduces the operation steps for downloading the backup file key.

<span id="prerequisites"></span>
## Prerequisites


* Instances have been created and are in the **Running** state. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* There are already encrypted data backup or log backup files in the same region.


<span id="steps"></span>
## Steps


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar on the upper left, select the project and region to which the instance belongs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, for this operation, you should select the project as <strong>All resources</strong>.   </div>
   

3. On the **Instancet** page, click the name of the target instance to enter the **Summary** page.

4. Click the **Backups** tab to enter the **Backups** page.

5. Under **Data backup** or **Binlog backup**, you can view the data backup list or log backup list of the instance.

6. According to the type of the target backup file, complete the following steps to download the key of the backup file.

   * In the **Data backup** list, click  **... \> Download Key** in the operation column of the target backup file.

   * In the **Binlog backup** list, click the **Download key** button in the operation column of the target backup file.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">The file name of the backup file key is <code>file name of the backup file.key</code>. For example, if the file name of a data backup file is <code>full-1234567890.xbstream</code>, then the file name of its key is <code>full-1234567890.xbstream.key</code>.</div>
