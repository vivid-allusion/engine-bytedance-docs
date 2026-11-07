---
title: "Video seeking"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-seeking"
---

The video seeking feature allows viewers to jump to specific points in a video by dragging the player's progress bar, significantly improving the playback experience. This guide provides step\-by\-step instructions on how to enable this feature for your Playback, Image, and Custom\-origin domain names within the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Video seeking applies to <strong>Playback domain name</strong>, <strong>Image domain name</strong>, and <strong>Custom\-origin domain name</strong>.</div>


<span id="0fc1e76b"></span>
## Introduction

The video seeking feature is commonly used in video\-on\-demand scenarios. When the video is playing, the user controls the video's playback position by dragging the progress bar of the player. When the user drags the progress bar to a certain point in time, if the video content at that point in time is not cached locally, the video player will re\-initiate a video content request to the server, and specify the requested time range using the `start` and `end` parameters. For example, the video player sends the `http://www.example.com/video.mp4?start=15&end=120` request, which requests a video clip of 15 to 120 seconds.

When the user drags the progress bar, generally there is only the `start` parameter in the request, and there is no `end` parameter, which means that the requested video starts from the specified time and continues to the end of the video. However, in order to save bandwidth, some video service providers may only load data for a limited duration, such as 5 minutes when the user drags the progress bar. In this case, the start and end parameters will appear together.

<span id="99a37d24"></span>
### Support for video seeking

When your service uses a content distribution network (CDN), the cache nodes can directly respond to user seeking operations. The video file formats that currently support seeking are MP4 and FLV.

When the video player sends a video content request with `start` and `end` to the CDN, if the video file is not cached, the cache node will request the video file from the origin server and cache the file. The cache node then transmits the requested video segment to the user.

When caching this video file, the cache node will remove the `start` and `end` parameters. In this way, when other users request the video, even if they specify different `start` and `end` parameter values, they can hit the cache.

<span id="42a630e7"></span>
### What is a keyframe

A keyframe is a frame in a video that stores a complete image. A keyframe defines the starting point for a sequence of frames, and the frames that follow are calculated based on the changes from that keyframe.

<span id="4cd956d5"></span>
## Configuring video seeking


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Advanced configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Video seeking**, set **Status** to **Enabled**.

8. At the top right of the page, click **Save**.


<span id="9382ba3c"></span>
## Parameter description


* The `start` and `end` parameters are case sensitive. For example, the request is http://www.example.com/video.mp4?Start=15 . At this time, the `Start` parameter will not be recognized as a video seeking parameter.

* If there is no `start` parameter in the request, it means to start from the beginning of the video. If there is no `end` parameter, it means to get to the end of the video.

* The relevant parameters for MP4 and FLV file formats are explained as follows:



|**File format** |**Meta information** |**`start`** |**`end`** |**Request example** |
|---|---|---|---|---|
|MP4 |The metadata of the source video must be placed in the file header. Videos with metadata information at the end are not supported. |Indicates the start time of the video. The unit is seconds, accurate to milliseconds, that is, 3 decimal places. If the time point represented by the `start` parameter is not a keyframe, playback starts from the keyframe immediately preceding the specified time. |Indicates the end time of the video. The unit is seconds, accurate to milliseconds, that is, 3 decimal places. If the time point represented by the `end` parameter is not a keyframe, the segment ends at the keyframe immediately preceding the specified time. |http://www.example.com/video.mp4?start=5.013<br><br>This example starts playback at 5.013 seconds. |
|FLV |The source video must have metadata information. |Specifies the starting byte offset of the video. If the specified byte offset is not a keyframe, playback starts from the keyframe immediately preceding that offset. |Specifies the ending byte offset of the video. If the specified byte offset is not a keyframe, the segment ends at the keyframe immediately preceding that offset. |http://www.example.com/video.flv?start=5<br><br>This example means to start playing from the 5th byte. |
