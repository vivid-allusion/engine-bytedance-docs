---
title: "Adaptive bitrate streaming"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-abr-streaming"
---

To ensure a smooth playback experience for your users across different network conditions, you can use BytePlus VOD's adaptive bitrate streaming (ABR) feature. This guide provides step\-by\-step instructions on the entire process, from creating an ABR template and configuring a workflow to obtaining the final playback URL for integration with your player.

<span id="2d1a576d"></span>
## Compatibility

BytePlus VOD currently supports HLS and DASH adaptive bitrate streaming protocols.

<span id="0fb1e525"></span>
## Restrictions

Pure audio input for ABR streaming is not supported.

<span id="39a8619b"></span>
## Prerequisites

Ensure that you have [added the playback domain name](https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-management) and [enabled type A signing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-url-authentication-overview).

<span id="aede4974"></span>
## Procedure

<span id="32f83d71"></span>
### Step 1: Create an ABR streaming template

Create an ABR streaming template on the BytePlus VOD console. For details, see [ABR streaming template](https://docs.byteplus.com/docs/byteplus-vod/docs-abr-streaming-template).

<span id="e2ad6c8c"></span>
### Step 2: Configure the workflow

Add an ABR streaming transcoding task in the workflow and specify the ABR streaming template you created in step 1, as shown in the following image. For details, see [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a335f4b3690414ba861215480d4df7a~tplv-goo7wpa0wc-image.image) </span>

<span id="bc38b88d"></span>
### Step 3: Trigger the transcoding task

Transcode the videos using the configured workflow. BytePlus VOD supports triggering transcoding during or after video upload. You can set a default workflow at the space level, specify a workflow ID during upload, or manually trigger the workflow after upload. For specific operations, see [Triggering a workflow](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#e6ad1664).

<span id="e06f086b"></span>
### Step 4: Get the video playback address

After triggering the transcoding task, obtain the playback address of the transcoded output video.

<span id="6fb3a124"></span>
#### **Using the console**


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter the specific space.

2. On the **Videos** page, click the **Details** button in the actions column for the target video to view the **Video details** page.

3. Under the **Playback address** tab, copy the link or preview the transcoded audio and video files.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be2e4597d81448c9b9296ff27adfe685~tplv-goo7wpa0wc-image.image) </span>


<span id="d2359504"></span>
#### **Using the OpenAPI or Server SDKs**

Call [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) with the `Vid` parameter and set `Definition` to `Auto` to obtain the video playback address of the ABR streaming file. You can retrieve the main stream and sub\-stream addresses from the returned `AdaptiveBitrateStreamingInfo` and `PlayInfoList` parameters. BytePlus VOD offers Server SDKs for OpenAPI, compatible with various programming languages to streamline development processes. It's recommended to use the Server SDKs for API calls. For more information, see the following documents:


* [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

* [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

* [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

* [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)


<span id="d019a1e3"></span>
#### Using the event

Retrieve the ABR file information from the `AdaptBitrateTranscodeInfos` parameter in the [WorkflowComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflowcomplete) event.

<span id="adc389c9"></span>
### Step 5: Multi\-bitrate adaptive playback

To allow the player to automatically switch to the optimal video stream based on network bandwidth and device, you must set up the ABR streaming feature in the player. For instructions on configuring the ABR streaming feature with the BytePlus VOD Player SDK, refer to the following documentation:


* [Web Player SDK - ABR streaming](https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-advanced-features-web#abr-streaming)
