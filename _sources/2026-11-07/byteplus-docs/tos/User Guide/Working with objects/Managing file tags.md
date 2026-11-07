---
title: "Managing file tags"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-managing-file-labels"
---

TOS supports object tagging and tag\-based object lifecycle management. This topic introduces object tags and describes the steps for relevant object management.

<span id="dbaa718f"></span>
## Object tag restrictions

An object tag is a key\-value pair and has the following restrictions:


|Item |Description |
|---|---|
|Billing |Currently, the object tagging feature is available for free. The timing for its transition to a paid version and the billing details will be communicated separately in advance. Make sure to keep track of the relevant announcements. |
|Quantity |An object can have up to 10 tags, each of which is identified by a unique key. |
|Key\-value pair |* The key can contain up to 128 characters.<br><br>* The value can contain up to 256 characters.<br><br>* Both the key and value are case\-sensitive. Valid characters include uppercase and lowercase letters, digits, spaces, and the following special symbols: `_ .` `: / = + -`. |
|Others |* If you want to set object tags that contain arbitrary characters through HTTP headers, the tag keys and values need to be URL\-encoded.<br><br>* Modifying the tags of an object does not update the object's Last\-Modified timestamp.<br><br>* When you copy objects across regions, tag information of objects is not transferred. |


<span id="dd55be05"></span>
## Setting object tags

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before setting object tags, ensure that you have the required permissions. You need to be either the bucket creator or a user with the read and write permissions on object tags to proceed. The read and write permissions on object tags can be granted only through bucket policies. The relevant actions are:</div>



* <div data-tips="true" data-tips-type="tip">GetObjectTagging: Gets object tags.</div>


* <div data-tips="true" data-tips-type="tip">PutObjectTagging: Sets tags for an object.</div>


* <div data-tips="true" data-tips-type="tip">DeleteObjectTagging: Deletes tags from an object.</div>



<div data-tips="true" data-tips-type="tip">For more information, see <a href="https://docs.byteplus.com/en/tos/docs/templates-and-parameters?version=1.0.0">Bucket policies</a>.</div>


The TOS console allows you to set tags for only uploaded files. To set tags when you upload files, use the APIs or SDK to upload files and specify the object tags through the `x-tos-tagging` request header. This feature is supported by the following APIs:


* PutObject

* CreateMultipartUpload

* CopyObject


<span id="00642f85"></span>
### Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, choose  **··· \> Edit tags** in the **Actions** column of the target file.

4. In the pop\-up dialog box, click the **Add Field** icon and set the tag keys and values as needed.

5. Click **Save**.


<span id="9412a5e6"></span>
## Managing object tags


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, choose  **··· \> Edit tags** in the **Actions** column of the target file.

4. In the pop\-up dialog box, modify tag information or delete tags as needed.

5. Click **Save**.


<span id="80890b43"></span>
## Further operations

You can continue to define lifecycle rules based on the object tags that you set. For more information, see [Setting lifecycle rules](https://docs.byteplus.com/en/tos/docs/setting-lifecycle-rules?version=1.0.0).
