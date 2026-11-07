---
title: "Limits"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-limits"
---

BytePlus Video on Demand (VOD) features operate within a specific set of limits and rules. This document details these constraints, covering quota limits, API call frequency (QPS), and transcoding specifications, to help you effectively plan your application's architecture and resource usage.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This article contains important information that may affect your business. Please read it carefully.</div>


* <div data-tips="true" data-tips-type="warning">If your business needs require higher limits, contact the BytePlus support team by <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112">creating a ticket</a>, and provide details about your use case and the requested limits.</div>



<span id="0e87e542"></span>
## Quota limits


|Feature |Resource type |Restriction |
|---|---|---|
|Space management |Region of use |For new users, only the **Asia Pacific (Johor)**  region is currently supported. |
||Number of spaces |A single account can create up to 20 spaces. |
|Media asset uploads |File size for console uploads |* Non\-materials: A single video cannot exceed 20 GB.<br><br>* Materials: A single video cannot exceed 500 MB; other materials cannot exceed 50 MB. |
||Concurrent URL pulls |A single account can pull up to 20 audio and video files concurrently. |
||URL pull speed |No more than 10 Gbps. |
|Media asset management |Maximum categories |* Up to three categories can be added.<br><br>* Up to 100 subcategories can be created under each category. |
||Number of tags |Up to 16 tags can be added to a single video. |
|Media processing |Input file size for media processing |A single file cannot exceed 100 GB. |
||Number of concurrent processing tasks |Up to 100 concurrent processing tasks can be configured. This limit can vary depending on the use case and your service plan. |
||Number of workflows |Up to 100 workflows can be created in a single space. |
||Number of media processing templates |Up to 100 media processing templates can be created in a single space. |
||Number of watermarks associated with a template |Up to 20 watermarks can be configured for a single watermark and ad insertion template. |
|Video distribution |Number of domain names |Up to 200 for a single account. |
||IP blocklist and allowlist entries |Up to 1000 for a single domain name. |
||Number of domain names and IPs configured in the referrer blocklist and allowlist |Up to 1000 for a single domain name. |
||Number of refreshed URLs per day |Up to 1000 URLs can be refreshed per day. |
||Number of directories refreshed per day |Up to 50 directories can be refreshed per day. |
||Number of warm\-up URLs per day |Up to 1000 warm\-up URLs per day. |
|Event callback |Number of event callback subscription addresses |You can add up to 10 callback subscription addresses for a single space. |


<span id="efd556d3"></span>
## API QPS limits

BytePlus VOD limits the call frequency for each API, measured as queries per second (QPS). If a user exceeds the QPS limit, rate limiting is implemented.

For more information, see [QPS limits on API calls](https://docs.byteplus.com/en/docs/byteplus-vod/reference-qps-limits-on-api-calls).

<span id="01664e42"></span>
## **ICP filing for accelerated domain names**

To access BytePlus VOD CDN services and accelerate a domain name, you must determine whether you need to complete ICP filing based on the acceleration region. When you add a domain name, if the selected acceleration region is **the Chinese mainland** or **Global**, then the domain name must be filed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Regardless of your source site's location, if you use BytePlus VOD CDN for content distribution in the Chinese mainland, the domain name used for content delivery must have an ICP filing.</div>


<span id="ffada564"></span>
## Audio and video transcoding restrictions


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Input file |Container format |MP4, FLV, ASF, RM, RMVB, MPEG, MOV, AVI, Flash, MPEG\-TS, M4S, M3U8, Matroska, MP3, M4A, WAV, WMA, AMR, AAC, OGG |
||Video codec |AV1, AVS2, H.264/AVC, H.263, H.263+, H.265, MPEG\-1, MPEG\-2, MPEG\-4, MJPEG, VP8, VP9, Quicktime, RealVideo, Windows Media Video |
||Audio codec |AAC, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, Windows Media Audio, VORBIS |
||File size |A single file cannot exceed 100 GB. |
|Output file |Container format |* Video: MP4, HLS (M3U8 + TS), DASH, FLV, TS<br><br>* Audio: MP3, M4A, MP4, DASH, HLS, OGG<br><br>* Images: GIF, WEBP, PNG, JPEG, JPG |
||Video codec |H.264, H.265 |
||Audio codec |MP3, AAC, OPUS |
||Bitrate |For H.264, the output bitrate range is [10,50000] Kbps. |
||Frame rate |The output frame rate range is [1,60] fps. |
|Transmuxing (original resolution) |N/A |Only MP4, DASH, and HLS are supported. |
