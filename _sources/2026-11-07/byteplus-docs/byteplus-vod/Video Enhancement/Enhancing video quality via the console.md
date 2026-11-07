---
title: "Enhancing video quality via the console"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/enhancing_video_quality_via_console"
---

This document describes how to use the BytePlus VOD console to configure and trigger video enhancement tasks.

<span id="da81c6ae"></span>
## **Step 1: Configure a video enhancement template**


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/). Ensure you have selected the **Johor** region from the dropdown menu in the top navigation bar of the console.

2. Navigate to **Media processing** \> **Templates** and click the **Video enhancement** tab.

3. Click **Create template** and configure its name, select a preset scenario, and customize parameters as needed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">For detailed, step\-by\-step instructions on this process, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template">Video enhancement template</a>.</div>


<span id="d6c3e56c"></span>
## Step 2: Trigger the video enhancement task

You can trigger the enhancement in two ways:

<span id="a3886ec1"></span>
### Option A: Via workflow

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Video enhancement tasks configured with a target resolution of 6K or 8K, a color depth of 12\-bit or 16\-bit, or a frame rate of 60 fps or higher have a very high risk of timing out when run in a workflow. To ensure reliable processing, <a href="https://docs.byteplus.com/en/docs/25/100675#b207c890">submit a single template task on the console</a> or use the <a href="https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-template">StartExecution</a> API to run a single video enhancement template instead.</div>



1. Once the template is created, you can add a video enhancement task to a workflow and associate the task with the video enhancement template that you have configured on the BytePlus VOD console, as shown in the image below.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/282fe60f3fc44f5b8ed11f812e9fe9fc) </span>

   When adding the video enhancement task, you must configure how the results are saved.

   * When separate storage is disabled (Default): The video enhancement task must be combined with a transcoding task. In this mode, the system first performs quality enhancement and then immediately transcodes the enhanced result into the desired formats.

   * When separate storage is enabled: The video enhancement task can run as a standalone operation. You must specify an output file path where the enhanced video will be saved.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed, step\-by\-step instructions on this process, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-workflow">Workflows</a>.   </div>
   

2. You can set this workflow as the space's default, specify the workflow ID during upload, or manually trigger it after upload. For detailed instructions, see [Triggering a workflow](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#e6ad1664).


<span id="b207c890"></span>
### Option B: Via single template task

For small\-scale processing needs, you can select the videos on the **Media assets** page of the console and manually trigger a single template task. For details, see [Trigger single template processing](https://docs.byteplus.com/docs/byteplus-vod/docs-media-processing#c55f5643).

<span id="510c16ed"></span>
## Step 3: View results


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select the specific space.

2. Click **Media processing** \> **Tasks** to check the status of the media processing task.

3. When the status is **Success**, click **View details**.

4. On the details page, click the **View product** button.

5. On the **Playback address** tab, view the results of the enhancement task.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d18c7a799e024d059d8c71d505277462) </span>
