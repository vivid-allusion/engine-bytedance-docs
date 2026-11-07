---
title: "Uploading data from WeChat Mini Programs to TOS"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-data-directly-to-TOS-from-wechat-mini-program"
---

This article explains how to upload files directly to TOS in the WeChat Mini Program environment.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

WeChat Mini Program, an app that requires no download, attracts more developers and users. How to upload files from WeChat Mini Program to TOS becomes a concern for developers. You can add signature information in the form and use the PostObject interface to upload files from WeChat Mini Program to TOS as an HTML form. For more information, see [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject) and [Post form pre-signature](https://docs.byteplus.com/docs/tos/Post-form-presignature-node-js-sdk).

<span id=".5q2l6aqk5LiA77ya6YWN572u6Leo5Z-f6K6_6Zeu"></span>
## Step 1: Configure cross\-origin access

Uploading data from WeChat Mini Program to TOS sends a cross\-origin request to TOS. When TOS receives a cross\-origin request, it reads the cross\-origin rules of the bucket to perform corresponding permission checks. You need to set up cross\-origin access rules in TOS to enable proper data transmission from the WeChat Mini Program to TOS. For detailed information about cross\-origin access rules, see [Cross-Origin Access Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.

3. In the left navigation bar, select **Permissions \> CORS rules.** 

4. On the **CORS rules** page, click **Create rule**.

5. On the **Create rule** page, configure the following parameters.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7569114b24356ea6c2628d7bbd7de480.png) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Origin |Set to the domain name of the WeChat Mini Program.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also set it to the wildcard asterisk (\*), allowing requests from any cross\-origin source.</div><br> |
   |Operation methods |Select **PUT**, **GET**, **POST**, **DELETE**, and **HEAD**. |
   |Allow\-Headers |Set to wildcard asterisk (\*). |
   |Expose\-Headers |Set to ETag, x\-tos\-request\-id, and x\-tos\-version\-id. One per line, separated by carriage returns. |
   |Max\-Age |Default value |
   

6. Click **Create**.


<span id=".5q2l6aqk5LqM77ya6YWN572u5Z-f5ZCN55m95ZCN5Y2V"></span>
## Step 2: Configure domain whitelist

The WeChat Mini Program requires a whitelist to access domains. You need to configure a whitelist for the Bucket domain in the WeChat Mini Program to enable normal access to the TOS storage bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to bind your own domain to the Bucket domain and use your own domain to access files stored in TOS. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/tos/Set-up-a-custom-domain-name">Setting up a custom domain</a>.</div>



1. Obtain the Bucket domain.

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.

   3. In the left navigation bar, click **Overview.** 

   4. On the **Overview** page, in the **Access domain** section, in the **Bucket Domain** column, obtain the domain corresponding to **External Access**.

2. Configure the domain whitelist.

   1. Log in to the WeChat Mini Program platform.

   2. On the mini program page, click **Server Domain** area, then select **Start Configuration**.

   3. In the **Configure Server Domain** dialog, enter the Bucket domain in both the **uploadFile valid domain** and **downloadFile valid domain** input boxes.

   4. Click **Save and Submit**.


<span id=".5q2l6aqk5LiJ77ya5LiK5Lyg5pWw5o2u5YiwLXRvcw=="></span>
## Step 3: Upload data to TOS

Use the uploadFile interface of the WeChat mini program to upload files. The sample code is as follows:

```javascript
// Ensure the SDK version is greater than or equal to 2.6.10
import { TosClient } from '@volcengine/tos-sdk'
async function wxUploadToTOS() {
  // Create a client instance
  const client = new TosClient({
    accessKeyId: "Provide your access key", // Temporary AccessKey ID obtained from the STS service
    accessKeySecret: "Provide your secret key", // Temporary AccessKey Secret obtained from the STS service
    stsToken: "Provide your session token", // Temporary Session Token obtained from the STS service
    region: "Provide your region", // Specify the region where the bucket is located. For example, for Beijing (North China 2), set this to "cn-beijing".
  });

  const res = await wx.chooseMessageFile({ count: 1 });
  const path = res.tempFiles[0].path;
  const bucket = 'test-bucket';
  const key = 'wx-miniprogram-test';

  //For the security of your data, we recommend using signed uploads. For details, see: https://docs.byteplus.com/en/docs/tos/Normal-pre-signature-node-js-sdk
  //For more information about POST form pre-signing, refer to "Including Signatures in Forms for Browser Uploads".
  const formData = await client.calculatePostSignature({
    bucket,
    key,
    expiresIn: 3600,
     // To add custom fields, uncomment and modify the following lines:
     //fields: {
     //  'key': 'value'
     // }
  })
  // Replace bucketHost with the corresponding bucket endpoint, e.g., ${bucket}.tos-${region}.bytepluses.com
  const bucketHost = `${bucket}.tos-ap-southeast-3.bytepluses.com`;
  const url = `https://${bucketHost}/${encodeURI(key)}`
  const result = await wx.uploadFile({
    filePath: path,
    name: 'file', // Fixed as "file"
    url,
    formData,
    success: (res) => {
      if (res.statusCode === 204) {
        console.log('Upload successful');
      }
    },
    fail: err => {
      console.log(err);
    }
  })
  console.log(result, 'result');
}
```


You need to replace the following parameters in the sample code according to your actual situation:


|**Parameter** |**Description** |
|---|---|
|accessKeyId |Temporary AccessKey ID obtained from the STS service.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can create temporary credentials and obtain temporary keys through the STS service. For detailed steps, see <a href="https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service">Accessing TOS with temporary credentials of Security Token Service</a>.</div><br> |
|accessKeySecret |Temporary Secret AccessKey obtained from the STS service. |
|stsToken |Temporary access Session Token obtained from the STS service. |
|region |The region where the bucket is located. |
|endpoint |The access domain name of the bucket.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information about bucket domain names, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and Endpoint</a>.</div><br> |
|const bucket |Name of the storage bucket. |
|const key |Object name. |
|const url |Access URL in the format `https://&lt;Bucket domain&gt;/&lt;object name encoded&gt;`. |
