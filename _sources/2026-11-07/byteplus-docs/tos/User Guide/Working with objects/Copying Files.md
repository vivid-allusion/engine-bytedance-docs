---
title: "Copying Files"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-copying-files"
---

TOS allows you to copy files or folders in a bucket to other paths. This topic describes how to copy files.

<span id="75499496"></span>
## **Note**


* This topic describes only copying files within the same region.

* Files cannot be copied to their original path.

* If you copy files between parent and child directories, data may be lost when files with the same name at different levels are overwritten. Proceed with caution.

* Files of the Archive, Cold Archive, and Deep Cold Archive types must be restored to a readable state before they can be copied.

* If versioning is enabled for your bucket, you need to toggle off Display Version before you can copy files.

* When copying files, the file size cannot exceed 50 GiB. If you want to copy large files, it is recommended to use [TOS Browser](https://docs.byteplus.com/en/docs/tos/Overview3) or [tosutil](https://docs.byteplus.com/en/docs/tos/overview).


<span id="0b404847"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, select the target files or folders and click **Copy to** above the file list.

4. In the **Copy To Folder** dialog box, click the target folder, and then click **Copy**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To copy files to a new folder, click <strong>Create Folder</strong> in the lower\-left corner of the dialog box. Then, click Edit, type the folder name, and click the Complete icon. For folder naming rules, see <a href="https://docs.byteplus.com/en/tos/docs/creating-a-folder?version=1.0.0">Creating a Folder</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the destination folder contains a file of the same name, select <strong>Overwrite</strong> or <strong>Skip</strong> and click <strong>OK</strong>.   </div>
