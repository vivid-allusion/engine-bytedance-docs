---
title: "Deleting a File"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-deleting-a-file"
---

This topic describes how to delete a file no longer needed in the TOS console,thereby saving your storage space and costs.

<span id="e87e59c4"></span>
## **Note**


* Files cannot be recovered after being deleted. Proceed with caution.

* If you need to delete a large number of files, we recommend that you use the lifecycle management feature as instructed in [Setting Lifecycle Rules](https://docs.byteplus.com/en/tos/docs/setting-lifecycle-rules?version=1.0.0).

* If versioning is enabled for your bucket, you need to toggle on Display Version on the File List page and select a specific file version to delete. Otherwise, deleting a file will add a **deletion mark** to, rather than permanently delete, the file. For how to delete a historical file version, see [Permanently deleting a file](https://docs.byteplus.com/en/tos/docs/versioning-related-operations?version=1.0.0).


<span id="b215a1dc"></span>
## **Deleting a single file**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click  **··· \> Delete** in the **Actions** column of the target file.

4. In the pop\-up dialog box, click **Delete**.


<span id="7481fba7"></span>
## **Batch deleting files**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, select the target files and click **Delete** in the bottom left of the page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you select the box in front of Filename, TOS will select all files on the current page, not all files in the bucket.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If versioning is enabled for your bucket but <strong>Show versions</strong> is not toggled on, deleting files will add deletion marks to, rather than permanently delete, the files. To permanently delete files, toggle on <strong>Show versions</strong> as instructed in <a href="https://docs.byteplus.com/en/tos/docs/versioning-related-operations?version=1.0.0">Permanently deleting a file</a>.   </div>
   

4. In the pop\-up dialog box, click **Delete**.
