---
title: "Overview "
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-asset-management"
---

Media asset management in BytePlus VOD is a suite of features that helps you organize, retrieve, and process your media files. This document introduces the core capabilities of media asset management and explains the two distinct management modes: the standard Vid mode for lifecycle management and the DirectUrl mode for object\-storage\-style operations, helping you choose the best approach for your needs.

## Applicable scenarios

* Manage the complete metadata of multiple types of media assets such as videos and images and reduce the cost of maintaining a large amount of media content.

* Use multiple methods to get media asset information, such as searching by name, tag, and vid.

* Create diversified content by transcoding and processing existing media assets.

* For audio and video files, you can generate playback addresses to facilitate subsequent sharing and distribution.

## Image asset management

Image assets use a unique picture ID (`Pid`) to associate the original image with its processed files. Use **Pid mode** to search images, edit their metadata, and submit processing tasks. Use **DirectUrl mode** to browse stored files by path. For instructions, see [Managing image assets](https://docs.byteplus.com/docs/byteplus-vod/docs-image-asset-management).

## Vid mode and DirectUrl mode

For audio and video assets, BytePlus VOD supports two media asset management modes: Vid and DirectUrl.

### Vid mode

Vid mode is the standard mode of BytePlus VOD. By default, after you upload an audio/video resource to BytePlus VOD, the service automatically generates a Vid for media asset lifecycle management or media processing. A Vid is the unique identifier for a source video and all its transcoded products, which can have different resolutions, codec formats, and container formats. You can use the Vid as an index to find or manage videos. When triggering a media processing workflow, you need to use the Vid as an input parameter to locate the video for processing, and use the Vid to request playback information from the BytePlus VOD server.

### DirectUrl mode

For users who are familiar with standard object storage, BytePlus VOD also provides a DirectUrl mode, which uses the file path FileName to connect various functional modules. FileName is the unique identifier of a media asset in the VOD bucket. The space name and file path determine a unique object. For example, if the storage location of the `video.mp4` file is `{BucketName}/Project/VideoFiles/video.mp4`, the file path is `Project/VideoFiles/video.mp4`. The format of the file path is: `FilePrefix/FileTitle.FileExtension`. The details are as follows:

* **FilePrefix**: The full path before the media asset file name, which does not include the bucket name. The console represents it as multiple nested folders. If you save the `video.mp4` file in a bucket with no specified path, the file prefix is `/`.

* **FileTitle**: The name of the media asset file without the extension. For the `video.mp4` file, the FileTitle is `video`.

* **FileExtension**: A mechanism that BytePlus VOD uses to identify the file format. For the `video.mp4` file, the FileExtension is `mp4`, which means that this file is a video file in MP4 format. A period `.` separates the file name from the file extension.

> **Warning**

> DirectUrl mode is currently available only in the Asia Pacific (Johor) region. To enable this feature, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) to contact the BytePlus support team.

### Feature comparison

The following table compares the main features of Vid mode and DirectUrl mode.

|**Stage** |**Comparison Item** |**Vid Mode** |**DirectUrl Mode** |
|---|---|---|---|
|**Media asset upload** |Upload parameters |When obtaining the upload address and credentials, you only need to pass in the basic information of the media resource, such as the target space name and file type. |When obtaining the upload address and credentials, in addition to the basic information, you also need to pass in the FileName. |
||Server\-side processing |The VOD service automatically generates a random 32\-bit string as the Vid. |The VOD service stores the user\-entered FileName. |
||Upload result |The returned parameters include the Vid. |The returned parameters include the FileName. |
||Storage location |The VOD service automatically generates the storage location, names it after the Vid, and stores it in a fixed location in the bucket. |Supports custom settings. The service stores media resources in the corresponding folder according to the prefix and file name in the FileName. |
|**Media asset management** |List index |Vid |FileName |
||Retrieval |Retrieve by Vid. |Retrieve by file prefix. |
||Directory structure |Not supported. You need to use the [Categories](https://docs.byteplus.com/docs/byteplus-vod/docs-system#e83439dc) for classification. |Supported. You can directly perform classification management through the directory structure. |
|**Media processing** |Trigger processing |Locate the media resource for processing through the Vid. |Locate the media resource for processing through the space name and file path. |
||Storage after processing |The processing outputs have the same Vid as the source file. |Supports custom file path rules for the processing outputs, and stores them according to the specified path. |
|**CDN distribution and acceleration** |Get playback address |You must obtain playback information from the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) API. |* Obtain from the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) API.<br><br>* [Manually constructing the URL](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-playback-addresses#50f0387f) |
|**Audio and video playback** |Playback method |Use the BytePlus VOD player SDK for playback. |Use a URL for playback by setting the playback address (generated by the VOD service or a third party) as the playback source. |
|**Event notification** |Get identifier |Get the Vid from the notification. |Get the FileName from the notification. |

## Features

The specific media asset management features provided by BytePlus VOD are as shown in the following table.

|**Feature** |**Description** |**Documentation** |
|---|---|---|
|Get media asset information |Get the basic information of a media asset using the media asset ID. Call different APIs for different types of media assets. |* [GetMediaList](https://docs.byteplus.com/docs/byteplus-vod/reference-getmedialist)<br><br>* [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo)<br><br>* [ListSnapshots](https://docs.byteplus.com/docs/byteplus-vod/reference-listsnapshots)<br><br>* [GetSubtitleInfoList](https://docs.byteplus.com/docs/byteplus-vod/reference-getsubtitleinfolist) |
|Update media asset information |* Update audio and video titles, descriptions, categories, and tags.<br><br>* Set the video cover image.<br><br>* Modify the audio and video publishing status.<br><br>* Modify the media asset storage type. |None |
|Delete media files |Delete media files at different granularities. BytePlus VOD allows you to delete various types of media files produced by VOD, including original audio and video files uploaded to VOD, files output by media processing, video snapshot files, uploaded image files, and so on. |[Deleting media files](https://docs.byteplus.com/docs/byteplus-vod/docs-deleting-media-files) |
