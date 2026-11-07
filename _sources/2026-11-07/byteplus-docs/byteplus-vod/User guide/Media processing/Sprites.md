---
title: "Sprites"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-sprites"
---

When you want to add smooth, bandwidth\-efficient thumbnail previews to your video player's progress bar using BytePlus VOD, this guide provides step\-by\-step instructions to configure sprite templates, add generation tasks to your workflow, trigger processing, and retrieve sprite URLs to implement this feature seamlessly.

## What are sprites

Sprites are composite images created by merging multiple video snapshots. They are used to display thumbnail previews of video content when users drag the player's progress bar. They have the following advantages:

* Reduced image size: By combining many small thumbnail images into a single large sprite, you can apply more efficient compression algorithms, reducing the total image file size and lowering the volume of network data transmitted.

* Fewer requests: By consolidating multiple thumbnail images into sprites, you reduce the number of server requests made by users, which improves page load times.

## Working principles

Sprites are usually generated during transcoding. The general process is as follows:

1. Take a number of snapshots from the input video at certain intervals.

2. Arrange these snapshots in order and merge them into multiple large sprites, with the sprite URIs recorded.

3. Once generated, you can retrieve the sprite URLs by calling the BytePlus VOD API, then extract thumbnails for specific timestamps using a calculated offset.

Therefore, if you need to implement a thumbnail preview feature on the progress bar, please make sure to include the task of generating sprites during the video transcoding process.

## Prerequisites

* Enable the BytePlus VOD service. For details, see [Step 1: Enable the BytePlus VOD service](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started#b4e9d150).

* Create a new space in the BytePlus VOD console. For details, see [Spaces](https://docs.byteplus.com/docs/byteplus-vod/docs-space-management).

* Add an image domain name in the BytePlus VOD console. For details, see [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management).

## Procedure

### Step 1: Configure the snapshot template

Configure the snapshot template in the BytePlus VOD console. The specific steps are as follows:

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. In the left navigation bar, click **Media processing \> Templates**.

3. Click the **Snapshot** tab and click the **Add snapshot template** button.

4. Configure the parameters based on the prompts on the page. For **Type**, select **Sprite snapshots**. For **Image format**, select `jpeg` or `webp`. The default is `jpeg`. For a detailed description of the parameters, see [Snapshot template](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template#7b61b3c1).

   In the JPEG configuration example shown below, the number of snapshots is set as 10. The arrangement of the snapshots is set as 2 rows \* 2 columns, so 3 sprites will be generated, containing 4, 4, and 2 snapshots. The two empty spaces in the last sprite will be filled with a black background.

   ![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261016024630-362402813431.png)

### Step 2: Add the snapshot task to the workflow

The specific steps are as follows:

1. In the left navigation bar, click **Media processing \> Workflows**.

2. Click **Create workflow**.

3. In **Workflows**, select the **Snapshot** task, and set the media processing template as the snapshot template created in Step 1.

   > **Note**

   > You can add transcoding and snapshot tasks in a single workflow.

4. Configure the other parameters based on the prompts on the page. For a detailed description of the parameters, see [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow).

### Step 3: Trigger the media processing task

Trigger the media processing task through the console or API to generate the sprites. The specific instructions are as follows:

* Console:

   * In the left navigation bar, click **Media assets \> Videos**.

   * Select the specific media asset file from the list to initiate processing.

* API: Call the [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow) API.

### Step 4: View media processing status

After triggering the media processing task, you can view the results of workflow execution via the console, API, or callback events. The specific instructions are as follows:

* Console: In the left navigation bar, click **Tasks \> Transcoding tasks** to view the task status.

* API: Call the [GetWorkflowExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getworkflowexecution) API to view the results of workflow execution.

* Callback event: [WorkflowComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflowcomplete)

### Step 5: Get the sprite URLs

Once media processing is successfully completed, you can get the sprite URLs directly via the console or API. You can also retrieve sprite URIs via the OpenAPI or callback events, then construct the full sprite URLs yourself by following the specified formatting rules.

#### Using the console

Follow the steps below to get the sprite URLs directly via the console:

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. In the left navigation bar, click **Media assets \> Videos**.

3. Click the **Details** button to go to the **Video details** page.

4. Click **Snapshot result**.You can then copy the link or preview the images.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68a0dfcb9d2d415fa8bc94548e2e836e~tplv-goo7wpa0wc-image.image)

#### Using the **OpenAPI**

Call [ListSnapshots](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listsnapshots) to get the sprite URLs or URIs from the `Urls` and `StoreUris` parameters in the `SpriteSnapshots` structure.

#### Using the event

Get the sprite URIs from the `StoreUris` parameter within the `Snapshots` structure in the [WorkflowComplete](https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflowcomplete) event.

> **Note**

> To learn more about how to merge and get sprite URLs based on `StoreUri`, see [Constructing the image URL](https://docs.byteplus.com/docs/byteplus-vod/docs-realtime-image-processing#72e02267).

Below is an example of the sprite information returned by the workflow execution completion event:

```json
{
"Snapshots": [
    {
      "Type": "Sprite",
      "Params": {
        "Format": "jpeg",
        "StoreUris": [
          "tos-vod-cn-v-03e4***3112705/48f0b9e130374ed6b***4b8be"
        ],
        "ImgXLen": 2,
        "ImgYLen": 2,
        "CellWidth": 360,
        "CellHeight": 202,
        "Interval": 4,
        "CaptureNum": 4
      }
    }
]
}
```
