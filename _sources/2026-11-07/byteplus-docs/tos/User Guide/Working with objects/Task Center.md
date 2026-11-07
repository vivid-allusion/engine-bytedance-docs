---
title: "Task Center"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-task-center"
---

In TOS, you can submit a task for file upload, file copy, file move, directory deletion, file restoration, or part deletion. Then, you can view the task status and manage the task at the task center.

<span id="639ae940"></span>
## **Note**

Refreshing the page after submitting a task will terminate the task and clear the records of non\-deletion tasks.

<span id="b782ae6c"></span>
## **Task statuses**


* Preparing: The task is being prepared. You can pause it using the corresponding option on its right side.

* Executing: Some files under this task are being executed. You can pause or cancel the task using the corresponding option on its right side.

* Failed: Some files under this task failed to be executed. You can retry or cancel the task using the corresponding option on its right side.

* Succeeded: The task succeeded. You can clear the record of the task using the corresponding option on its right side.

* Stopped: The task has stopped. You can start or cancel the task using the corresponding option on its right side.


<span id="a3073141"></span>
## **Viewing the task status**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the upper\-right corner of the **Overview** page, click **Task center**.

3. In the **Task progress management** pane, view the task status.

   * Click the **Upload task** tab to view the statuses of file upload tasks.

   * Click the **Copy and move task** tab to view the statuses of file copy or file move tasks.

   * Click the **Delete task** tab to view the statuses of file/directory deletion tasks.

   * Click the **Restore task** tab to view the statuses of file restoration tasks.

   * Click the **Parts clean\-up task** tab to view the statuses of part deletion tasks.


<span id="fdbd5ceb"></span>
## **Viewing files under a task**

The following describes how to view the information of a file in an upload task. The steps are the same for copy/move, deletion, restoration, and part clean\-up tasks.


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the upper\-right corner of the **Overview** page, click **Task center**.

3. On the **Upload task** tab of the **Task progress management** pane, click a task name to view the files under that task.

   * Viewing the file upload progress

      On the right side of the pane, view the upload progress of files under the task.

   * Viewing the file status

      On the left of the pane, view files under the task that are in **Preparing**, **Executing**, **Succeeded**, **Failed**, or **Stopped** status.

   * Sharing a file

      On the left of the pane, click **Succeeded**, and then click **Copy Link** in the **Actions** column of the target task.
