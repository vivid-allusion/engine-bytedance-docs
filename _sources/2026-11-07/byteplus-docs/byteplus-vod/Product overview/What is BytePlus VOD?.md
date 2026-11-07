---
title: "What is BytePlus VOD?"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-what-is-byteplus-vod"
---

BytePlus Video on Demand (VOD) is an all\-in\-one service providing a complete solution for media upload, storage, processing, accelerated distribution, and playback.

Leveraging its robust infrastructure, you can quickly build a VOD streaming platform or application, allowing you to focus on your core business. The service also includes an advanced monitoring and alarm platform to help deliver an excellent audio\-visual experience for your users.

<span id="b741be48"></span>
## **Product architecture**

The following figure shows the end\-to\-end capabilities provided by BytePlus VOD, including media upload, management and processing, distribution, and playback.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d56215e48f0543ffbe5116e5d1f5f138~tplv-goo7wpa0wc-image.image) </span>

<span id="4abff9ec"></span>
## Features

<span id="bc8a0c3a"></span>
### Media upload

You can upload media files to BytePlus VOD using any of the following methods:


* The BytePlus VOD console

* The Upload SDKs for Android, iOS, and Web

* Open APIs


BytePlus VOD accepts input files in the following formats:


|**File type** |**Format** |
|---|---|
|Audio |MP3, M4A, WAV, WMA, AMR, AAC, OGG |
|Video |MP4, FLV, ASF (Advanced Systems Format, also known as WMV), RM, RMVB, MPEG, MOV, AVI, Flash, MPEG\-TS, M4S, M3U8, Matroska (MKV) |
|Image |PNG, JPG, JPEG, GIF, WebP |
|Subtitle |SRT, VTT, and ASS |
|Font |TTF, FON, and TTC |


<span id="96f2627f"></span>
### **Media storage**

With backup redundancy, remote disaster recovery, and resource isolation, BytePlus VOD provides high\-performance and reliable storage for large volumes of media assets.

<span id="8c303e67"></span>
### **Media management**

BytePlus VOD provides a console and OpenAPIs for managing media assets. You can perform the following operations on media assets:


* View and edit their information.

* Remove, download, and publish them.

* Generate cover images.

* Obtain access addresses of viewers.


<span id="5bcdfa68"></span>
### Media processing

Process BytePlus VOD files in one of the following ways:


* Audio and video standard transcoding: Transcode an audio or video file to one or more files with different encoding parameters to adapt to various network bandwidths, terminal processing capabilities, and user needs.

* Low\-bitrate HD transcoding: Analyze scenes, motion, content, and textures in videos, select appropriate encoding parameters, and output videos with better subjective quality at a low bit rate. This transcoding method reduces bandwidth costs while ensuring a good viewing experience.

* Adding watermarks and advertisements: Add brand logos and app names to videos or attach ads to the beginning or end of videos, protecting copyright and increasing brand exposure.

* Screenshot generation: Take screenshots, sampled screenshots, thumbnail screenshots, and image sprites for use as video covers and previews.


The supported formats for transcoding are as follows:


|Parameter |Type |Description |
|---|---|---|
|Input format |Container format |MP4, FLV, ASF, RM, RMVB, MPEG, MOV, AVI, Flash, MPEG\-TS, M4S, M3U8, Matroska, MP3, M4A, WAV, WMA, AMR, AAC, OGG |
||Video codec |AV1, AVS2, H.264/AVC, H.263, H.263+, H.265, MPEG\-1, MPEG\-2, MPEG\-4, MJPEG, VP8, VP9, Quicktime, RealVideo, Windows Media Video |
||Audio codec |AAC, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, Windows Media Audio, VORBIS |
|Output format |Container format |Video: MP4, HLS (M3U8 + TS), DASH, FLV, TS |
|||Audio: MP3, M4A, MP4, DASH, HLS, OGG |
|||Image: GIF, WEBP, PNG, JPEG, JPG |
||Video codec |H.264, H.265 |
||Audio codec |MP3, AAC, OPUS |


<span id="31cc7e0a"></span>
### Accelerated distribution

With access to BytePlus's worldwide Content Delivery Network (CDN) cache nodes, BytePlus VOD provides smooth and accelerated video content delivery to users around the world. You can add domain names for videos and images, which can redirect to BytePlus VOD origin servers or third\-party origin servers. For access control, BytePlus VOD supports configuring referer blocklists and allowlists, IP blocklists and allowlists, and URL authentication.

<span id="a23638ee"></span>
### Media playback

BytePlus VOD provides a cross\-platform suite of SDKs designed for seamless media playback. The Player SDK offers a rich set of features, ensuring a high\-quality and stable playback experience. The Player SDK features small package size and efficient memory usage. Its efficiently architected APIs make it straightforward to integrate into applications that play short\-form, feed, and long\-form videos. For details, see [Player SDK Overview](https://docs.byteplus.com/en/byteplus-vod/docs/player-sdk-overview).
