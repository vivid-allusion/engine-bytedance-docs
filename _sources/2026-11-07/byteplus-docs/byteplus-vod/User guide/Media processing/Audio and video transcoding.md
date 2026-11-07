---
title: "Audio and video transcoding"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-audio-and-video-transcoding"
---

Transcoding converts audio and video files to make them compatible with various playback devices, network environments, and business scenarios. This process can help you reduce storage and distribution costs while delivering a smooth, high\-quality viewing experience. This guide explains the types of transcoding available in BytePlus VOD, their common applications, and provides step\-by\-step instructions for configuring and executing transcoding tasks.

<span id="72d07ddf"></span>
## Feature introduction

<span id="fa00a3d1"></span>
### What is transcoding?

Transcoding is the process of converting one video stream to another. It involves converting codecs (such as H.264, AAC), encoding parameters (sample rate, resolution, bitrate, I\-frame interval), and container formats (MP4, TS) to adapt to different business scenarios, playback devices, and network environments. Transcoding essentially entails decoding and re\-encoding, which means that the streams before and after conversion may not follow the same video codec standards.

<span id="f00c9760"></span>
### Transcoding types

BytePlus VOD supports multiple types of transcoding. You can select a transcoding type to suit your business needs when configuring media processing templates.


|Type |Description |
|---|---|
|Standard transcoding |Convert an audio or video file into one or more audio or video files. You can modify the video codec, container format, resolution, bitrate, and other parameters to adapt to different business scenarios, playback devices, and network environments. |
|Low\-bitrate HD transcoding |Intelligently analyzes scenes, actions, content, textures, and more in the video and selects the optimal encoding parameters to output videos with better subjective quality at a relatively lower bitrate. This reduces bandwidth costs while presenting a better visual experience. |


<span id="5f97f015"></span>
## Applicable scenarios

Transcoding is applicable in various scenarios, including:


* Multi\-end device scenarios: Transcoding enables videos to be played back seamlessly across multiple platforms, such as desktops, TVs, and mobile devices.

* Cost reduction in storage and distribution: Transcoding ensures consistent image quality while adjusting the video bitrate, improving video compression, and reducing file size. This leads to smoother playback, as well as reduced storage and traffic costs.

* Network environment: Transcoding allows users with different network bandwidths to select the optimal bitrate for smooth playback, ensuring a better viewing experience.

* Copyright protection: Transcoding plays a crucial role in protecting audiovisual files in online copyright scenarios, including online education, finance, industry training, and exclusive dramas.


<span id="3a6e6dd5"></span>
## Procedure

<span id="9b8098a9"></span>
### Step 1: Configure the transcoding template

Configure the transcoding template on the BytePlus VOD console. You can use one of the pre\-built templates or create your own. For details, see the following:


* [Audio transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template)

* [Video transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-video-transcoding-template)

* [Low-bitrate HD template](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template)


<span id="bab89b46"></span>
### Step 2: Add a transcoding task in the workflow

Add a transcoding task in the workflow via the BytePlus VOD console, as shown in the following picture.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9c9b3c4c63f433f8e82e0f242c40e2d~tplv-goo7wpa0wc-image.image) </span>

<span id="6296c076"></span>
### Step 3: Trigger a media processing task

Trigger the media processing task through the console or API to generate video files. The specific instructions are as follows:


* Using the console:

   * In the left navigation bar, click **Media assets** \> **Videos**.

   * Select the specific media asset file from the list to initiate processing.

* API: Call [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow). You need to pass in the workflow ID that contains the transcoding task.


<span id="6689f311"></span>
### Step 4: Retrieve the transcoding result

After a transcoding task is triggered, you can check its status and obtain information, such as the playback address of the output video, using the following methods. Once you have the video playback address, you can use the BytePlus Player SDK or a third\-party player to play the transcoded video.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before you begin, ensure that you have added a VOD acceleration domain and enabled VOD scheduling. This allows you to retrieve the video playback address from the VOD service based on your domain using the <a href="https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a> API. For detailed instructions, refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management">Adding domain name</a>.</div>


**Using the console**


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and navigate to the desired space.

2. Find the video for which you want to transcode and click **Details** in the **Actions** column.

3. Under the **Playback address** tab, copy the link or preview the transcoded audio and video files.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cacba50b5104b699fba51c95a567c7a~tplv-goo7wpa0wc-image.image) </span>


**Using the OpenAPI/Server\-Side SDK**


1. Call [GetWorkflowExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getworkflowexecution) to retrieve the execution status of the workflow task.

2. Once the task is successful, call [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) to obtain the video playback address. The playback address of the transcoded output will be returned in the `PlayInfoList` parameter.


**Manually constructing the URL**


1. Configure the [WorkflowComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete) event notification to be alerted upon workflow completion. The VOD service will notify you when a task is finished. You can then retrieve the storage address of the transcoded output from the `StoreUri` parameter within the `TranscodeInfo` array of the callback result.

2. Parse the `FileName` from the `StoreUri`. The `StoreUri` consists of a `BucketName` and a `FileName`. For example, if the `StoreUri` is `tos-vod-v-9fbcde4037780626/40e625a6d1694fe7b6f03f9eddcc16a5`, the `BucketName` is `tos-vod-v-9fbcde4037780626`, and the `FileName` is `/40e625a6d1694fe7b6f03f9eddcc16a5`.

3. Construct the playback address using the following format:

   * **Format**: `Protocol://PlaybackDomain/FileName?auth_key=xxx`

   * **Example**: If your VOD acceleration domain, `PlaybackDomain`, is `play.vod.com`, the playback address for the video will be `http://play.vod.com/40e625a6d1694fe7b6f03f9eddcc16a5`. If you have enabled URL authentication in the VOD console, you will also need to calculate the `auth_key` signature based on your chosen authentication type. For more information, see the [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview).


**Using the API**

Call the [DeleteTranscodes](https://docs.byteplus.com/docs/byteplus-vod/reference-deletetranscodes) API to delete transcoded files. You need to provide the `Vid` of the video and the `FileIds` of the transcoded files to be deleted.
