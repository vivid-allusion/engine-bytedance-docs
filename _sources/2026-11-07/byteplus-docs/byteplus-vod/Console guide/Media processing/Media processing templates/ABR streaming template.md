---
title: "ABR streaming template"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-abr-streaming-template"
---

To optimize video delivery for various devices and network conditions, you can create an ABR streaming template in the BytePlus VOD console. This guide provides step\-by\-step instructions for creating and configuring the template, and details all available video and audio parameters to help you customize the output.

<span id="c133bbef"></span>
## Creating an ABR streaming template


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media processing** \> **Templates** on the left navigation bar.

5. Switch to the **ABR streaming** tab.

6. Click **Create ABR streaming template**.

7. In the dialog box that appears, configure the basic information, audio transcoding parameters, and video transcoding parameters according to your specific business requirements. For details, see the following documentation:

   * [Basic information](https://docs.byteplus.com/docs/byteplus-vod/docs-abr-streaming-template#a6276a7a)

   * [Sub-stream configuration](https://docs.byteplus.com/docs/byteplus-vod/docs-abr-streaming-template#b39bc2d5)

8. Click **Save**.


<span id="f7595f27"></span>
## Parameters

<span id="a6276a7a"></span>
### Basic information


|**Parameter** |**Description** |
|---|---|
|Template name |The length of the template name cannot exceed 64 characters. We recommend using a name that clearly identifies the template's purpose. |
|Template description |The length of the template description cannot exceed 140 characters. |
|Transcoding mode |This parameter offers the following options:<br><br><br>* **Standard transcoding**: This mode transcodes video files by modifying the video codec, container, resolution, and bit rate to suit various business scenarios, devices, and network environments.<br><br>* **Low\-bitrate HD**: This mode selects the optimal encoding parameters to output videos with better subjective quality at a relatively lower bitrate. This not only reduces bandwidth costs but also provides an enhanced visual experience. |
|||
|||
|||
|Output format |This parameter offers the following options:<br><br><br>* DASH<br><br>* HLS |
|Container format |This parameter only appears when the output format is HLS and offers the following options:<br><br><br>* TS (MPEG Transport Stream)<br><br>* FMP4 (Fragmented MP4) |
|Encryption method |BytePlus supports the following encryption methods:<br><br><br>* **HLS standard encryption**: For details, see [HLS standard encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-standard-encryption).<br><br>* **Private encryption**: For details, see [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption).<br><br>* **DRM encryption**: For details, see [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption). |
|DRM type |Select the DRM type you want to enable. BytePlus VOD supports Google Widevine, Apple FairPlay, and Microsoft PlayReady DRM encryption. For a detailed overview of DRM encryption, please refer to [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption). |


<span id="b39bc2d5"></span>
### Sub\-stream configuration

<span id="c1315544"></span>
#### Video parameters

Define how the video stream will be processed.


|**Parameter** |**Description** |
|---|---|
|Resolution |This parameter offers the following options:<br><br><br>* 240p<br><br>* 360p<br><br>* (Default) 480p<br><br>* 540p<br><br>* 720p<br><br>* 1080p<br><br>* 2k<br><br>* 4k<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend using 360p, 480p, and 720p for most business scenarios, devices, and network environments. If the user's bandwidth is limited or video deduplication is necessary, we suggest using 240p or 360p.</div><br> |
|Custom resolution |Customize the resolution of the output video using the following two methods.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The available range for custom resolution values depends on the standard resolution you have selected.</div><br><br><br><br>* **Based on long and short sides**: The VOD service will automatically identify the longer and shorter sides during transcoding.<br><br>   * If both long and short sides are empty, the default resolution will be used.<br><br>   * If one side is empty, the other side will be scaled proportionally to the original video.<br><br>   * If both long and short sides are not empty, the video will be output according to the configured long and short sides.<br><br>* **Based on width and height**:<br><br>   * If both width and height are empty, the default resolution will be used.<br><br>   * If one side is empty, the other side will be scaled proportionally to the original video.<br><br>   * If both width and height are not empty, the video will be output according to the configured width and height. |
|Video scaling method |This parameter controls how the video is scaled to fit the target output resolution.<br><br><br>* **Maintain the original video's aspect ratio**: Scale the video to fill the target dimensions while maintaining the original aspect ratio. This process may crop parts of the video that extend beyond the target dimensions.<br><br>* **Adaptive stretching**: Stretch the video to fit the target output resolution, regardless of the original aspect ratio. This can distort the original video, potentially creating a stretched or squeezed appearance.<br><br>* **Adaptive scaling plus black edge**: Scale the video to fit the smaller dimension of the target output resolution, maintaining the original aspect ratio. If the other dimension doesn't match, black edges are added to fill the remaining space. |
|Video codec |This parameter offers the following options:<br><br><br>* (Default) H.264<br><br>* H.265 |
|CRF value |Constant Rate Factor (CRF) is an encoding mode that adjusts the file data rate up or down to achieve a selected quality level rather than a specific data rate. CRF values range from 0 to 51, with lower numbers delivering higher quality scores. The default value is 25 and we recommend you set a value between 23 and 27. |
|Maximum bitrate |The value for the maximum bit rate can range from 10 to 50,000. |
|Frame rate |This parameter offers the following options:<br><br><br>* **Same as input**: The value for the maximum frame rate can range from 1 to 60. If the input video's frame rate does not exceed the specified maximum, the output frame rate will match the input. Otherwise, the output frame rate will be capped at the specified maximum.<br><br>* **Fixed frame rate**: The value for the fixed frame rate can range from 1 to 60. |
|Dynamic range |When processing HDR video, the dynamic range of the output video can be:<br><br><br>* **Map HDR to SDR**: By using an algorithm that maps HDR to SDR, you can preserve the video's color richness as much as possible and achieve better playback compatibility.<br><br>* **Maintain HDR**. |


<span id="2f07fc5a"></span>
#### Audio parameters

Define how the audio stream will be processed. The available options depend on the **Output format** and **Container format** you selected in the **Basic information** section.


* If you have selected `HLS` as the output format and `FMP4` or `TS` as the container format, you have the option to configure multiple audio tracks.

   1. Decide if your output video will contain one or multiple audio tracks by selecting **Track mode**:

      * **Single audio track:**  (Default) The output video will have one standard audio track.

      * **Multiple audio tracks:**  This mode is designed for source videos that already contain multiple audio tracks. It allows you to extract these tracks and apply specific transcoding configurations to each. The output video will contain multiple audio tracks that viewers can switch between.

   2. Configure audio parameters:

      * If you selected **Single audio track**: Configure the parameters directly using the **Audio parameter** table below.

      * If you selected **Multiple audio tracks**: Proceed to the **Multiple audio tracks** section further down to choose your strategy.

* If you have selected any other output format (such as `DASH`), only a **single audio track** is supported. Configure the parameters for the single output audio track using the **Audio parameter** table below.


<span id="739f7015"></span>
##### Single audio track

This table describes the transcoding parameters that can be applied to an audio track.


|**Parameter** |**Description** |
|---|---|
|Codec |AAC |
|Encoding level |Supports the following levels:<br><br><br>* **AAC\-LC**: Low complexity specification.<br><br>* **AAC\-HE**: High\-efficiency coding specification v1.<br><br>* **HE\-AAC v2**: High\-efficiency coding specification v2. It is recommended for low bit rate scenarios (< 80 kbps). It reduces the bit rate by half compared to AAC\-LC while maintaining similar audio quality. |
|Sampling rate |Supports the following options:<br><br><br>* 32000 Hz<br><br>* (Default) 44100 Hz<br><br>* 48000 Hz |
|Audio bitrate |If you do not set the audio bit rate, the output audio will retain the same bit rate as the original audio. The default value is 128. The value can range from 26 to 256. |
|Encoding method |Supports the following methods:<br><br><br>* (Default) Constant bit rate (CBR)<br><br>* Audio bit rate (Follow)<br><br>* Adaptive bit rate (CAE): Adopts adaptive encoding strategies for various audio scenarios. It dynamically adjusts based on the preset audio bit rate, and reduces the audio bit rate by 10% to 20% without compromising audio quality. |
|Channel |This parameter offers the following options:<br><br><br>* Original audio channels<br><br>* Mono<br><br>* Stereo<br><br>* 5.1 channel<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">It is not supported when the encoding level is set to <strong>HE\-AAC v2</strong>.</div><br> |
|Volume equalization |Enabling volume equalization helps to maintain a consistent output audio volume, avoiding any sudden increases or decreases in volume. You can set:<br><br><br>* (Required) **Target loudness**: Sets the target integrated loudness for the output audio, measured in LUFS (Loudness Units Full Scale). More negative values result in quieter audio. The value can range from \-70 to \-5.<br><br>* (Required) **True peak limit**: Sets the maximum true peak level allowed for the audio, measured in dBTP (decibels True Peak). This is crucial for preventing digital clipping and distortion. The value can range from \-9 to 0.<br><br>* (Optional) **Dynamic range**: Controls the amount of volume variation allowed in the audio. Smaller values reduce the difference between the loudest and quietest sounds (compression), making the overall volume more uniform. Larger values preserve more of the original dynamics. The value can range from 1 to 20. The default value is 7. |


<span id="e6343868"></span>
##### Multiple audio tracks

In **Multiple audio tracks** mode, you must first select a strategy for how the source audio tracks should be handled:


* **Retain all source audio tracks**: Applies a common transcoding configuration to all audio tracks from the source video. For example, if the source has 5 audio tracks, the output will also have 5 audio tracks, all processed with the same configuration. A maximum of 15 source tracks can be retained. If the source has more than 15 tracks, only the first 15 will be retained. If you select this, refer to the parameter definitions in the **Single audio track** section above to configure this single set of parameters.

* **Specify source tracks to retain**: Applies a unique transcoding configuration to a specific audio track, identified by its index. This allows you to process different source tracks with different configurations. You can add and configure up to 15 individual tracks. If you select this, click the **Add audio track** button. For each track you add, set the following parameters:

   * **Track index**: (Required) The index number of the source audio track to configure (starting from 0).

   * **Track name**: An optional custom name for this track, with a maximum length of 32 characters.

   * **Audio parameters**: Refer to the parameter definitions in the **Single audio track** section above to configure the transcoding settings for this specific track.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">When you configure multiple audio tracks for an ABR template using the <strong>FMP4</strong> or <strong>TS</strong> container, each audio track is generated as an independent stream and is not hard\-bound to any specific video sub\-stream. This allows the player to dynamically pair any audio track with any video quality during playback.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cadb372d3504d138db5133cbd7ac623~tplv-goo7wpa0wc-image.image) </span>

<span id="30059afd"></span>
## **Recommended configuration**

It is recommended to set clear tiers when configuring the maximum bitrate for sub\-streams. For example, use 1Mbps, 2Mbps, and 3Mbps to ensure a clear distinction in bitrate between the different video resolutions produced by the final transcoding output. This helps players to adapt and select the appropriate bitrate based on network bandwidth fluctuations.


* **Sub\-stream configuration example:** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/908a34b40cd04b7f976aeddba195b07c~tplv-goo7wpa0wc-image.image) </span>

* **Transcoding output sub\-streams example:** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee65b4b5bcb746bfa3b5fbf196651ec5~tplv-goo7wpa0wc-image.image) </span>
