---
title: "Video Seeking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-video-seeking"
---

The video seeking feature on BytePlus CDN enhances the user viewing experience by allowing players to request specific video segments, such as when a user drags the progress bar, instead of downloading the entire file. This document explains how this feature works, its prerequisites, and provides the steps to enable it for your domain.

<span id="prerequisites"></span>
## Prerequisites


* The video file must be in MP4 format.

* The player specifies the requested video segment by using the `start` and `end` query parameters in the request URL. For example, the following request URL indicates that the player is requesting the video segment from the 15th second to the 120th second.

   * `http://www.example.com/4K_demo.mp4?start=15.000&end=120.000`


<span id="steps"></span>
## Steps


1. Open the **Video Seeking** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set the **Status** to **Enabled**.

3. After completing the configuration, click **Save**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66bfe1582d7b4dbe89dd3a1e9f499b8c~tplv-goo7wpa0wc-image.image) </span>

<span id="explanation-of-start-end-parameters-and-metadata-requirements-for-video-files"></span>
## ## Parameter and metadata requirements


|**Video Format** |**Metadata** |**start/end Parameters** |**Request URL Example** |
|---|---|---|---|
|MP4 |On the origin server, MP4 video files must contain metadata, and the metadata must appear at the beginning of the file. |Indicates the start and end times of the video in seconds, with millisecond precision. |`http://www.example.com/video.mp4?start=5.013&end=12.123` |



* The start and end parameter names are case\-sensitive. For example, if CDN receives a request URL `http://www.example.com/sample.mp4?Start=15`, due to the incorrect case of the `Start` parameter, CDN will return the complete `sample.mp4` instead of the specified video segment.

* If the frame specified by start or end is not a keyframe, CDN uses the nearest preceding keyframe as the actual start or end point.


<span id="more-information"></span>
## More Information

<span id="overview-of-video-seeking"></span>
### Overview of Video Seeking

Video seeking is a common feature supported by modern video players. During video playback, users can drag the progress bar in the player to change the playback position. When the user drags the progress bar to a certain position, the player will request a video segment from the server starting from that position, instead of requesting the entire video. This way, users do not need to wait for the entire video file to download while watching the video; they can start watching from the corresponding position as soon as the player obtains the video segment, providing a good user experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When a user first opens a video in the player, the player requests a video segment starting from the beginning of the video.</div>


* <div data-tips="true" data-tips-type="tip">During video playback, the player will request the next video segment from the server before the current video segment finishes playing.</div>



<span id="how-cdn-handles-video-segment-requests-from-the-player"></span>
### How CDN Handles Video Segment Requests from the Player

When your scenario meets the [Prerequisites](https://docs.byteplus.com/docs/byteplus-cdn/docs-video-seeking#prerequisites) and the video seeking feature is enabled, CDN extracts the requested video segment from the cached complete video file based on the `start` and `end` parameters in the request, and then returns it to the player. If the request itself is a Range request, CDN ignores the `Range` request header.

When CDN receives a video segment request from the player, if CDN has not yet cached the complete video file or the cached video file has expired, CDN will first request the complete video file from the origin server. Therefore, the player that sent the segment request will wait longer for a response from CDN. To avoid this issue, for popular videos, we recommend using the [prefetch](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-prefetch) feature to cache these video files on CDN nodes.

<span id="what-is-a-keyframe"></span>
### What is a Keyframe

Keyframes define the start and end points of a smooth transition in a video. For MP4 video files, their metadata specifies which video frames are keyframes.

<span id="additional-information"></span>
### Additional Information


* When CDN caches video files, the cache key of the file does not include the `start` or `end` parameters.

* When CDN requests the complete video file from the origin server, the back\-to\-origin request does not include the `start` or `end` parameters.
