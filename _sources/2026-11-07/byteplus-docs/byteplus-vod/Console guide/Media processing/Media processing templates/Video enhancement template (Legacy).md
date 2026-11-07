---
title: "Video enhancement template (Legacy)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-enhancement-template-legacy"
---

To improve the quality of your videos with advanced AI algorithms, you can use BytePlus VOD's video enhancement feature. This guide provides step\-by\-step instructions on how to create and configure a video enhancement template in the console, enabling features like super resolution, frame interpolation, and SDR to HDR conversion.

<span id="192b0731"></span>
## Feature overview

BytePlus VOD's video enhancement feature uses advanced AI algorithms to restore or enhance the quality of videos. The feature includes a template that offers the following capabilities:


* Super resolution: Uses deep learning methods to enhance and restore details in low\-resolution videos, outputting high\-resolution videos with clearer details.

* Frame interpolation: Inserts additional frames between existing ones to provide a smoother viewing experience and fix stuttering and shaky videos shot at low frame rates.

* SDR enhancement: Optimizes the color of SDR videos based on their semantic content and color, resulting in improved color quality.

* SDR to HDR: Converts SDR videos to HDR and increases the color depth to display a wider gamut and more color details.

* Noise reduction: Removes random noise introduced during video recording from the camera and environment while maintaining audio/video details.


<span id="c0c51ae4"></span>
## Specifications and limitations


* Video enhancement templates can be applied to input resolutions below 1080p. The output resolution is not fixed and depends on the source video quality.

* When video enhancement and transcoding tasks are combined, and the [Video transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-video-transcoding-template) is set to a target resolution:

   * **When the video enhancement result is less than the target resolution:**  The output is generated at the resolution of the video enhancement result.

   * **When the video enhancement result is equal to or greater than the target resolution:**  The output is generated at the target resolution.

   * *Example:*  If the target resolution in the transcoding template is 1080p and the video enhancement result is 1440p, the output will be 1080p. If the target resolution is 1080p and the video enhancement result is 720p, the output will be 720p.


<span id="cd85d45a"></span>
## Creating a video enhancement template


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media processing** \> **Templates** on the left navigation bar.

5. Click the **Video enhancement** tab.

6. Click **Add video enhancement template**.

7. In the dialog box that appears, configure the basic information of the template.

   
   |**Parameter** |**Description** |
   |---|---|
   |Template name |The length of the template name cannot exceed 64 characters. It is recommended to use a name that clearly identifies the template's purpose. |
   |Template description |The length of the template description cannot exceed 140 characters. |
   

8. Enable the feature that you want.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b63985be3a864126adb8c26c8a63a7cb~tplv-goo7wpa0wc-image.image) </span>

9. Click **Save**.
