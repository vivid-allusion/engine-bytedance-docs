---
title: "Set Server-side Encryption for the Bucket"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-server-side-encryption-for-the-bucket"
---

After setting server\-side encryption for the bucket, files uploaded to this bucket will inherit the bucket’s server\-side encryption settings by default if you do not specify the encryption method for the files. This article explains how to set server\-side encryption for the bucket.

<span id="1945d50c"></span>
## Precautions


|**Type** |**Precautions** |
|---|---|
|Encryption method |* Only objects uploaded after enabling SSE on the bucket will be encrypted. This does not change the SSE status of objects uploaded before the feature was enabled. Changing the SSE settings of a bucket will only affect the objects uploaded thereafter. It does not alter the SSE settings of objects already present before the change.<br><br>* Only SSE\-KMS and SSE\-TOS are supported for bucket encryption settings. |
|SSE\-KMS encryption |* To use SSE\-KMS for server\-side encryption for the first time, you need to activate the KMS service. Activating the KMS service is free, but using the KMS service will incur charges. Using SSE\-KMS for server\-side encryption will result in API call charges, and creating KMS keys will incur key management fees charged by KMS. For more information, please see [BytePlus KMS Pricing](https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing).<br><br>* SSE\-KMS only encrypts object data but does not encrypt object metadata.<br><br>* To upload an encrypted object using SSE\-KMS, you need the `kms:GenerateDataKey` permission for the key; to download an SSE\-KMS encrypted object, you need the `kms:Decrypt` permission for the key.<br><br>* Objects encrypted with SSE\-KMS do not support anonymous user access. You must subscribe to the KMS service and have permission to access the primary key in order to use signed access for objects encrypted with SSE\-KMS.<br><br>* Only Asia Pacific(Johor) ,Asia Pacific (Jakarta),China (Beijing),China (Shanghai) ,China (Hong Kong) regions support SSE\-KMS server\-side encryption. For a detailed introduction to server\-side encryption, please refer to [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview). |
|SSE\-TOS encryption |Only Asia Pacific(Johor), Asia Pacific (Jakarta), China (Beijing), China (Shanghai), China (Hong Kong) regions support SSE\-TOS server\-side encryption. For a detailed introduction to server\-side encryption, please refer to [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview). |


<span id="6ff547a6"></span>
## Enable server\-side encryption when creating a bucket

You can activate server\-side encryption when creating a bucket. For detailed operations, please refer to [Creating a Bucket](https://docs.byteplus.com/docs/tos/docs-create-a-bucket).

<span id="afbdd692"></span>
## Enable server\-side encryption after creating a bucket


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane,select **Basic configurations \> Static website**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click on <strong>Overview</strong> in the left navigation bar, then in the <strong>Basic</strong> <strong>information</strong> section, click on <strong>Server\-side</strong> <strong>encryption</strong> on the right side of <strong>Settings</strong>, and then set the server\-side encryption method on the <strong>Server\-side</strong> <strong>encryption</strong> page.   </div>
   

4. On the **Server\-Side encryption** page, click **Edit**, and choose the server\-side encryption method.

   * **None**: No encryption.

   * **SSE\-TOS**: Managed encryption keys by TOS, refers to files being automatically encrypted by TOS upon upload and automatically decrypted upon download. The keys are managed by TOS, for more information, see [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).

   * **SSE\-KMS**: Files are encrypted and decrypted using keys managed by BytePlus KMS, for more information, see [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview). After choosing **SSE\-KMS**, you also need to select **a custom key**. If you have not created a key, you can go to KMS service to create one. For detailed operations, please refer to [KMS Quick Start](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management).

5. Click **OK**.


<span id="8edfea54"></span>
## Modify the server\-side encryption of the bucket


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Basic configurations \> Static website**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click on <strong>Overview</strong> in the left navigation bar, then in the <strong>Basic</strong> <strong>information</strong> section, click on <strong>Server\-side</strong> <strong>encryption</strong> on the right side of <strong>Settings</strong>, and then set the server\-side encryption method on the <strong>Server\-side</strong> <strong>encryption</strong> page.   </div>
   

4. On the **Server\-Side encryption** page, click **Edit**, and choose the server\-side encryption method.

   * **None**: No encryption.

   * **SSE\-TOS**: Managed encryption keys by TOS, refers to files being automatically encrypted by TOS upon upload and automatically decrypted upon download. The keys are managed by TOS, for more information, see [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).

   * **SSE\-KMS**: Files are encrypted and decrypted using keys managed by BytePlus KMS, for more information, see [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview). After choosing **SSE\-KMS**, you also need to select **a custom key**. If you have not created a key, you can go to KMS service to create one. For detailed operations, please refer to [KMS Quick Start](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management).

5. Click **OK**.


<span id="b55c9b3e"></span>
## Related Operations


* Setting server\-side encryption when uploading files

   You can set server\-side encryption when uploading files. For specific operations, please refer to [Uploading a File](https://docs.byteplus.com/docs/tos/docs-uploading-a-file).

* Viewing the server\-side encryption method of the bucket

   You can view the server\-side encryption method of the bucket in the **Overview** page **Basic Information** section. For specific operations, please refer to [Bucket Overview](https://docs.byteplus.com/docs/tos/docs-bucket-overview).
