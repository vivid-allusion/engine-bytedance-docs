---
title: "Use RenameObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Use-renameobject"
---

Object storage supports the RenameObject feature, which allows objects to be renamed directly within the bucket without using the CopyObject and DeleteObject methods. You can enable the RenameObject feature and then use the RenameObject interface to rename objects. This article introduces the background information, considerations, and operational steps for enabling, using, and disabling the RenameObject feature.

<span id="fb0416ca"></span>
## Background information

The RenameObject feature is not the same as the [Renaming Files](https://docs.byteplus.com/docs/tos/docs-renaming-files) feature. Compared to file renaming, the RenameObject feature renames objects more quickly, capable of renaming within milliseconds. The RenameObject feature supports renaming all types of object names. After renaming an Appendable object's name, the object will still maintain the same Append capability as the original object.

<span id="ff92afef"></span>
## Precautions


|**Category** |**Precautions** |
|---|---|
|Constraints and limitations |The RenameObject feature is mutually exclusive with the version control feature. If version control is enabled or paused on your bucket, the RenameObject feature cannot be used. |
|Renamed content |The RenameObject interface only modifies the name of the object and does not change metadata such as the modification time of the object. |
|The renamed object |* Only objects uploaded after enabling RenameObject can be renamed; renaming is not supported for pre\-existing objects uploaded before this feature was enabled.<br><br>* Files of type archive storage,cold archive storage and deep cold archive storage can only be renamed using the RenameObject feature after they are restored. For specific operations, please see [Restoring Files](https://docs.byteplus.com/docs/tos/docs-restoring-files).<br><br>* Concurrent renaming of the same object using the RenameObject feature is not supported.<br><br>* RenameObject supports renaming objects created by all types, including those created by Put, Multi\-Upload, Append, Copy, Rename, etc. After renaming, the Appendable object still retains the same ability to append as the original object. |


<span id="f86532f9"></span>
## Enable RenameObject

<span id="57363ab1"></span>
### Enable RenameObject when creating a bucket


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. On the navigation pane on the left, click **Buckets**. In the upper\-left corner of the page displayed, click **Create bucket**.

3. On the **Create bucket** page, set the bucket parameters, click **Advanced settings**, and enable the **RenameObject** feature.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For other parameters concerning bucket creation, please see <a href="https://docs.byteplus.com/docs/tos/docs-create-a-bucket">Creating a Bucket</a>.   </div>
   

4. Click **Create**.


<span id="d98b1e60"></span>
### Enable RenameObject on the created bucket.

TOS supports enabling the RenameObject feature from the console and also supports using the PutBucketRename API. For detailed information about PutBucketRename, please see [PutBucketRename](https://docs.byteplus.com/docs/tos/Putbucketrename).


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation bar, select **Basic configurations \> RenameObject**.

4. On the **RenameObject** page, click **Edit**.

5. Select **Enabled** RenameObject, then click **Select**.

6. In the pop\-up dialog, click **Confirm**.


<span id="a9785c50"></span>
## Use RenameObject

After enabling the RenameObject feature, you can use the RenameObject interface to rename objects. For detailed information, please refer to [RenameObject](https://docs.byteplus.com/docs/tos/Renameobject).

<span id="ae280e66"></span>
## Disable RenameObject

TOS supports disabling the RenameObject feature through the console and also supports using the DeleteBucketRename interface to disable the RenameObject feature. For detailed information about DeleteBucketRename, please refer to [DeleteBucketRename](https://docs.byteplus.com/docs/tos/Deletebucketrename).


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation bar, select **Basic configurations \> RenameObject**.

4. On the **RenameObject** page, click **Edit.** 

5. Select **Disabled** RenameObject feature, click **Select**.

6. In the popup dialog, click **Confirm**.
