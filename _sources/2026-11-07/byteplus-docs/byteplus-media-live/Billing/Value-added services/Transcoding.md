---
title: "Transcoding"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding"
---

BytePlus MediaLive offers several transcoding services to adapt your media for various playback scenarios. This topic details the pricing for standard, low\-bitrate HD, video enhancement, and audio\-only transcoding. It explains how fees are calculated based on transcoding duration, resolution, and codec, allowing you to accurately estimate your usage costs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can use resource packs to offset transcoding duration (both standard and low\-bitrate HD transcoding) consumed after their purchase. For details, refer to <a href="https://docs.byteplus.com/byteplus-media-live/docs/resource-packs">Resource packs</a>.</div>


* <div data-tips="true" data-tips-type="tip">If you need to enable video enhancement for transcoding, please <a href="https://console.byteplus.com/workorder/create">contact technical support</a>.</div>


* <div data-tips="true" data-tips-type="tip">Enabling watermarking may also incur transcoding fees.</div>



<span id="Pricing (unit: USD/minute)"></span>
## Pricing (unit: USD/minute)

The unit price is determined by a combination of the resolution tier and codec of the transcoded stream and whether you use standard or low\-bitrate HD transcoding.

To determine the resolution tier, multiply the video's width by its height. The tiers are defined as follows:


|**Tier** |**Calculation** |
|---|---|
|480p |length × width ≤ 640×480 |
|720P |length × width ≤ 1280×720 |
|1080p |length × width ≤ 1936×1088 |
|2K |length × width ≤ 2560×1440 |
|4K |length × width ≤ 4096×2160 |


For example, a transcoding template with a resolution of 960×540p (960×540 = 518,400 pixels) falls into the 720p tier, since the resolution is higher than the 480p tier (640×480 = 307,200 pixels) and lower than the 720p tier (1280×720 = 921,600 pixels).

<span id="Standard transcoding"></span>
### Standard transcoding


|**Resolution** |**H.264** |**H.265** |
|---|---|---|
|Up to 480p |0.0027 |0.0134 |
|Over 480p to 720p |0.0054 |0.0261 |
|Over 720p to 1080p |0.0105 |0.0522 |
|Over 1080p to 2K |0.0228 |0.1124 |
|Over 2K to 4k |0.0466 |0.2248 |


**Billing example**

On November 1, User A performed two transcoding tasks using standard transcoding, both in H.264 format. Transcoding Task A had a resolution of 480p and lasted for 1 hour, while Transcoding Task B had a resolution of 720p and lasted for 30 minutes. The standard transcoding fees for November 1 are as follows:


* **Fee for Transcoding Task A** = 0.0027 USD/minute × 60 minutes = 0.162 USD

* **Fee for Transcoding Task B** = 0.0054 USD/minute × 30 minutes = 0.162 USD


Therefore, the total transcoding fee for November 1 is **0.324 USD**, which is charged the next day.

<span id="Low-bitrate HD transcoding"></span>
### Low\-bitrate HD transcoding


|**Resolution** |**H.264** |**H.265** |
|---|---|---|
|Up to 480p |0.011 |0.0332 |
|Over 480p to 720p |0.0211 |0.0632 |
|Over 720p to 1080p |0.0421 |0.1263 |
|Over 1080p to 2K |0.0842 |0.2526 |
|Over 2K to 4k |0.1683 |0.5051 |


**Billing example**

On November 2, User A performed two transcoding tasks using low\-bitrate HD transcoding with both tasks in H.265 format. Transcoding Task A had a resolution of 720p and lasted for 50 minutes, while Transcoding Task B had a resolution of 1080p and lasted for 40 minutes. The Low\-bitrate HD transcoding fees for November 2 are as follows:


* **Fee for Transcoding Task A** = 0.0632 USD/minute × 50 minutes = 3.16 USD

* **Fee for Transcoding Task B** = 0.1263 USD/minute × 40 minutes = 5.052 USD


Therefore, the total transcoding fee for November 2 is **8.212 USD**, which is charged the next day.

<span id="aab33600"></span>
### Video enhancement transcoding


|**Resolution** |**H.264 and H.265** |
|---|---|
|Up to 480p |0.14 |
|Over 480p to 720p |0.27 |
|Over 720p to 1080p |0.53 |
|Over 1080p to 2K |1.14 |
|Over 2K to 4k |2.33 |


**Billing example**

On November 3, User A performed two transcoding tasks using video enhancement transcoding. Transcoding Task A had a resolution of 480p and lasted for 20 minutes, while Transcoding Task B had a resolution of 1080p and lasted for 10 minutes. The Video enhancement transcoding fees for November 3 are as follows:


* **Fee for Transcoding Task A** = 0.14 USD/minute × 20 minutes = 2.8 USD

* **Fee for Transcoding Task B** = 0.53 USD/minute × 10 minutes = 5.3 USD


Therefore, the total transcoding fee for November 3 is **8.1 USD**, which is charged the next day.

<span id="Audio transcoding"></span>
### Audio\-only transcoding

Audio\-only transcoding means that only the audio in a live stream is transcoded, while the video remains unchanged. For example, if the audio codec is converted from AAC to Opus while the video codec, resolution, and other video settings remain unchanged, audio\-only transcoding fees apply.

The price of audio transcoding is 0.0009 USD/minute.

**Billing example**

On November 1, User A used audio\-only transcoding for 20 hours. The audio transcoding fee for November 1 is **1.08 USD** (0.0009 USD/minute × 1200 minutes). This amount will be charged on the following day.

<span id="Billing cycle"></span>
## Billing cycle

Transcoding supports both daily and monthly pay\-as\-you\-go.
