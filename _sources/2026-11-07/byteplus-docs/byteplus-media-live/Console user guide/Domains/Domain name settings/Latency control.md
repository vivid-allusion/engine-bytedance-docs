---
title: "Latency control"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/latency-control"
---

To reduce live streaming latency for stream pulling over FLV and RTMP, you can configure the server's GOP cache. This topic describes how GOP cache works and guides you through configuring it in the BytePlus MediaLive console.

The GOP cache is a buffer on the edge server that temporarily stores video data, configured in millseconds. Adjusting the cache size allows you to balance between lower latency and better resilience against network fluctuations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">GOP stands for Group of Pictures. It represents a group of consecutive frames in a video stream that are interrelated and allow for efficient compression. A GOP consists of Intra\-coded frames (I\-frame), Predictive\-coded frames (P\-frame), and Bidirectional\-coded frames (B\-frame).</div>


In the server cache, GOPs are discarded based on the First\-In, First\-Out (FIFO) rule. The oldest GOP is discarded when the cache reaches the specified GOP cache size.

<span id="207a290e"></span>
## Procedure


1. Go to [BytePlus MediaLive console > Domains](https://console.byteplus.com/live/main/domain/list).

2. Find the pull streaming domain name that you want to review, and click **Settings** in the **Actions** column.

3. Click the **Advanced settings** tab.

4. Click **Edit** in the **GOP cache** section to open the dialog box.

   Though a larger cache size increases latency, it provides better resilience to network fluctuations or temporary disruptions, as more frames are available for playback on the edge server. The appropriate caching duration depends on several factors, including streaming protocols, desired latency, error resilience, and length of a GOP.

   You can enter a number from 500 to 20,000 to specify the cache size.
