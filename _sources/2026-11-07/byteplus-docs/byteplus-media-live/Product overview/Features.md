---
title: "Features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-features"
---

BytePlus MediaLive is a comprehensive live streaming platform that provides stable and feature\-rich services. This topic outlines its core capabilities, including stream pushing and pulling, domain management, live transcoding, recording, and time\-shifting, helping you build professional live streaming applications.

<span id="Stream pushing"></span>
## Stream pushing


|**Feature** |**Description** |
|---|---|
|Protocol |RTMP, RTMPS, RTM, and SRT. |
|Method |Use the BytePlus MediaLive Broadcast SDK for Web, or common third\-party streaming software such as OBS, XSplit, and FMLE. |
|Device |Common RTMP\-streaming hardware. |


<span id="Stream pulling"></span>
## Stream pulling


|**Feature** |**Description** |
|---|---|
|Protocol |RTMP, RTMPS, FLV, RTM, HLS, LL\-HLS, and LL\-DASH. |
|Method |Use the BytePlus MediaLive Player SDK for iOS, Android, React Native, Flutter, and Web, or common third\-party players that support FLV, RTMP, and HLS. |
|Play control |Applicable to the original or live\-transcoded stream. |


<span id="Domain management"></span>
## Domain management


|**Feature** |**Description** |
|---|---|
|Basic configurations |* Add and delete domain names.<br><br>* Query domain name list and information.<br><br>* Enable and disable domain names.<br><br>* Associate and disassociate a domain name for stream pushing with a domain name for stream pulling. |
|HTTPS configuration |Configure HTTPS secure acceleration using an HTTPS certificate, which you can then associate with a domain name. |
|Access control |* Configure a custom authentication key, which BytePlus MediaLive uses to authenticate push and pull stream URLs.<br><br>* Configure a referer blocklist or allowlist to prevent referer spam.<br><br>* Configure an IP blocklist or allowlist to restrict access to domain names. |
|Callback management |Configure callback addresses. BytePlus MediaLive sends callbacks to the addresses when stream pushing starts or ends. |


<span id="Live management"></span>
## Live management


|**Feature** |**Description** |
|---|---|
|Stream management |* Disable, enable, and disconnect a stream.<br><br>* Query live streams and ended streams.<br><br>* Query disabled streams and stream status. |
|Screenshot management |Display information about screenshots taken during a live stream, including their file names and storage paths. |
|Recording management |Display information about live stream recordings, including their file names and storage paths. |


<span id="Value-added services"></span>
## Value\-added services


|**Feature** |**Description** |
|---|---|
|Live transcoding |Transcode streams into different resolutions, bitrates, frame rates, and video codecs (H.264 and H.265). Low\-bitrate HD is also supported, which produces high\-quality videos with lower bitrates and less bandwidth consumption. |
|Recording |Record a live stream and save the recording to your storage space. |
|Screenshot capturing |Automatically capture screenshots from your live stream and save them to your storage space. |
|Relay |Pull content from a third\-party video source or an on\-demand video (VoD) and relay it to BytePlus MediaLive viewers. |
|Origin pulling |Pull live streams from third\-party content delivery networks (CDNs). |
|Time\-shifting |Allow your viewers to replay any streamed content. |
|Live\-stream watermark |Watermark your live streams to prevent unauthorized use of your content. |


<span id="Statistics"></span>
## Statistics


|**Feature** |**Description** |
|---|---|
|Usage |Query usage data for bandwidth, traffic, transcoding, and screenshots. |
|Stream |Query push\-stream information, including bitrate and frame rate. |
|Viewing |View data about online viewer counts and client\-side requests. |


<span id="Others"></span>
## Others


|**Feature** |**Description** |
|---|---|
|Log management |Query and filter log files. |
|Address generator |Generate push and pull stream addresses. This feature is available only on the console. |
