---
title: "Resource packs"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-resource-packs"
---

BytePlus MediaLive provides pre\-paid resource packs for live\-stream traffic and transcoding durations. This article outlines their pricing and billing details.


|**Resource Pack** |**Description** |
|---|---|
|Live\-stream traffic pack |Used to deduct both upstream and downstream live\-stream traffic, including standard and RTM streaming. |
|Transcoding duration pack |Used to deduct transcoding duration (including standard transcoding and low\-bitrate HD transcoding). |



* The validity period of resource packs is 12 months. Unused resources expire when the resource pack does.

* Traffic or transcoding duration consumed is first deducted from your resource packs. Any usage exceeding the resource pack limits will be charged at [live-streaming service fees](https://docs.byteplus.com/byteplus-media-live/docs/live-streaming-service-fees) and [transcoding fees](https://docs.byteplus.com/byteplus-media-live/docs/transcoding).

* Resource packs can be used on top of one another. For example, if you purchase two 100 GB resource packs, you can use them to deduct a total of 200 GB of traffic. The deduction follows the order of their purchase.

* The BytePlus MediaLive resource packs can only be used to deduct traffic or duration consumed when using BytePlus MediaLive's service.

* A resource pack takes effect on the day of purchase, but it cannot be used to deduct any traffic or duration that occurred during a previous billing cycle.

* You can apply for a refund for a resource plan within seven days after purchase if it has not been used. You cannot apply for a refund seven days or more after purchase or if the resource pack has been used in full or part.


<span id="Live-stream traffic packs"></span>
## Live\-stream traffic packs


* The packs are effective when you are billed by traffic. If you choose to be billed by bandwidth, the resource pack will be frozen.

* Each region is assigned a deduction factor that is multiplied by the actual traffic when calculating the traffic to deduct. For example, if you use 10 GB of traffic in the Asia Pacific 2 region, the traffic deducted from your resource pack is calculated as: 10 GB × 1.3 (the deduction factor for Asia Pacific 2), resulting in a deduction of 13 GB. Refer to [Deduction factor](https://docs.byteplus.com/docs/byteplus-media-live/docs-resource-packs#b853e26f) for the deduction factor of each region.

* The deduction factor for downstream traffic in [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media) streaming differs from that of standard streaming.


<span id="c15c3c59"></span>
### Pricing

> The conversion factor for units of traffic is 1,000. For example, 1 GB = 1,000 MB.



|**Traffic pack** |**Unit price (USD)**  |
|---|---|
|100 GB |7 |
|500 GB |33 |
|1 TB |63 |
|10 TB |599 |
|100 TB |5026 |
|1 PB |43700 |


<span id="b853e26f"></span>
### Deduction factors


|**Region** |**Deduction factor for standard streaming** |**Deduction factor for RTM stream pulling** |
|---|---|---|
|The Chinese mainland |0.4928 |0.9855 |
|Asia Pacific 1 |1 |2 |
|Asia Pacific 2 |1.3 |2.6 |
|Asia Pacific 3 |1.4667 |2.9333 |
|North America |0.7333 |1.4667 |
|Europe |0.7333 |1.4667 |
|Middle East |1.6667 |3.3333 |
|South America |1.6667 |3.3333 |


<span id="Transcoding duration packs"></span>
## Transcoding duration packs

<span id="Pricing (unit: USD)"></span>
### Pricing


|**Transcoding resource pack** |**Price (USD)**  |
|---|---|
|1,000 h |154 |
|10,000 h |1463 |


The duration in the packs is for **standard transcoding,**  **H.264**, **480p resolution**. The duration for other codec, resolution, and transcoding type combinations for the same price varies according to the following tables.

**Standard Transcoding**


|**Codec** |**Resolution** |**Duration (hours)**  ||
|---|---|---|---|
|||**1,000** |**10,000** |
|H.264 |480p and below (including 480P) |1,000 |10,000 |
||480–720p (including 720P) |515.1515152 |5,151.515152 |
||720–1080p (including 1080P) |261.5384615 |2,615.384615 |
||1080p – 2K (including 2K) |125 |1,250 |
||2–4K (including 4K) |62.5 |625 |
|H.265 |480p and below (including 480P) |200 |2,000 |
||480–720p (including 720p) |100 |1,000 |
||720–1080p (including 1080p) |50 |500 |
||1080p – 2K (including 2K) |25 |250 |
||2–4K (including 4K) |12.5 |125 |


**Low\-bitrate HD transcoding**


|**Codec** |**Resolution** |**Duration (hours)**  ||
|---|---|---|---|
|||**1,000** |**10,000** |
|H.264 |480p and below (including 480P) |251.8518519 |2,518.518519 |
||480–720p (including 720p) |127.8195489 |1,278.195489 |
||720–1080p (including 1080p) |63.90977444 |639.0977444 |
||1080p – 2K (including 2K) |31.48148148 |314.8148148 |
||2–4K (including 4K) |15.74074074 |157.4074074 |
|H.265 |480p and below (including 480p) |100 |1,000 |
||480–720p (including 720p) |50 |500 |
||720–1080p (including 1080p) |25 |250 |
||1080p – 2K (including 2K) |12.5 |125 |
||2–4K (including 4K) |6.25 |62.5 |
