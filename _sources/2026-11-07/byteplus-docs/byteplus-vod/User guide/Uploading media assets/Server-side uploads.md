---
title: "Server-side uploads"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-server-side-uploads"
---

Server\-side uploads refer to uploading media files to BytePlus VOD from your app server. Server\-side uploads are generally used for automated uploads and migration. This article provides information on server\-side upload methods, process flows, authentications, and references.

<span id="07a1af62"></span>
## **Server\-side upload methods**

BytePlus VOD currently supports the following server\-side upload methods.

<span id="8d65ad8d"></span>
### **Direct uploads**

Directly upload videos stored on your app server to BytePlus VOD via API or Server SDK. The process of direct uploads is shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fbbe4e112834295b0fc9223e06934ee~tplv-goo7wpa0wc-image.image) </span>

The process is explained as follows:


1. The app server calls the [ApplyUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-applyuploadinfo) API to get the upload address and credentials.

2. BytePlus VOD returns the upload address and credentials.

3. The app server uploads the file to BytePlus VOD.

4. The app server calls the [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) API to confirm the upload.

5. BytePlus VOD returns the upload results, such as Vid and Mid.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">BytePlus VOD automatically creates IDs for uploaded media assets. These IDs may differ depending on the type of media asset:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Videos are assigned a Video ID, abbreviated as Vid.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Materials are assigned a Material ID, abbreviated as Mid.   </div>
   

6. (Optional) If you have configured the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) event, BytePlus VOD will send a callback to the app server when uploading finishes.


<span id="e2ae6634"></span>
### **URL batch upload**

Pull media files stored on third\-party services by using the URLs that can be accessed over the Internet and upload them to BytePlus VOD. You just need to send the URL list to BytePlus VOD, and the BytePlus VOD server will trigger the upload task.

The process flow of URL batch upload is shown in the diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af4b1e83b88845e0a58f0ff672c57382~tplv-goo7wpa0wc-image.image) </span>

The process is explained as follows:


1. The app server obtains the video URL from the original storage service.

2. The original storage service returns the video URL.

3. The app server calls the [UploadMediaByUrl](https://docs.byteplus.com/docs/byteplus-vod/reference-uploadmediabyurl) API to submit the URL batch upload task.

4. When a task is successfully submitted, BytePlus VOD returns task information, including the upload task ID.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Task IDs are only stored on BytePlus VOD servers for 7 days.   </div>
   

5. BytePlus VOD asynchronously pulls the video file from the original storage service via the URL.

6. (Optional) If you have configured the [FileUploadByUrlComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadbyurlcomplete) event, BytePlus VOD will send a callback to the app server after each URL is pulled.

7. (Optional) The app server can also actively call the [QueryUploadTaskInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-queryuploadtaskinfo) API to obtain the URL batch upload results.


<span id="99a74d51"></span>
## **References**

BytePlus VOD offers Server SDKs that encapsulate logic for obtaining upload addresses and credentials, and for performing uploads. You can simply configure the AK and SK on the app server, along with a simple API call, to begin uploading media assets. For details, refer to the following documents:


* [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

* [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

* [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

* [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)
