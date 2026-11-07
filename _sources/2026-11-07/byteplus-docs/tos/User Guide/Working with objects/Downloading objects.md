---
title: "Downloading objects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-downloading-a-file"
---

You can download an object from the bucket to your local system (to the default download path of the browser) in the TOS console.

<span id="e636302a"></span>
## Note


* When downloading files, the file size must not exceed 5 GiB. If you need to download large files, we recommend using [TOS Browser](https://docs.byteplus.com/en/docs/tos/Quickly-use-the-tos-browser) or [tosutil](https://docs.byteplus.com/en/docs/tos/Quick-start).

* Files in Archive Storage,Cold Archive Storage and Deep Cold Archive Storage need to be restored to a readable status before they can be downloaded.


<span id="40e275f5"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. On the **Objects** page, click **Download** in the **Actions** column of the object you want to download.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Downloading folders and batch downloading objects:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The console does not support downloading folders or multiple objects in batches directly. To perform these operations, use TOS Browser.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you try to batch download folders or objects from the console, a pop\-up window will appear, prompting you to install TOS Browser. After installing the latest version, click <strong>Open the TOS Browser</strong> to finish downloading.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If versioning is enabled for your bucket and you need to download a specified file version, see <a href="https://docs.byteplus.com/en/tos/docs/versioning-related-operations?version=1.0.0">Downloading a specified file version</a> for detailed directions.   </div>
