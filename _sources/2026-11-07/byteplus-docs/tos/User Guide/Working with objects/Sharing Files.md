---
title: "Sharing  Files"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Sharing-files"
---

After you upload files to TOS, you can share files or folders with other users via URL. This article outlines the steps to share files.

<span id="b1d7d248"></span>
## Sharing method explanation

TOS offers various ways to share files, as explained below:


* By generating a URL on the file details page: Supports sharing a single object, with a default URL validity of 1 hour. For more details, please see [Viewing File Details](https://docs.byteplus.com/docs/tos/docs-viewing-file-details).

* By generating a URL for file sharing: Supports sharing files and folders, with the option to set the URL validity period ranging from 1 minute to 12 hours.

* By generating a pre\-signed URL through SDK: Supports sharing files and folders, allows setting URL validity period, with a range from 1 minute to 7 days. For more details, please refer to the respective SDK documentation.

* Share authorization codes using the tosutil tool: supports sharing files, folders, and all objects starting with a certain prefix. You can also set the validity period of the authorization code, ranging from 1 minute to 7 days. If you used a temporary access key to configure the tosutil tool, the maximum optional validity period of the authorization code will be the same as the expiration time of the temporary access key. For more details, please see [Create Authorization Code (share-crt)](https://docs.byteplus.com/docs/tos/Create-authorization-code-share-crt).


<span id="fb1208f4"></span>
## Precautions

After generating a file sharing link, the validity period cannot be altered. If the file sharing period is about to expire, it is recommended that you regenerate the file sharing URL.

<span id="f581ab76"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **file list** page, share according to the file type.

   * **Share folder**: Click on the **Share** option in the **Actions** column of the specified folder .

   * **Share file**: Click ··· \> **Share** in the **Actions** column of the specified file.

4. In the pop\-up dialog, set the following parameters.

   
   |**Parameters** |**Description** |
   |---|---|
   |Filename |The file name to be shared, automatically generated and cannot be modified. |
   |URL Validity Period |Set the URL validity period, ranging from 1 minute to 12 hours.<br><br>Any user can access or download this file directly via the URL within its validity period. |
   

5. After setting, click **Create Sharing**.

   After creation, TOS will automatically generate a sharing link, which you can copy and share with other users.
