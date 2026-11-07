---
title: "Managing media asset information"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/media-asset-information"
---

Media asset information is the collection of data and metadata generated when you upload and process media in BytePlus VOD. This includes basic details, transcoding outputs, and playback information. This document describes the different types of media asset information available in Vid and DirectUrl modes and shows you how to update basic information like titles and descriptions using the console or API.

<span id="029b01c7"></span>
## **What is media asset information?** 

When you upload media assets to BytePlus VOD for transcoding, the process generates a high volume of audio, video, images, text, and other business data. We refer to this business data, its descriptive metadata, and related information as media asset information.

<span id="fb96555f"></span>
### Vid mode

The following table lists the types and description of media asset information in Vid mode.


|**Types of media asset information** |**Description** |**Documentation** |
|---|---|---|
|Basic information |* Information about audio and video: Includes the video ID (Vid), name, description, storage address, publishing status, tags, category, creation date, and so on.<br><br>* Information about materials: Includes the material ID (Mid), name, description, material type, file format, file size, creation date, and so on. |See `VodMediaBasicInfo` in the [GetMediaList](https://docs.byteplus.com/docs/byteplus-vod/reference-getmedialist) API |
|Input file information |Information related to original audio and video files that you upload to BytePlus VOD services, including the file ID, MD5 value, file type, encoding type, video width, video height, format, duration, size, file address, definition, bitrate, frame rate, storage type, and so on. |See `VodMediaBasicInfo` in the [GetMediaList](https://docs.byteplus.com/docs/byteplus-vod/reference-getmedialist) API |
|Output file information |Information related to the files output by BytePlus VOD after media processing, including the file ID, MD5 value, file type, watermarks and tags, encryption status, format, duration, size, file address, and so on. |See `VodTranscodeInfo` in the [GetMediaList](https://docs.byteplus.com/docs/byteplus-vod/reference-getmedialist) API |
|Playback information |Includes resolution, audio quality, format, encoding type, playback address, bitrate, width, height, file size, duration, and so on. |See the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo)API |
|Snapshot results |Includes snapshot type, format, image width and height, storage address, and so on. |See the [ListSnapshots](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listsnapshots) API |
|Subtitle information |Includes subtitle tags, format, language, source, date created, and so on. |See `VodSubtitleInfo` in the [GetSubtitleInfoList](https://docs.byteplus.com/docs/byteplus-vod/reference-getsubtitleinfolist) API |


<span id="a56af2c1"></span>
### **DirectUrl mode**

Media asset information in DirectUrl mode includes the file path (FileName), file size, storage type, and last modification time. See `VodFileMetaInfos` in the [ListFileMetaInfosByFileNames](https://docs.byteplus.com/en/docs/byteplus-vod/listfilemetainfosbyfilenames) API.

<span id="c9b5a3f7"></span>
## **Updating basic media asset information**

BytePlus VOD supports updating a video's basic information, such as its cover, name, category, tags, and description. However, it does not support updating the metadata of a media asset, such as its format, size, and type.

<span id="006815aa"></span>
### **Using the console**


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vod/overview/) and enter a specific space.

2. On the **Videos** page, click the **Details** button in the **Actions** column of the target video to go to the **Video details** page.

3. On the **Basic information** tab, you can view and edit the video's basic information.

   * You can view the video cover, title, Vid, file path, publishing status, format, codec, resolution, duration, bitrate, size, dynamic range, creation time, category, tags, description, and storage type.

   * You can edit the title, category, tags, or description.


<span id="1c38a26f"></span>
### **Using the API or Server SDKs**

Call the [UpdateMediaInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-updatemediainfo)API to update basic media asset information, including the title, description, tags, category, cover image, and expiration time.
