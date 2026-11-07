---
title: "Audio transcoding template"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-audio-transcoding-template"
---

To standardize your audio processing workflows, you can create and configure reusable audio transcoding templates in the BytePlus VOD console. This guide provides step\-by\-step instructions for creating a template and details all available configuration parameters, including container formats, encryption, codecs, and bitrates.

<span id="6dd6f799"></span>
## Creating an audio transcoding template


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media processing** \> **Templates** on the left navigation bar.

5. Click the **Audio transcoding** tab.

6. Click **Create audio transcoding template**.

7. In the dialog box that appears, configure the basic information, audio transcoding parameters, and video transcoding parameters based on your specific business requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5771708cd614408a2b57e2181021bf0~tplv-goo7wpa0wc-image.image) </span>

   For details, see the following documentation:

   * [Configuring basic information](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template#6f81f7de)

   * [Configuring audio parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template#28b038c6)

8. Click **Save**.


<span id="6f81f7de"></span>
## Configuring basic information


|**Parameter** |**Description** |
|---|---|
|Template name |The length of the template name cannot exceed 64 characters. It is recommended to use a name that can identify the content of the template. |
|Template description |The length of the template description cannot exceed 140 characters. |
|Container format |This parameter offers the following options:<br><br><br>* MP4<br><br>* DASH<br><br>* HLS<br><br>* FLV<br><br>* TS |
|DASH segment type |This parameter only appears when the container format is DASH. The available options are:<br><br><br>* SegmentTemplate<br><br>* SegmentBase |
|DASH segment duration |This parameter only appears when the container format is DASH. The default value is 5 seconds. The range is [1,600]. |
|HLS segment type |This parameter only appears when the container format is HLS. The available options are:<br><br><br>* SegmentTemplate<br><br>* SegmentBase |
|HLS segment duration |This parameter only appears when the container format is HLS. The default is 5 seconds. The value range is [1,600]. |
|Audio quality |This parameter offers the following options:<br><br><br>* Standard quality<br><br>* (Default) High quality<br><br>* Music quality |
|Audio encryption |This parameter only appears when the container format is M4A, MP4, DASH, or HLS. BytePlus supports the following encryption methods:<br><br><br>* Private encryption. For more information, see [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption).<br><br>* DRM encryption. This option only appears when the container format is DASH or HLS. For more information, see [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption). |
|DRM type |This parameter is only available when using DRM encryption. Select the DRM type you want to enable. BytePlus VOD supports Google Widevine, Apple FairPlay, and Microsoft PlayReady DRM encryption. For a detailed overview of DRM encryption, please refer to [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption). |


<span id="28b038c6"></span>
## Configuring audio parameters


|**Parameter** |**Description** |
|---|---|
|Codec |mp3 |
|Sampling rate |This parameter offers the following options:<br><br><br>* 8000 Hz<br><br>* 11025 Hz<br><br>* 12000 Hz<br><br>* 16000 Hz<br><br>* 22050 Hz<br><br>* 24000 Hz<br><br>* 32000 Hz<br><br>* (Default) 44100 Hz<br><br>* 48000 Hz<br><br>* 64000 Hz<br><br>* 88200 Hz<br><br>* 96000 Hz |
|Audio bitrate |If you do not set the audio bitrate, the output audio will retain the same bit rate as the input audio. The default value is 128. The value range is [26,256]. |
|Channel |This parameter offers the following options:<br><br><br>* Mono<br><br>* Stereo<br><br>* 5.1 channel |
|Volume equalization |Enabling volume equalization helps to maintain a consistent output audio volume, avoiding any sudden increases or decreases in volume. |
