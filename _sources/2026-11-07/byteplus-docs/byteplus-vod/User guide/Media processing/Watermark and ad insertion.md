---
title: "Watermark and ad insertion"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-watermark-and-ad-insertion"
---

To protect your video copyright and increase brand exposure, you can use the watermark and ad insertion feature. This feature allows you to add image, video, or text watermarks and place ads at the beginning or end of your videos. This guide provides step\-by\-step instructions on how to configure and apply these settings through a workflow.

<span id="89d62521"></span>
## Feature introduction

BytePlus VOD supports three types of watermarks:


* Image watermark: Supports PNG format. You can specify where and when the image is displayed in the video.

* Video watermark: Supports MOV format. You can specify where and when the video watermark is displayed.

* Text watermark: You can add specific text over the video as a watermark. Font style, size, and color can all be customized. Different videos can have different text watermarks.


Additionally, BytePlus VOD allows for the placement of ads at the beginning or end of videos. Currently, only MP4 format is supported. This feature is useful for attaching branding or short videos to increase exposure.

<span id="e7aa47b5"></span>
## Applicable scenarios


* Watermarks can be used for displaying brand names, brand logos, TV station logos, app names, and other relevant information. This serves purposes such as copyright protection and brand promotion.

* Video ads can be utilized to attach branding or short videos to the beginning or end of videos, thereby increasing exposure.


<span id="10e28d0f"></span>
## Procedure

<span id="174aa7e2"></span>
### Step 1: Configure the watermark and ad insertion template

Configure the watermark and ad insertion template on the BytePlus VOD console. You can use one of the pre\-built templates or create your own. For details, see [Watermark and ad insertion template](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template).

<span id="409f2683"></span>
### Step 2: Enable in the workflow

Enable watermark or in\-stream ad when configuring the video transcoding or low\-bitrate HD transcoding task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d858969b84f414ab02df166ea803974~tplv-goo7wpa0wc-image.image) </span>

<span id="a8a1c636"></span>
### Step 3: Trigger a media processing task

Trigger the media processing task through the console or API to apply the watermark or ad. The specific instructions are as follows:


* Console:

   * In the left navigation bar, click **Media assets** \> **Videos**.

   * Select the specific media asset file from the list to initiate processing.

* API: Call the [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow) API.
