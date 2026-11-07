---
title: "Deleting media files"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-deleting-media-files"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important information that may affect your business. Please read this article carefully before proceeding.</div>


To manage your media assets in BytePlus VOD, you can delete files at various granularities. This guide provides detailed procedures for deleting media files using the console, API, or Server SDKs. You will learn how to delete all files associated with a video, only frame extraction results or transcoded outputs, or clear all files within an entire space.

<span id="4d3c4dfc"></span>
## Introduction

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">All deletions are physical and unrestorable. Please proceed with caution.</div>



|Feature |Description |Method |
|---|---|---|
|Delete all media files |Delete all media files associated with a specified **Vid**, including uploaded original videos, output files after media processing, cover images, snapshots, and frame extraction results. |* Console<br><br>* API<br><br>* Server SDK |
|Delete frame extraction results |Delete some or all frame extraction results associated with a specified **Vid** while retaining the source video. You can filter the results by user tag or task run. |* API |
|Delete media processing output files |Delete the media processing output files associated with a specified **Vid** and keep the original uploaded video. |* Console<br><br>* API<br><br>* Server SDK |


<span id="e33ee12b"></span>
## Using the console

<span id="3e14cbd3"></span>
### Deleting uploaded media assets

Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and delete media files on the **Videos** and **Materials** pages. You can directly click the **Delete** button in the Actions column or select multiple videos and then click the **Delete** button in the upper\-left corner of the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a61c834f603242d1ac050111d43fc164~tplv-goo7wpa0wc-image.image) </span>

<span id="58d66e77"></span>
### Deleting transcoded output files


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vod) and navigate to the desired space.

2. In the left navigation bar, click **Media assets** \> **Videos**.

3. Find the video for which you want to delete transcoded files and click **Details** in the **Actions** column.

4. In the **Playback address** tab, you can click **Delete** to delete the transcoded files.


<span id="44d7d281"></span>
### **Clearing all files in a space**

You can clear all files in a space from the BytePlus VOD console.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">The clearing operation deletes all files and their metadata in your space. The deleted data cannot be accessed or restored. Please proceed with caution.</div>



1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and navigate to the desired space.

2. In the left navigation bar, click **Media assets** \> **Videos**.

3. Click **Clear files**.

4. In the dialog box that appears, enter the space name as prompted.

5. Select the scope of application:

   * **All files**: Clears all files in both DirectUrl mode and Vid mode.

   * **Videos in Vid mode**: Clears only the video files in Vid mode.

   * **Materials in Vid mode**: Clears only the material files in Vid mode.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have <a href="https://docs.byteplus.com/docs/byteplus-vod/process-media-files-stored-in-tos-buckets#step-1-associate-a-tos-bucket-to-vod">associated an object storage bucket with space</a>, clearing all files is not supported.   </div>
   

6. Click **Confirm** **clear**. During the clearing process, you can click the **Stop** button to interrupt the operation.


<span id="a0d36d8c"></span>
## Using the API or Server SDKs

You can call the following APIs to delete media files:


* [DeleteMedia](https://docs.byteplus.com/docs/byteplus-vod/reference-deletemedia)

* [DeleteFrameExtractions](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteframeextractions)

* [DeleteTranscodes](https://docs.byteplus.com/docs/byteplus-vod/reference-deletetranscodes)

* [DeleteMediaTosFile](https://docs.byteplus.com/docs/byteplus-vod/deletemediatosfile)


We recommend that you use the Server SDKs to call APIs to delete the media files. For details, refer to the following documents:


* [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

* [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

* [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

* [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)


<span id="8164c689"></span>
## Event notification

Deleting media files is an asynchronous task, and it may take some time. If you have any tasks that must be run after deletion is complete, you can set up a deletion completion callback, as shown below:


* [DeleteMediaComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-deletemediacomplete)

* [DeleteTranscodesComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-deletetranscodescomplete)
