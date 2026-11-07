---
title: "Deleting a Folder"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-deleting-a-folder"
---

You can delete a folder that is no longer needed. Deleting the folder will delete both the folder and its files.

<span id="623c38f7"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, delete folders as needed.

   * If versioning is not enabled for the bucket:

      Click **Delete** in the **Actions** column of the target folder. In the pop\-up dialog box, confirm the information and click **Delete** .

   * If versioning is enabled for the bucket:

      * Permanently deleting a folder:

         1. Turn on **Show versions** in the upper\-right corner of the file list.

         2. Click **Delete** in the **Actions** column of the target folder. In the pop\-up dialog box, confirm the information and click **Delete**.

            The folder and its files will be permanently deleted.

      * Making a folder a historical version:

         1. Turn off **Show versions** in the upper\-right corner of the file list.

         2. Click **Delete** in the **Actions** column of the target folder. In the pop\-up dialog box, confirm the information and click **Delete**.

            The folder and its files will become historical versions. Toggle on **Display Version** to view historical versions of files.

            You will then be redirected to the **Task progress management** pane, where you can view the folder deletion method and status on the **Delete task** tab.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">All files in a deleted folder will be deleted and unrecoverable. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Deleting a folder takes time. Wait patiently and do not repeat your operation.</div>


* <div data-tips="true" data-tips-type="warning">When deleting a folder:</div>


   * <div data-tips="true" data-tips-type="warning">Do not refresh the page or close the task progress pane; otherwise, the deletion task may be interrupted, or the number of deleted files may be inaccurate.</div>


   * <div data-tips="true" data-tips-type="warning">Do not upload new files to the folder being deleted; otherwise, the newly uploaded files may be deleted.</div>
