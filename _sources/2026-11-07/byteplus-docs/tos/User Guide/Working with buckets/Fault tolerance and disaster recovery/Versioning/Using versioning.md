---
title: "Using versioning"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-versioning-related-operations"
---

When versioning is enabled, TOS assigns a unique version ID to each object in a bucket. This ID can be used to restore the object if it is accidentally deleted or overwritten. This topic introduces the operations you can perform after enabling versioning.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

For more information on versioning and how to enable it, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

After enabling versioning, you can only suspend it. You cannot revert it to the "Disabled" state. When you suspend versioning, existing objects in your bucket do not change.

<span id=".5p-l55yL5paH5Lu255qE5Y6G5Y-y54mI5pys"></span>
## **Viewing a historical object version**

When versioning is enabled on your bucket, the objects list displays the latest versions and hides historical versions by default. Follow the steps below to view historical versions.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the Buckets list, click the bucket you want to check.

3. On the **Objects** page, toggle the **Show versions** switch on in the upper\-right corner. The list will then display the historical versions.

   <div style="text-align: center">
   <img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a128aa7567ba577dd89e32cccb295e47.png" />   </div>
   

4. Click **Details** in the **Actions** column of the historical version to view its details, including **filename**, **version ID**, and **URL**.


<span id=".5b275bqV5Yig6Zmk5paH5Lu2"></span>
## **Permanently deleting an object**

To permanently delete an object from a versioning\-enabled bucket, you must first toggle the **Show versions** switch. Follow the steps below to permanently delete an object.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the Buckets list, click the bucket you want to manage.

3. On the **Objects** page, toggle the **Show versions** switch on in the upper\-right corner.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleting an object from a versioning\-enabled or versioning\-suspended bucket without enabling <strong>Show versions</strong> will add a <strong>deletion mark</strong> to the object rather than deleting it. In other words, the object is still stored in your bucket, but hidden.   </div>
   

4. On the **Objects** page, click  **... \>**  **Permanently Delete** in the **Actions** column of the object you want to remove.

5. In the box that appears, confirm the deletion by clicking **Delete**.


<span id=".5b275bqV5Yig6Zmk5paH5Lu25aS5"></span>
## Permanently deleting a folder

You can delete any folders that are no longer needed. Deleting a folder will also delete its contents. Follow the steps below to permanently delete a folder.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the Buckets list, click the bucket you want to manage.

3. On the **Objects** page, toggle the **Show versions** switch on in the upper\-right corner.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleting a folder from a versioning\-enabled or versioning\-suspended bucket without enabling <strong>Show versions</strong> will add a <strong>deletion mark</strong> to the folder rather than deleting it. In other words, the folder is still stored in your bucket, but hidden.   </div>
   

4. On the **Objects** page, click **Permanently Delete** in the **Actions** column of the folder you want to remove.

5. In the box that appears, confirm the deletion by clicking **Permanently Delete**.


<span id=".5Yig6Zmk5paH5Lu255qE5Yig6Zmk5qCH6K6w"></span>
## Deleting a deletion mark

Deleting an object from a versioning\-enabled or versioning\-suspended bucket without enabling **Show versions** will add a **deletion mark** to the object rather than deleting it. Follow the steps below to delete a deletion mark.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the Buckets list, click the bucket you want to manage.

3. On the **Objects** page, toggle the **Show versions** switch on in the upper\-right corner.

4. On the **Objects** page, click  **... \>**  **Delete** in the **Actions** column of the deletion mark you want to remove.

5. In the box that appears, confirm the deletion by clicking **Delete**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Rather than deleting the object, deleting a deletion mark cancels the object deletion operation. To delete the object, see <a href="https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#.5b275bqV5Yig6Zmk5paH5Lu2">Permanently deleting an object</a>.   </div>
   

<span id=".5LiL6L295oyH5a6a54mI5pys5paH5Lu2"></span>
## **Downloading a specific object version**

Once versioning is enabled, all versions of an object are retained by default. Follow the steps below to download a specific version.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the Buckets list, click the bucket you want to manage.

3. On the **Objects** page, toggle the **Show versions** switch on in the upper\-right corner.

4. On the **Objects** page, click **Download** in the **Actions** column of the version you want.


<span id="f51b1a84"></span>
## Restoring an object

Once versioning is enabled, all versions of an object are retained by default. You can restore an object by either deleting the latest version or copying an earlier version. Follow the steps below to restore an object:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend restoring objects by copying their historical versions. Deleting the latest version is an irreversible action, whereas copying the historical version allows you to keep all versions of the object.</div>



<Tabs>
<Tab zoneid="pdSUfKZZNV" title="Delete the latest version">
<TabTitle>Delete the latest version</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the Buckets list, click the bucket you want to manage.

3. On the **Objects** page, toggle the **Show versions** switch on in the upper\-right corner.

4. Click  **... \> Permanently Delete** in the **Actions** column of the latest version you want to remove.

5. In the box that appears, enter Permanently Delete and click **Delete**.

   Once the latest version has been deleted, the previous version automatically becomes the latest.


</Tab>
<Tab zoneid="KTS4NY9Y81" title="Copy an earlier version">
<TabTitle>Copy an earlier version</TabTitle>

You can use the CopyObject API to copy an earlier version of the object to the same bucket. After this process, a new version identical to the historical version is created and becomes the latest version. The previous latest version then becomes a historical version and all object versions are preserved. For instructions, see [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).


</Tab>
</Tabs>
