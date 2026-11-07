---
title: "Managing Parts"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-managing-parts"
---

If you upload a large file in parts, unmerged parts will be stored in the part list. This topic describes how to view part details and delete parts.

<span id="24bdca51"></span>
## **Note**

Like regular objects, uploaded parts take up storage space in the bucket and incur fees. To save costs, delete unneeded parts in time. To have uploaded parts deleted regularly, set lifecycle rules as instructed in [Setting Lifecycle Rules](https://docs.byteplus.com/en/tos/docs/setting-lifecycle-rules?version=1.0.0).

<span id="1b500e31"></span>
## **Viewing part details**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click **Parts management**.

4. In the **Parts** list pane, click **Details** in the **Actions** column of the target part to view its details.


<span id="30149fe9"></span>
## **Deleting parts**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click **Parts management**.

4. In the **Parts** list pane, delete parts as needed.

   * To delete a single part, click **Delete** in the **Actions** column of the target part and click **Save** in the pop\-up dialog box.

   * To delete all parts, click **Clear Parts** in the upper\-left corner of the **Part** list pane, and then click **Clear** in the pop\-up dialog box.

      Then, the **Task Progress Management** pane appears, where you can view the task information and status on the **Part Clean\-up Task** tab.
