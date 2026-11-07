---
title: "System Settings"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/System-settings"
---

TOS Browser supports setting parameters for upload and download tasks. You can optimize the performance of upload or download by setting corresponding parameters.

<span id="4e585bdf"></span>
## **Procedure**


1. [Log in to TOS Browser](https://docs.byteplus.com/docs/tos/Log-in-to-tos-browser).

2. Click the target bucket name on the **Buckets list** page.

3. On the file list page, click on the top right of the page <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83c6da26b6b57688e384bda59aade5fb.png) </span> Button.

4. In the dialog box that pops up, select the **setting type** as needed, and then set the following parameters.



<Tabs>
<Tab zoneid="cuDiBclHn9" title="Upload and download settings">
<TabTitle>Upload and download settings</TabTitle>

On the **Upload and download settings** page, sign the setting parameters. The parameter descriptions are as follows:


* **Maximum number of upload tasks** : The maximum number of upload tasks that can be run simultaneously. The default is 10, with values ranging from 1 to 100.

* **Upload part concurrent**: When uploading large files, TOS Browser uses shard upload by default to upload files. You can set the maximum number of sharding uploads simultaneously in a upload task. The larger the upload sharding concurrency value, the faster the file upload speed. The default is 1, and the value range is 1 to 100.

* **Maximum number of download tasks** : The maximum number of downloadable tasks that can be run simultaneously. The default is 10, with values ranging from 1 to 100.

* **Download part concurrent** : When downloading large files, TOS Browser uses sharding download method to download files by default. You can set the maximum number of sharding downloads at the same time in a download task. The larger the download sharding concurrency value, the faster the download file. The default is 1, and the value range is 1 to 100.

* **Timeout**: The default is 30s, and the value range is 30s~ 600s.

* **Part size** : When uploading shards, the size of each sharding, the default is 8MiB, and the value range is 5MiB~ 1024MiB.

* **Number of retries** : The default value is 3, and the value range is 1 to 5.

* **Upload secondary validation** : After the file is uploaded, TOS Browser will perform consistency verification on the cloud file and the local file. If the verification fails, the upload task will fail. It is suitable for the scene where the local file is accidentally modified during the upload process.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Turning on <strong>Upload secondary validation</strong> will consume additional system resources and may trigger the card.   </div>
   

* **Download secondary validation** : After the file download is completed, TOS Browser will perform consistency verification on cloud files and local files. If the verification fails, the download task will fail. It is suitable for scenarios where local files are accidentally modified during the download process.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Opening the <strong>Download secondary validation</strong> function will consume additional system resources and may trigger the card.   </div>
   


</Tab>
<Tab zoneid="EyG3mdONsl" title="Security settings">
<TabTitle>Security settings</TabTitle>

Click the **Security Settings** tab and select whether to turn on **Hazardous operation level**, as follows:


* After opening, when you need to delete the file, you need to manually enter the confirmation information to reduce the possibility of your misoperation and protect the corresponding data security.

* It is not opened by default, that is, there will still be a dialog box prompt risk when deleting files, but there is no need to manually enter confirmation information.


</Tab>
</Tabs>



5. When setup is complete, click **Save**.
