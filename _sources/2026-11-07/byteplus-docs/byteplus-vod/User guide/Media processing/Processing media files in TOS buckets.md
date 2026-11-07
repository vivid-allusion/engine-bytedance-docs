---
title: "Processing media files in TOS buckets"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/process-media-files-stored-in-tos-buckets"
---

By associating an existing BytePlus TOS (TOS) bucket with the BytePlus VOD service, you can perform a wide range of media processing operations on your files in TOS. This document guides you through associating a TOS bucket with the VOD service to process your media files using features like transcoding and video enhancement.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Feature availability</div>


<div data-tips="true" data-tips-type="warning">This feature requires allowlist access. Please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112">contact us</a> to enable this feature.</div>


<span id="Benefits"></span>
## Benefits


* **Flexible storage**: Process files directly in your TOS bucket without data migration, keeping your existing storage architecture intact.

* **Comprehensive features**: Access a wide range of media processing features, including video and audio transcoding, super\-resolution, screenshot capture, video enhancement, and watermarking.


<span id="Billing"></span>
## Billing


* **Media processing and distribution**: Fees for media processing and CDN distribution are charged by BytePlus VOD. For details, see [BytePlus VOD Pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* **Storage**: Storage fees for your files are charged by BytePlus TOS. For details, see [BytePlus TOS Storage Fee](https://docs.byteplus.com/en/docs/tos/docs-storage-fee).


<span id="f7cf2d43"></span>
## Restrictions


* You can only associate buckets in the **Johor** region.

* A TOS bucket can only be associated with one VOD space at a time. For example, if the test\-tos bucket is associated with the test space in VOD, it cannot be associated with any other space.

* To ensure that media assets can be correctly identified and processed in stages of the VOD service (such as transcoding, VOD CDN, and playback), please follow [Character rules for file naming](https://docs.byteplus.com/docs/byteplus-vod/docs-character-rules-for-file-naming).

* If you use VOD's media asset management features, avoid deleting files directly from your TOS bucket, as this can lead to metadata inconsistencies.


<span id="Before you begin"></span>
## Before you begin


* Ensure that you have activated the [BytePlus TOS](https://console.byteplus.com/tos) and [BytePlus VOD](https://console.byteplus.com/vod) services.

* This feature is available only in the **Asia Pacific (Johor)**  region.


<span id="Procedure"></span>
## Procedure

<span id="Step 2: Associate a TOS bucket to VOD"></span>
### Step 1: Associate a TOS bucket to VOD


1. Follow these steps to associate your TOS bucket with VOD:

2. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vod) and enter a specific space.

3. Click **System settings** \> **Post\-upload actions** on the left navigation bar.

4. Click the **Storage settings** tab.

5. Click the **Add storage address** button.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If this is your first time adding a TOS Bucket in the VOD console, you need to complete a one\-time cross\-service authorization. This authorization grants the VOD service the necessary permissions to read and write objects in your TOS bucket.   </div>
   

6. Select the target TOS bucket from the drop\-down list and click **Confirm**.

7. Click **Set as default** to set the associated bucket as the default storage address. The switch takes about 5 minutes to take effect. During this period, uploaded videos may be stored in the previous default storage address.


<span id="Step 3: Processing media files"></span>
### Step 2: Processing media files

After associating the bucket, you can begin processing your media files. The processing method varies based on how and when your files are uploaded.


* **Existing media files**: For files already in your TOS bucket before you associate it with VOD, you can only process them using [DirectUrl mode](https://docs.byteplus.com/docs/byteplus-vod/docs-media-asset-management#c2223f21). This mode identifies files by their `FileName` (the file path in the bucket).

* **New media files**: For files uploaded after associating the bucket and setting it as the default storage:

   * Files uploaded through the VOD console or SDK can be processed using either Vid or DirectUrl mode.

   * Files uploaded directly to TOS can only be processed using DirectUrl mode.


The following steps describe how to process your files in **DirectUrl mode**:


1. **Configure media processing templates and workflows**: All media processing configurations are done in the BytePlus VOD console. You first create individual processing templates and then combine them into a workflow.

   * **Templates**: Create or configure templates for transcoding, screenshots, video enhancement, and watermarking based on your needs. For details, see the following documents:

      * [Audio transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template)

      * [Video transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-video-transcoding-template)

      * [Low-bitrate HD template](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template)

      * [Video enhancement template](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template)

      * [Snapshot template](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template)

   * **Workflows**: Combine your configured media processing templates into a workflow. For details, see [Creating a custom workflow](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#a9136274).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">It is recommended that you enable <strong>Custom file path</strong> and set the file path in the output file path text box. For example, you can set the output file path to <code>{{filePrefix}}{{fileTitle}}</code>. VOD will automatically use the source file's prefix and name as the path for the transcoded file. If the source file path is <code>vod/video.mp4</code>, the output path for the m3u8 file will be <code>vod/video.m3u8</code>. For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path">Customizing output file path</a>.      </div>
      

2. **Trigger and monitor workflows**: You can trigger and monitor workflows in the following ways:

   * **VOD console**:

      * **Trigger**:

         1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vod) and enter the desired space.

         2. Navigate to **Media assets** \> **Video** \> **DirectUrl mode**.

         3. Select the desired video and click **Process video** to manually trigger a workflow.

      * **Monitor**: Go to the **Media processing** \> **Workflows** page to view the execution status of each task.

   * **OpenAPI or Server\-Side SDK**:

      * **Trigger**: Programmatically trigger a workflow by calling [StartWorkflow](https://docs.byteplus.com/docs/byteplus-vod/reference-startworkflow). In your request, you must specify the `TemplateId` (workflow ID) and use the `DirectUrl` parameter to provide the `FileName` (the path to the file in the TOS bucket). Example request:

         ```JSON
         POST /?Action=StartWorkflow&Version=2020-08-01 HTTP/1.1
         Host: vod.volcengineapi.com
         Content-Type: application/json
         
         {
           "DirectUrl": "{\"FileName\":\"path/to/your/video.mp4\",\"SpaceName\":\"your-vod-space\"}",
           "TemplateId": "your-workflow-id"
         }
         ```
         

      * **Monitor**: Get workflow results by setting up event notifications for the [WorkflowComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete) event.

3. **View the output files**: After media processing is complete, you can view the output files in two ways:

   * **VOD console**:

      1. In the VOD console's left navigation bar, click **Media assets** \> **Video**.

      2. At the top\-left of the **Video** page, select the **DirectUrl mode** tab.

      3. Under the **Uploaded** tab, locate the processed file using the filename.

   * **TOS console**: You can also sign in to the [BytePlus TOS console](https://console.byteplus.com/tos) to find the file in your bucket by its name. From there, you can download, share, or view its details.


<span id="559162ef"></span>
## Next steps

After adding an object storage bucket and processing your media files, you can retrieve the playback addresses of the original videos and the processed output videos from the VOD service. To do this, you need to:


1. Add a domain name and **set its origin to the object storage address**. For details, see [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management).

2. Obtain the playback address of the processed video using the VOD console, API/Server SDK, or by manual concatenation. For details, see [Obtaining playback addresses](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-playback-addresses#a46c2be1).


<span id="a6cde137"></span>
## FAQ

**1. Where are the output files from media processing stored?** 

The output files are stored based on the default storage address configured in your VOD space.

**2. How do I cancel the association with a TOS bucket?** 

To unlink a bucket, navigate to **System settings** \> **Post\-upload actions** \> **Storage settings** in the VOD console, locate the associated bucket, and click **Delete**.
