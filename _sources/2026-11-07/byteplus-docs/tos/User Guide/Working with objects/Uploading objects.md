---
title: "Uploading objects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file"
---

This topic describes how to upload a file in the TOS console.

<span id="dbc7c538"></span>
## Note


* Before file upload, make sure that you have created a bucket as instructed in [Creating buckets](https://docs.byteplus.com/en/tos/docs/create-a-bucket?version=1.0.0).

* For file naming rules, see [Object](https://docs.byteplus.com/en/docs/tos/docs-common-concepts#object).

* In simple mode, you can upload files up to 5 GiB.

* In multipart upload in the console, you can upload files up to 50 GiB. For even larger files, use the API, which allows you to upload files up to 48.8 TiB (up to 5 GiB per part, and up to 10,000 parts). For detailed directions, see Multipart Upload.

* By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform this operation, the account owner must grant the user the `tos:PutObject` permission using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).


<span id="ffdfdbae"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click **Upload File**. On the page displayed, set the file parameters.

   
   |**Parameter** |**Description** ||
   |---|---|---|
   |Upload to |Specify the storage path in the TOS bucket to which the file will be uploaded.<br><br><br>* **Current Directory**: Upload the file to the current directory.<br><br>* **Specified Directory**: Specify a directory to store the uploaded file. The specified directory name should conform to the following conventions:<br><br>   * It can contain Chinese words, English letters, digits, and common characters.<br><br>   * You can quickly create a subfolder by entering a name with both the folder and subfolder names separated by a forward slash (/), the name of which cannot start with a forward slash (/) or backslash (\) and cannot contain consecutive forward slashes (/).<br><br>   * You cannot name a folder `..`.<br><br>   * Folder names must be unique in the same bucket. ||
   |To be uploaded |Select or drag and drop the target local file or folder.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Filenames must be unique in a bucket. If the name of the file to upload is the same as that of an existing file in the bucket, TOS will:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Overwrite the existing file if versioning is not enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Retain both files if versioning is enabled. The uploaded file becomes the latest version, and the existing file becomes the historical version. For more information, see <a href="https://docs.byteplus.com/en/tos/docs/overview?version=1.0.0">Versioning overview</a>.</div><br> ||
   |Advanced settings |Storage type |Expand **Advanced settings** to specify the storage type of the file, which is the same as that of the bucket. The options are as follows:<br><br><br>* **Inherit Bucket** (default value): The storage type is the same as that of the bucket.<br><br>* **Standard Storage**: This storage type is highly available, highly reliable, and high\-performance, which applies to the scenario where data is accessed frequently.<br><br>* **Intelligent Tiering**: This storage type applies to the scenario where data is accessed in multiple modes. You are charged for file monitoring. For more information, see [Intelligent Tiering](https://docs.byteplus.com/en/tos/docs/overview_1?version=1.0.0).<br><br>* **Infrequent Access Storage**: This storage type applies to the scenario where data is accessed infrequently. The minimum storage duration is 30 days.<br><br>* **Archive Flashback**: This storage type applies to the scenario where data is rarely accessed. The minimum storage duration is 90 days.<br><br>* **Archive**: This storage type applies to the scenario where data is stored in the long run and rarely accessed. The minimum storage duration is 90 days. You need to restore data before accessing it from Archive Storage.<br><br>* **Cold Archive**:This storage type applies to the scenario where data is basically not accessed, and can accept a certain response time for access. The minimum storage period is 180 days. Cold Archive data must be restored before it can be accessed.<br><br>* **Deep Cold Archive**:It is suitable for extremely cold data that requires ultra\-long\-term storage.The minimum storage period is 180 days.Deep Cold Archive data must be restored before it can be accessed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Cold Archive storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information, see <a href="https://docs.byteplus.com/en/tos/docs/storage-type?version=1.0.0">Storage type</a>.</div><br> |
   ||Server\-Side encryption |Expand **Advanced settings** to set the server\-side encryption method. Explanation of different encryption methods is as follows:<br><br><br>* **Inherit Bucket Encryption Configuration**: The default value, consistent with the server\-side encryption method of the storage bucket. You can view the server\-side encryption method of the storage bucket on the **Overview** page **Basic information** section. You can also modify the server\-side encryption method of the storage bucket, for specific operations, please see [Set server-side encryption for the bucket](https://docs.byteplus.com/docs/tos/Set-server-side-encryption-for-the-bucket).<br><br>* **SSE\-TOS**: The TOS\-managed key approach means that files are automatically encrypted on upload, stored encrypted, and decrypted on download, with keys managed by TOS. For more information, please see [Server-side encryption overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br>* **SSE\-KMS**: Utilizes BytePlus KMS\-managed keys for file encryption and decryption. For more information, please see [Server-side encryption overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only Asia Pacific(Johor), Asia Pacific (Jakarta), China (Beijing), China (Shanghai), and China (Hong Kong) supports SSE\-TOS and SSE\-KMS.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To use SSE\-KMS for server\-side encryption, you need to activate KMS service. Activating KMS service is free, using KMS service incurs charges. Using SSE\-KMS for server\-side encryption incurs API call charges, and creating KMS keys incurs key management charges, both of which are levied by KMS. For more information, please see <a href="https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing">BytePlus KMS pricing</a>.</div><br> |
   ||Encryption Key Type |Expand **Advanced settings**, default to **Custom Key**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when <strong>Server\-Side encryption</strong> selects <strong>SSE\-KMS</strong>, this parameter is displayed.</div><br> |
   ||Custom Key |Expand **Advanced settings**, and select the key created in the KMS service. If you have not created a key, you can go to the KMS service to create one. For specific operations, please see [KMS quick start](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when <strong>Server\-Side encryption </strong>selects <strong>SSE\-KMS</strong>, this parameter is displayed.</div><br> |
   ||Metadata |Expand **Advanced settings** and click Add Field to set object metadata. For more information on available metadata in TOS, see [Managing object metadata](https://docs.byteplus.com/en/tos/docs/managing-file-metadata?version=1.0.0). |
   ||Access permission |Set the ACL policy for the object as follows:<br><br><br>* Inherit Bucket: Objects will inherit the bucket's ACL, meaning the object's ACL policy will be consistent with the bucket's ACL policy. For the corresponding relationship between object ACL and bucket ACL, please refer to [Object ACL default policy](https://docs.byteplus.com/docs/tos/docs-overview_4#9b50293d).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also enable the default bucket ACL inheritance feature. Once enabled, the ACL policy of newly uploaded objects will default to be consistent with the bucket ACL policy. For specific instructions, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-configuring-an-object-acl#c50eea03">Enabling objects to automatically apply bucket ACL</a>   </div><br>   <br><br>* Private: The default value is that only the owner of the object and authorized accounts have read and write permissions, which is recommended for use.<br><br>* Public read: Any user has read access to this object (including anonymous users), but only the owner of the object and authorized accounts have write access.<br><br>* Public read/write: Any user has read and write permissions for this object (including anonymous users). |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Then, you can view the list of files to upload on the <strong>Upload File</strong> page.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click <strong>Remove</strong> in the <strong>Operation</strong> column of a file to cancel its upload, or click <strong>Clear List</strong> above the file list to cancel the upload of all files.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Do not refresh or close the page during file upload; otherwise, the upload task will be interrupted and the list will be cleared.   </div>
   

4. After confirmation, click **Upload**. Then, you are redirected to the **Task Progress Management** page.

   You can also click **Task Center** in the upper\-right corner of the console to view the task progress and status.


<span id="1113b5ea"></span>
## Further operations

You can view the file upload progress and status on the **Upload Task** tab in the **Task Progress Management** pane. You can also do the following on the **Upload Task** tab:


* **Cancel upload**: In the file list, click **Cancel** in the **Actions** column of the target file.

* **Reupload**: If an upload task is canceled or failed, you can click **Retry** in the **Actions** column of the target file.

* **Clear the record**: Click **Clear Record** in the **Actions** column of the target file to clear its upload record. This will not delete the file.

* **Copy the link**: Click **Copy Link** in the **Actions** column of the target file to copy its download link.

* **Clear successful tasks**: Click **Clear Successful Tasks** in the upper\-left corner of the file list to clear the records of all successful uploads.
