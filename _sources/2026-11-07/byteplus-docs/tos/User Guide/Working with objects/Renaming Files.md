---
title: "Renaming Files"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-renaming-files"
---

This topic introduces the precautions and steps for renaming files in the TOS console.

<span id="c66d92b7"></span>
## **Precautions**


* You need to turn off **Display Version** in the upper\-right corner of the TOS console before you can rename files.

* If you enable versioning for a bucket, renaming a file in the bucket will not permanently delete the original file but will instead add a deletion mark to the file.

* Renaming a file will update the modification time of the file. If the file storage type is Infrequent Access Storage, Flashback Archive, Archive Storage, Cold Archive,or Deep Cold Archive, and the minimum storage duration requirement is not met, a storage fee will be charged. For billing details, see[ Storage Fees](https://docs.byteplus.com/en/tos/docs/storage-fee?version=1.0.0).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Files of the Archive Storage type can only be renamed after restoration. For more information, see <a href="https://docs.byteplus.com/en/tos/docs/restoring-files?version=1.0.0">Restoring Files</a>.   </div>
   

<span id="ec32af59"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, hover over the name of the target file and click the icon following the name.

4. In the pop\-up dialog box, rename the file and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the original file name contains a file extension, retain it in the new file name.   </div>
