---
title: "Low-bitrate HD template"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template"
---

To reduce video bandwidth costs and enhance visual quality for your viewers, you can use low\-bitrate HD templates in BytePlus VOD. This guide provides step\-by\-step instructions on how to create and configure these templates in the console, covering all basic, video, and audio parameters.

<span id="33258f35"></span>
## Feature overview

BytePlus VOD's low\-bitrate HD transcoding feature intelligently analyzes scenes, actions, content, textures, and more in the video. It selects the optimal encoding parameters to output videos with better subjective quality at a relatively lower bitrate. This not only reduces bandwidth costs but also provides an enhanced visual experience.

<span id="6dd6f799"></span>
## Creating a low\-bitrate HD template


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media processing** \> **Templates** on the left navigation bar.

5. Click the **Low\-bitrate HD** tab.

6. Click **Create low\-bitrate HD template**.

7. In the dialog box that appears, configure the basic information, audio transcoding parameters, and video transcoding parameters according to your specific business requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de9bc684d7be43a9ad35c5d0c4943a24~tplv-goo7wpa0wc-image.image) </span>

   For details, see the following documentation:

   * [Basic information](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template#6f81f7de)

   * [Video parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template#01d87a9a)

   * [Audio parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template#28b038c6)

8. Click **Save**.


<span id="55d5899e"></span>
## Parameters

<span id="6f81f7de"></span>
### Basic information


|**Parameter** |**Description** |
|---|---|
|Template name |The length of the template name cannot exceed 64 characters. It is recommended to use a name that can identify the content of the template. |
|Template description |The length of the template description cannot exceed 140 characters. |
|Output format |BytePlus VOD supports the following containers:<br><br><br>* MP4<br><br>* DASH<br><br>* HLS<br><br>* FLV<br><br>* TS |
|Resolution |The resolution of the output video:<br><br><br>* 240p<br><br>* 360p<br><br>* (Default) 480p<br><br>* 540p<br><br>* 720p<br><br>* 1080p<br><br>* 2k<br><br>* 4k<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">We recommend using 360p, 480p, and 720p for most business scenarios, devices, and network environments. If the user's bandwidth is limited or video deduplication is necessary, we suggest using 240p or 360p.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When selecting an output format such as MP4, DASH, or HLS, we suggest setting the video resolution to one of the following: 240p, 360p, 480p, 540p, 720p, 1080p, 2k, 4k, or original (transmuxing). If you choose original (transmuxing), the output video will maintain the same video and audio parameters as the original.</div><br> |
|||
|Custom resolution |Customize the resolution of the output video. |
|Scaling method |When the width and height set in the template are inconsistent with the aspect ratio of the input video, you can choose from one of the following scaling modes:<br><br><br>* (Default) Keep the aspect ratio of the input video.<br><br>* Adaptive stretching: Stretch the input video according to the width and height set in the template.<br><br>* Adaptive stretching plus black edge: Resizes the input video while maintaining its aspect ratio. Any resulting empty areas are filled with black bars. |
|Encryption |This parameter only appears when the output format is MP4, DASH, or HLS. BytePlus VOD supports the following encryption methods:<br><br><br>* **Private encryption**: For details, see [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption).<br><br>* **HLS standard encryption**: This option only appears when the output format is HLS. For details, see [HLS standard encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-standard-encryption).<br><br>* **DRM encryption**: This option only appears when the output format is DASH or HLS. For details, see [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption). |
|DRM type |This parameter is only available when using DRM encryption. Select the DRM type you want to enable. BytePlus VOD supports Google Widevine, Apple FairPlay, and Microsoft PlayReady DRM encryption. For a detailed overview of DRM encryption, please refer to [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption). |


<span id="01d87a9a"></span>
### Video parameters

Define how the video stream will be processed.


|**Parameter** |**Description** |
|---|---|
|Codec |* (Default) H.264<br><br>* H.265 |
|Container format |This parameter only appears when the output format is HLS and offers the following options:<br><br><br>* TS (MPEG Transport Stream)<br><br>* FMP4 (Fragmented MP4) |
|Image quality |* Higher quality<br><br>* High quality<br><br>* (Default) Standard<br><br>* Low bandwidth<br><br>* Lower bandwidth |
|CRF value |Constant Rate Factor (CRF) is an encoding mode that adjusts the file data rate up or down to achieve a selected quality level rather than a specific data rate. CRF values range from 0 to 51, with lower numbers delivering higher quality. The default value is 25 and we recommend you set a value between 23 and 27. |
|Maximum bitrate |The value range for the maximum bitrate is [10,50000]. |
|Frame rate |This parameter offers the following options:<br><br><br>* Same as input: The value range for the maximum frame rate is [1, 60]. If the input video's frame rate does not exceed the specified maximum, the output frame rate will match the input. Otherwise, the output frame rate will be capped at the specified maximum.<br><br>* Fixed frame rate: The value range for the maximum frame rate is [1, 60]. |


<span id="28b038c6"></span>
### Audio parameters

Define how the audio stream will be processed. First, decide if your output video will contain one or multiple audio tracks by selecting **Track mode**:


* **Single audio track:**  (Default) The output video will have one standard audio track.

* **Multiple audio tracks:**  This mode is designed for source videos that already contain multiple audio tracks. It allows you to extract these tracks and apply specific transcoding configurations to each. The output video will contain multiple audio tracks that viewers can switch between.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">The available options depend on the <strong>Output format</strong> and <strong>Container format</strong> you selected in the <strong>Basic information</strong> section. <strong>Multiple audio tracks</strong> are supported only when:</div>



* <div data-tips="true" data-tips-type="warning">The <strong>Output format</strong> is <code>MP4</code>.</div>


* <div data-tips="true" data-tips-type="warning">The <strong>Output format</strong> is <code>HLS</code> and the <strong>Container format</strong> is <code>FMP4</code> or <code>TS</code>.</div>



<div data-tips="true" data-tips-type="warning">For all other output formats (such as <code>DASH</code>, <code>FLV</code>, or <code>TS</code>), only a <strong>single audio track</strong> is supported.</div>


<span id="2cbe0f14"></span>
#### Single audio track

In **Single audio track** mode, configure the audio parameters directly according to the following table.


|**Parameter** |**Description** |
|---|---|
|Codec |AAC |
|Encoding level |Supports the following levels:<br><br><br>* **AAC\-LC**: Low complexity specification.<br><br>* **AAC\-HE**: High\-efficiency coding specification v1.<br><br>* **HE\-AAC v2**: High\-efficiency coding specification v2. It is recommended for low\-bitrate scenarios (< 80 kbps). It reduces the bit rate by half compared to AAC\-LC while maintaining similar audio quality. |
|Sampling rate |Supports the following options:<br><br><br>* **32000 Hz**<br><br>*  **(Default) 44100 Hz**<br><br>* **48000 Hz** |
|Audio bitrate |If you do not set the audio bitrate, the output audio will retain the same bitrate as the original audio. The default value is 128. The value range is [26,256]. |
|Encoding method |Supports the following methods:<br><br><br>* (Default) Constant bit rate (CBR)<br><br>* Audio bitrate (Follow)<br><br>* Adaptive bit rate (CAE): Adopts adaptive encoding strategies for various audio scenarios. It dynamically adjusts based on the preset audio bitrate and reduces the audio bitrate by 10% to 20% without compromising audio quality. |
|Channel |This parameter offers the following options:<br><br><br>* Original audio channels<br><br>* Mono<br><br>* Stereo<br><br>* 5.1 channel<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">It is not supported when the encoding level is set to <strong>HE\-AAC v2</strong>.</div><br> |
|Volume equalization |Enabling volume equalization helps to maintain a consistent output audio volume, avoiding any sudden increases or decreases in volume. You can set:<br><br><br>* (Required) **Target loudness**: Sets the target integrated loudness for the output audio, measured in LUFS (Loudness Units Full Scale). More negative values result in quieter audio. The value range is[\-70, \-5].<br><br>* (Required) **True peak limit**: Sets the maximum true peak level allowed for the audio, measured in dBTP (decibels True Peak). This is crucial for preventing digital clipping and distortion. The value range is [\-9, 0].<br><br>* (Optional) **Dynamic range**: Controls the amount of volume variation allowed in the audio. Smaller values reduce the difference between the loudest and quietest sounds (compression), making the overall volume more uniform. Larger values preserve more of the original dynamics. The value range is [1, 20]. The default value is 7. |


<span id="de965b66"></span>
#### Multiple audio tracks

In **Multiple audio tracks** mode, you must first select a strategy for how the source audio tracks should be handled:


* **Retain all source audio tracks**: Applies a common transcoding configuration to all audio tracks from the source video. For example, if the source has 5 audio tracks, the output will also have 5 audio tracks, all processed with the same configuration. A maximum of 50 source tracks can be retained. If the source has more, only the first 50 will be retained. If you select this, refer to the parameter definitions in the **Single audio track** section above to configure this single set of parameters.

* **Specify source tracks to retain**: Applies a unique transcoding configuration to a specific audio track, identified by its index. This allows you to process different source tracks with different configurations. You can add and configure up to 50 individual tracks. If you select this, click the **Add audio track** button. For each track you add, set the following parameters:

   * **Track index**: (Required) The index number of the source audio track to configure (starting from 0).

   * **Track name**: An optional custom name for this track, with a maximum length of 32 characters.

   * **Audio parameters**: Refer to the parameter definitions in the **Single audio track** section above to configure the transcoding settings for this specific track.
