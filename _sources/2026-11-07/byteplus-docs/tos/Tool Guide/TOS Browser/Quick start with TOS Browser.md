---
title: "Quick start with TOS Browser"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quickly-use-the-tos-browser"
---

This article introduces the quick start process for TOS Browser, including creating buckets, uploading objects, downloading objects, and deleting objects.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Install TOS Browser](https://docs.byteplus.com/docs/tos/Install-tos-browser)

2. [Log in to TOS Browser](https://docs.byteplus.com/docs/tos/Log-in-to-tos-browser)


<span id=".5q2l6aqk5LiA77ya5Yib5bu65a2Y5YKo5qG2"></span>
## Step 1: Create a bucket


1. On the **Buckets** page, click **Create Bucket** in the upper\-left corner.

2. In the pop\-up dialog, set the bucket parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the parameter descriptions of creating a bucket, see <a href="https://docs.byteplus.com/docs/tos/docs-create-a-bucket">Creating buckets</a>.   </div>
   

3. After completing the settings, click **Create**.


<span id=".5q2l6aqk5LqM77ya5LiK5Lyg5paH5Lu2"></span>
## Step 2: Upload an object to the bucket


1. On the **Buckets** page, click the bucket where you want to upload an object.

2. On the Objects page, click **Upload file.** 

3. On the **Upload file** page, set the parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the explanation of upload parameters, see <a href="https://docs.byteplus.com/docs/tos/docs-uploading-a-file">Upload file</a>.   </div>
   

4. After selecting the object to upload, click **Upload ** to start uploading the object.

   After clicking Upload, the page automatically redirects to the **Task schedule management** panel. You can also click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1631884ec2eb31777fbc962bd23306a.png) </span> icon at the top right to view the task progress and status.


<span id=".5q2l6aqk5LiJ77ya5LiL6L295paH5Lu2"></span>
## Step 3: Download the object


1. Click the target bucket name on the **Buckets** page.

2. On the Objects page, click **Download** in the **Actions** column of the specified object to download it.


<span id=".5q2l6aqk5Zub77ya6I635Y-W5paH5Lu25Zyw5Z2A"></span>
## Step 4: Get the object address


1. Click the target bucket name on the **Buckets** page.

2. On the Objects page, click  **...**    **\> Get address ** in the **Actions** column of the specified object.

3. In the pop\-up dialog, select the URL type you want to obtain. Click the copy button behind the URL address to get the corresponding URL.

   The address type descriptions are as follows.

   
   |Type |Note |
   |---|---|
   |Object address |Supports configuring URLs and pre\-signed URLs.The download address of the object is valid for 1 hour. |
   |Pre\-signed URL |* If your bucket policy conflicts with object access control permissions — for example, objects are set to **public read** but the bucket policy denies access — the bucket policy takes precedence. In this case, you may be unable to access your objects via the object URL. You can obtain a **pre\-signed URL** to access the object instead.<br><br>* The default validity period of the pre\-signed URL is 3 minutes; it supports a range from 0 to 7 days. You can set the validity period of the pre\-signed URL as needed. After setting, click **Generate and copy links**. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the bucket containing the object was created on or before January 3, 2024, scan the QR code below the <strong>URL</strong> to preview or download the object according to its type.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the bucket containing the object was created after January 3, 2024, scanning the QR code below the <strong>URL</strong> only allows downloading the object.   </div>
   


<span id=".5q2l6aqk5LqU77ya6YCA5Ye6LXRvcy1icm93c2Vy"></span>
## Step 5: Log out of TOS Browser

When you no longer need to use the TOS Browser tool, you can click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa5cfee9c7a29530d08874bfb27fbcaa.png) </span> icon at the top right and click **Log out** to exit the TOS Browser.
