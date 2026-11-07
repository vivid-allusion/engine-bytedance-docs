---
title: "HLS and LL-HLS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/hls-and-ll-hsl"
---

In HTTP Live Streaming (HLS) and Low\-Latency HLS (LL\-HLS), a live stream is sliced into Transport Stream (TS). The corresponding URIs of these segments in the M3U8 playlist are constantly updated. You can adjust the segment duration and segment number to effectively reduce the latency and improve compatibility in live streaming.

<span id="a77e62f0"></span>
## Limitations


* The HLS/LL\-HLS encapsulation is applicable for stream pushing, origin pull using FLV and Real\-Time Messaging Protocol (RTMP), and stream pulling using HLS. Note that it does not apply to origin pull using HLS.

* The HLS/LL\-HLS encapsulation configuration will apply not only to streams under this domain name but also to streams under other domain names associated with the same domain name space (Vhost).

* The HLS/LL\-HLS encapsulation configuration will not apply to the application which enables the [HLS-ABR](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) feature.

* The encapsulation configuration takes effect in 3 minutes to 5 minutes.


<span id="5291f43e"></span>
## Prerequisites


* A player supporting LL\-HLS is required.


<span id="1b226441"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Find the pull\-stream domain name that you want to check out, and click **Settings** in the **Actions** column.

4. Click the **Advanced settings** tab.

5. Click **Edit** in the HLS/ LL\-HLS section to launch the dialog box and configure the following settings:

   * **Segment duration**: You can enter an integer from 1 to 60. We recommend that the group of pictures (GOP) size of the live stream is stable and that the segment duration is equal to or a multiple of the GOP size.

   * **Segment number**: The number of media segments included in a playlist. You can enter an integer from 2 to 10.

   * **Segment number in the initial playlist**:

      Minimizing the duration of the initial requested segments can speed up the initial video playback.

   * **Low latency HLS**: Low\-Latency HLS extends the protocol to enable low\-latency video streaming while maintaining scalability. The feature is disabled by default.

   * **Partial segment duration**:

      Low\-Latency HLS divides each media segment into a larger number of smaller files. These smaller files are called Partial Segments. While regular media segments might be 6 seconds each, an example Partial Segment might be only 200 milliseconds.

   * **Insert PDT**: Whether to insert the PDT(#EXT\-X\-PROGRAM\-DATE\-TIME) time tag in the playback file.

   * **PDT Interval**: If the PDT insertion is enabled, the interval time for inserting PDT needs to be set in seconds, ranging from 0 to 3600.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the PDT interval is set to 0 or a value less than the segment duration, a PDT tag will be inserted for each segment.      </div>
