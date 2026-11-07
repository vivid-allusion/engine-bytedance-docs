---
title: "Video snapshots"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-snapshots"
---

To create engaging video covers and previews such as static images, dynamic GIFs, or image sprites, you can use the BytePlus VOD snapshot feature. This guide explains the different snapshot types available and provides step\-by\-step instructions on how to configure a workflow to automatically generate them from your videos.

<span id="7cfb2ced"></span>
## Snapshot types

BytePlus VOD supports many types of snapshots, which can be used as video covers and previews to attract users, effectively improving the platform's click\-through rate.


|Snapshot type |Description |
|---|---|
|Static snapshots |Captures a single static snapshot from a video. |
|Sampled snapshots |Captures multiple images from a video. Supports capturing images by time interval, capturing a specified number of images distributed uniformly, and also supports random snapshots. |
|Dynamic snapshots |Captures content from a range within the specified video to generate a dynamic image in WebP or GIF format. Supports custom capture start and end times, dynamic snapshot duration, and dynamic snapshot frame rate. |
|Sprites |Sprites are created by capturing static snapshots and then splicing them into a single large image according to a specific layout, which provides a preview effect when a user drags the player's progress bar. For more information, see [Sprites](https://docs.byteplus.com/docs/byteplus-vod/docs-sprites). |


<span id="13495ab9"></span>
## Procedure

<span id="8bc4cf90"></span>
### Step 1: Configure the snapshot template

Configure the snapshot template on the BytePlus VOD console. You can use one of the pre\-built templates or create your own. For detailed steps, see [Snapshot template](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template).

<span id="ab7063c0"></span>
### Step 2: Add the snapshot task to the workflow

The specific steps are as follows:


1. In the left navigation bar, click **Media processing \> Workflows**.

2. Click **Create workflow**.

3. In **Workflows**, select the **Snapshot** task, and set the media processing template as the snapshot template created in Step 1.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add transcoding and snapshot tasks in a single workflow.   </div>
   

4. Configure the other parameters based on the prompts on the page. For a detailed description of the parameters, see [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow).


<span id="a40237b2"></span>
### Step 3: Trigger the media processing task

Trigger the media processing task through the console or API to generate the snapshots. The specific instructions are as follows:


* Console:

   * In the left navigation bar, click **Media assets \> Videos**.

   * Select the specific media asset file from the list to initiate processing.

* API: Call the [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow) API.


<span id="9f62b83a"></span>
### Step 4: Get the snapshot result

Once media processing is successfully completed, follow the steps below to get the snapshot URLs directly via the console:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. In the left navigation bar, click **Media assets \> Videos**.

3. Click the **Details** button to go to the **Video details** page.

4. Click **Snapshot result**. You can then copy the link or preview the images.
