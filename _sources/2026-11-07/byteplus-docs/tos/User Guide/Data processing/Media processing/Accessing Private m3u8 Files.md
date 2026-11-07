---
title: "Accessing Private m3u8 Files"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Accessing-private-m3u8-files"
---

TOS supports the access to private m3u8 files, effectively protects the content security of m3u8 files, and meets your access needs for m3u8 files. This article introduces how to enable the access function for private m3u8 files, obtain download authorization for private m3u8 files, and more.

<span id="8c1d59a2"></span>
## Precautions


* The feature for accessing private m3u8 files is in a beta\-testing phase, please contact the account manager if you wish to use it.

* Access to private m3u8 files that have been encrypted server\-side is not supported.


<span id="1303f890"></span>
## Enabling the Access to Private m3u8 Files

<span id="bfa01388"></span>
### Prerequisites

To initially enable the access to private m3u8 files, you need to visit the **Media Processing** page, under the **Private m3u8** tab, click **Authorize**, and in the pop\-up dialog, click **Confirm,**  to grant TOS product services the permissions to read and write files in the corresponding storage bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the <strong>media handling</strong> page displays <strong>"You have authorized the TOS Object Storage Service to read and write files to your bucket"</strong>, it means the TOS authorization is complete, and no further authorization action is required.</div>


<span id="c075088b"></span>
### Operation Steps


1. Log in to [Object Storage Console](https://console.volcengine.com/tos).

2. In the left navigation bar, click **Bucket List**, then on the **Bucket List** page, click on the target bucket name.

3. In the left navigation bar, select **Data Processing** \> **Media Processing**.

4. On the **Media Processing** page, click on the **Private m3u8** tab.

5. Click **Edit**, then at the **Current Status**, enable the Private m3u8 feature.

6. Click **Confirm**.


<span id="25fc23c1"></span>
## Obtain the download authorization for the private m3u8 file

You can obtain the download authorization for the private m3u8 file through the Pm3u8 interface, then copy the API endpoint URL with authorization information to the browser, and watch the audio and video data of the m3u8 file in the browser. For more information, please see [Pm3u8](https://docs.byteplus.com/docs/undefined/67e4cd3f8daf51050219f0a2).
