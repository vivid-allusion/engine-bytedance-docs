---
title: "Upload overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview"
---

To efficiently manage, process, and distribute your media assets with BytePlus VOD, you must first upload them. This guide provides a comprehensive overview of the entire upload process, covering supported media types, various upload methods from the console to SDKs, available settings for customization, and how to receive event notifications.

## Media asset types and formats

BytePlus VOD supports three media asset types: **audio/video**, **materials**, and **images**.

### Audio/video

Audio/video refers to media assets that can be processed and played.

|**Type** |**Supported formats** |**Size limit** |
|---|---|---|
|Video |MP4, FLV, ASF (Advanced Systems Format, also known as WMV), RM, RMVB, MPEG, MOV, AVI, FLASH, MPEG\-TS (MTS), M4S, M3U8, Matroska (MKV) |A single file cannot exceed 20 GB. |
|Audio |MP3, M4A, WAV, WMA, AMR, AAC, OGG |A single file cannot exceed 20 GB. |

### Materials

Materials refer to auxiliary media assets that can be used as video covers, watermarks, patches, or editing creatives.

> **Warning**

> Materials cannot be transcoded or played back.

|**Type** |**Supported formats** |**Size limit** |
|---|---|---|
|Video |MP4, FLV, ASF (Advanced Systems Format, also known as WMV), RM, RMVB, MPEG, MOV, AVI, FLASH, MPEG\-TS (MTS), M4S, M3U8, Matroska (MKV) |A single file cannot exceed 500 MB. |
|Audio |MP3, M4A, WAV, WMA, AMR, AAC, OGG |A single file cannot exceed 50 MB. |
|Animated images |GIF and WEBP |A single file cannot exceed 50 MB. |
|Images |PNG, JPG, JPEG |A single file cannot exceed 50 MB. |
|Captions |SRT, VTT, and ASS |A single file cannot exceed 50 MB. |
|Fonts |TTF, FON, and TTC |A single file cannot exceed 50 MB. |

### Images

Images uploaded as image assets have a unique picture ID (`Pid`). You can enhance or process them and manage the original image together with its processed files. The console supports static PNG, JPG, JPEG, and WebP images and animated GIF and WebP images, with a maximum size of 50 MB per image. AI enhancement has stricter input limits. For upload instructions, see [Managing image assets](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management); for processing requirements, see [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement).

## Upload methods

BytePlus VOD provides two types of upload methods: **using GUI tools** and **using developer tools**.

### **Upload by using GUI tools**

To support quick uploads and large file uploads in simple operational scenarios without requiring code, BytePlus VOD provides the following GUI upload tools:

|**Method** |**Description** |**Applicable scenarios** |
|---|---|---|
|[The BytePlus VOD console](https://console.byteplus.com/vodpaas) |After activating the BytePlus VOD service, you can sign in to the BytePlus VOD console in your browser for uploads. Local file uploads as well as URL pull uploads are supported. |This is suitable for product trial and small\-scale file upload scenarios. |

### Upload by using developer tools

To meet developers' upload needs, BytePlus VOD provides developer tools in the form of upload SDKs and API operations:

|**Method** |**Description** |**Applicable scenarios** |**Documentation** |
|---|---|---|---|
|Upload SDK |Android, iOS, and Web are supported. Developers can integrate the BytePlus VOD Server SDK into the app server for issuing temporary upload tokens, and then pass them to the app client. |This is suitable for UGC, PGC, operational console, and other end user upload scenarios. |[Upload SDK overview](https://docs.byteplus.com/docs/byteplus-vod/docs-upload-sdk-overview) |
|Server SDK |The BytePlus VOD Server SDK encapsulates the logic of obtaining upload credentials and uploading, allowing you to directly upload from your app server to BytePlus VOD with simple configuration. The languages that are currently supported are Java, Python, PHP, Go, and Node.js. |This is suitable for automated uploads, mass video migration and uploads, and other scenarios. |[Server SDK overview](https://docs.byteplus.com/docs/byteplus-vod/docs-server-sdk-overview) |
|Batch URL upload |Call the API to pull media files from other platforms to BytePlus VOD. You just need to send the URL list to BytePlus VOD, and the BytePlus VOD server will trigger the upload task. This is suitable for large\-scale media asset migration and automated syncing. |This is suitable for scenarios where files are not stored on a local server or terminal and must be uploaded from a public URL. |[UploadMediaByUrl](https://docs.byteplus.com/docs/byteplus-vod/reference-uploadmediabyurl) |

## Upload settings

### Space upload settings

BytePlus VOD supports configuring upload settings at the space level. Once set, regardless of which upload method you use, as long as the audio and video assets are uploaded to the given space, the corresponding settings will automatically be triggered unless they are overridden by a supported upload parameter.

> **Note**

> For the steps for space upload settings, see [System settings](https://docs.byteplus.com/docs/byteplus-vod/docs-system).

The following table lists the supported space upload settings.

|**Upload settings** |**Description** |
|---|---|
|Automatically generate covers |Automatically capture the first non\-black frame and use it as the cover image.<br><br>> **Warning**<br><br><br>> Automatic cover generation will affect upload speed. The higher the resolution, the longer it will take. We recommend only enabling it when needed.<br> |
|Automatically trigger default workflow |You can set a default workflow that is automatically triggered upon upload. |
|Automatically set video status |Automatically publish audio and video assets. A playback address can only be obtained for audio/video with **Published** status. |
|Cross\-region upload acceleration |For a VOD space in Asia Pacific (Johor), configure an IGA custom domain to improve cross\-region upload stability and performance. For details, see [Cross-region upload acceleration](https://docs.byteplus.com/docs/byteplus-vod/docs-cross-region-upload-acceleration). |

### One\-time upload settings

BytePlus VOD also allows you to configure settings **during uploads**, such as settings for media asset management, transcoding, upload control and event notifications. The detailed upload settings for each method are as follows:

|**Feature** |**Setting** |**Description** |**Console** |**Upload SDK** |**Server SDK** |**Batch URL upload** |
|---|---|---|---|---|---|---|
|Media asset management (when uploading) |Set media asset name |Set the name of audio/video and materials when uploading. |Supported |Supported |Supported |Supported |
||Set video category |You need to create categories in advance and specify that the audio/video belongs to a certain category when uploading. |Supported |Supported |Supported |Supported |
||Set video tags |Set audio/video tags when uploading. |Not supported |Not supported |Supported |Supported |
||Set video cover |When uploading, specify a screenshot of a video frame at a specified point in time to be used as the video cover. |Not supported |Supported |Supported |Supported |
|Media processing |No transcoding |Direct upload without transcoding |Supported |Supported |Supported |Supported |
||Transcoding |Specify a workflow template when uploading. Once the upload is complete, the workflow is automatically executed.<br><br>> The specified workflow takes precedence over the space's default workflow. |Supported |Supported |Supported |Supported |
|Upload control |Get upload progress |Get the upload progress or status |Supported |Supported |Only supported by Java SDK |Supported |
||Pause/resume/stop upload |During the upload process, users can pause, resume, or terminate the upload as required. |Not supported |Supported |Not supported |Not supported |
||Multipart uploads |Divide a file to be uploaded into multiple parts and upload them separately.<br><br>Once the upload is complete, these parts are combined into a complete object. |Enabled by default |Enabled by default |Enabled by default |Enabled by default |
||Resume from breakpoints |If you encounter a network error during the upload process that causes the upload to fail, you can resume uploading from the last successfully uploaded part. |Not supported |Supported. Call API to enable |Not supported |Not supported |
|Callback |"Relay information as\-is" field in upload event notification |Once an upload is complete, the BytePlus VOD console will provide the "relay information as\-is" field to the developer through an upload completion event. |Not supported |Supported |Supported |Supported |

## Upload event notifications

You can configure callbacks to receive event notifications about the upload progress and status after you upload media files. BytePlus VOD allows you to configure HTTP or HTTPS callbacks to obtain event notifications.

> **Note**

> To learn about callback configuration, see [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).

The following table shows the upload events supported by BytePlus VOD:

|**Event type** |**Description** |
|---|---|
|[FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) |Triggered when the upload of audio and video files is complete.<br><br>> **Note**<br><br><br>> Because metadata extraction is asynchronous, the complete metadata may not be returned when the upload is completed. Therefore, to get the complete metadata, please use the UploadGetMetaComplete event.<br> |
|[MaterialUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-materialuploadcomplete) |Triggered when the upload of material files is complete. |
|[FileUploadByUrlComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadbyurlcomplete) |Triggered when the BytePlus VOD server has finished pulling the uploads from each URL after you call the [UploadMediaByUrl](https://docs.byteplus.com/docs/byteplus-vod/reference-uploadmediabyurl) API. |
|[UploadGetMetaComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-uploadgetmetacomplete) |Triggered once the BytePlus VOD server has extracted the metadata from an uploaded audio and video asset. |

## After uploads

After uploading media assets, you can use the following BytePlus VOD features. Note the precautions listed below:

|**Feature** |**Description** |
|---|---|
|Media asset management (after upload) |* By default, audio and video assets are **Unpublished** after being uploaded to BytePlus VOD. A playback address cannot be obtained for assets in this state. Therefore, before playing audio/video, you must modify the audio/video status to **Published**.<br><br>* Once an upload is complete, you can manage the media files, including the source files and transcoded files. |
|Media processing |You can perform transcoding and video enhancement, take screenshots, and add smart captions to uploaded audio and video assets. |
|Video playback |For audio and video assets uploaded to BytePlus VOD, you can preview them on the BytePlus VOD console, play them by integrating the BytePlus VOD Player SDK, or get the playback address to use with any player. |

## Upload security

To enhance upload security, the BytePlus VOD service implements the following measures:

* By default, it uses HTTPS upload domains to ensure the secure transmission of data.

* It conducts CRC32 checksum validation to verify the integrity of data during transmission and prevent unauthorized file alterations.

* Authentication is achieved through temporary upload tokens, thereby mitigating the risk of access key ID (AK) and secret access key (SK) exposure.
