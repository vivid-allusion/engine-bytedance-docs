---
title: "DASH and LL-DASH"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/dash-and-ll-dash"
---

In Dynamic Adaptive Streaming over HTTP (DASH) and Low\-Latency DASH (LL\-DASH), a live stream is sliced into Common Media Application Format (CMAF) segments. You can adjust the duration and segment number settings to effectively reduce latency and improve compatibility in live stream.

<span id="a77e62f0"></span>
## Limitation


* The DASH encapsulation is applicable for stream pushing, origin pull using HLS, FLV and Real\-Time Messaging Protocol (RTMP), and stream pulling using DASH over CMAF.

* The DASH encapsulation configuration applies to this domain name and other domain names within the same domain name space (Vhost).

* The encapsulation configuration takes effect in 3 minutes to 5 minutes.


<span id="5291f43e"></span>
## Prerequisite


* A player supporting DASH is required.

* iOS 10.0, macOS 10.12, and tvOS 10.0 or later OS versions support CMAF content.


<span id="1b226441"></span>
## Procedure


1. Go to [BytePlus MediaLive console > Domains](https://console.byteplus.com/live/main/domain/list).

2. Find the pull\-stream domain name that you want to check out, and click **Settings** in the **Actions** column.

3. Click the **Advanced settings** tab.

4. Click **Edit** in the DASH section to launch the dialog box and configure the following settings:

   * **CMAF** **Segment duration**: You can enter an integer from 1 to 60. We recommend that the group of pictures (GOP) size of the live stream is stable and that the segment duration is an integer multiple of the GOP size.

   * **Segment number**: The number of media segments included in a playlist. You can enter an integer from 3 to 10.

   * **Low latency DASH**: Low\-Latency DASH extends the protocol to enable low\-latency video streaming while maintaining scalability.
