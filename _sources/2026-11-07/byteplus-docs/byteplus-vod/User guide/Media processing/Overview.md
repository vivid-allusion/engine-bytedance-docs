---
title: "Overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-processing-overview"
---

BytePlus VOD's media processing provides a rich set of features, including transcoding, snapshotting, and video enhancement, to convert your media files for optimal playback on any device. To streamline this process, you can use media processing templates to manage complex parameters and combine them into workflows to automate multi\-step tasks. This document introduces these core capabilities and the workflow mechanism, guiding you on how to configure, trigger, and monitor your media processing tasks.

> **Note**

> For video enhancement capabilities, configuration options, and guides for the console, OpenAPI, and AI skill, see the [Video Enhancement overview](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement).

## Media processing capabilities

The media processing capabilities provided by BytePlus VOD are as shown in the table below:

|**Media processing capability** |**Description** |
|---|---|
|Audio and video transcoding |* Standard transcoding: Converts an audio or video file into one or more audio or video files. You can modify the video codec, container format, resolution, bitrate, and other parameters to adapt to different business scenarios, playback devices, and network environments.<br><br>* Low\-bitrate HD: Intelligently analyzes scenes, actions, content, textures, and more in the video and selects the optimal encoding parameters to output videos with better subjective quality at a relatively lower bitrate. This reduces bandwidth costs while presenting a better visual experience.<br><br>* Low\-cost transcoding: Performs transcoding with lower resource consumption while ensuring subjective image quality. The price for low\-cost transcoding is 50% off the normal transcoding price. |
|Snapshots |Offers a range of snapshot options, including static images, sampled snapshots, GIFs, looping GIFs, and sprites, which can be used as video covers and video previews. |
|Video enhancement |Supports image enhancement and repair of the input video through AI super resolution, AI frame interpolation, HDR, and other techniques. This improves the clarity, image quality, and subjective quality of the video, thereby improving the playback and viewing experience. |
|Image enhancement and processing |Enhances image assets with AI super resolution or applies basic resizing, cropping, padding, and format conversion. Configure processing during image upload or submit a task for an existing image. See [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement). |
|Watermarks and tiles |Supports adding watermarks and tiles to videos. Video watermarks can display the brand name, logo, TV station logo, app name, and other information, for copyright protection, brand promotion, and other purposes. |
|Smart captioning |Supports fast, accurate generation of captions and extraction of captions from video files through the use of AI capabilities, as well as machine translation of captions. |

## Media processing templates

The parameters for media processing are generally rather complex. For example, video transcoding can include dozens of parameters such as container format, codec, bitrate, resolution, and frame rate. To make parameter management easier, BytePlus VOD provides media processing templates, which can contain the various media processing parameters:

* Pre\-built media processing templates: For common media processing parameter sets, BytePlus VOD provides pre\-built media processing templates.

* Custom media processing templates: For personalized media processing needs, you can customize media processing templates on the BytePlus VOD console.

By using media processing templates, you can avoid the tedious process of reconfiguring and adjusting media processing parameters. You just need to select a suitable template, and then apply it to the media file to be processed. The system will automatically process the file based on the parameters defined in the template.

## Workflows

In BytePlus VOD, the following video processing actions are all independent tasks:

* Transcode a video file into MP4 with a resolution of 360p

* Transcode a video file into MP4 with a resolution of 480p

* Sample screenshots from a video file at an interval of 10 seconds

* Intelligently categorize video files

To make it easier for you to process video files, BytePlus VOD provides the **workflow** mechanism. A workflow is essentially a "parent task" containing multiple media processing subtasks. Initiating a workflow is equivalent to initiating all subtasks contained in the workflow. You can customize workflows in advance to process videos as a single operation instead of repeatedly calling API operations.

The workflow mechanism has the following advantages:

* It supports high\-volume concurrent processing.

* It allows you to customize the conditions that trigger the next node.

* Sub\-nodes can perform computational reprocessing of the output of the parent node. Through multi\-step computational processing, the input video is converted into output that meets your business needs.

* It visualizes the workflow configuration and allows you to observe the progress of media processing.

* Workflows can be standardized and reused, reducing repetitive work,and standardizing business processes.

## Configuring a workflow

You can sign in to the BytePlus VOD console and enter a specific space. On the **Workflows** page, you can view all the pre\-built workflows and create custom workflows. For details, see [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow).

## Triggering a workflow

You can trigger a workflow in one of the following ways:

### Set space default workflow

Follow these steps to set a default workflow at the space level. All audio and video files uploaded to this space will be processed using the default workflow.

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. In the left navigation bar, click **System settings \> Post\-upload actions** to visit the **Post\-upload actions** page.

3. Click the **Modify** button in the **Automatic actions** section to enable the default workflow trigger.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72201859918e4a778793c67330ed6b8c~tplv-goo7wpa0wc-image.image)

4. Click the **Modify** button in the **Default settings** section to select the workflow you want to trigger from the dropdown list.

### Specify a workflow when uploading audio and video

BytePlus VOD supports specifying workflows when uploading audio and video using the console, API, and Server SDK. The specific instructions are as follows:

* Using the console: Select the workflow you want to trigger when uploading the video, as shown in the following image:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9dd69ca6db7648768ec8a333668e3218~tplv-goo7wpa0wc-image.image)

* Using API or Server SDK: When you call the [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) API, specify the workflow you want to trigger by passing the workflow ID.

### Manually trigger a workflow after uploading audio and video

BytePlus VOD supports manually triggering workflows for uploaded audio and video using the console, OpenAPI, and server\-side SDK methods. The specific instructions are as follows:

* Using the console: On the **Videos** page, select the video you want to process, then click the **Process** button in the action bar, as shown in the following image.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc0933e52ea44f4c80dbbf3aa5230589~tplv-goo7wpa0wc-image.image)

* Using API or Server SDK: Call the [StartWorkflow](https://docs.byteplus.com/docs/byteplus-vod/reference-startworkflow) API to trigger the workflow.

## Get the results of workflow execution

After triggering a workflow, you can get the results of workflow execution using the console, API/Server SDK, and event notification. The specific instructions are as follows:

* Using the console:

   * On the **Transcoding tasks** page, view the status of a specific task.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c51c2a1ce14a4e6ea65f13b3857746eb~tplv-goo7wpa0wc-image.image)

   * You can click the **View details** button to view the status and outputs of each subtask contained in the workflow.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3236b3bb9f54448a220a303ad939ff7~tplv-goo7wpa0wc-image.image)

* API/Server SDK method:

   * Call the [GetWorkflowExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getworkflowexecution) to get the workflow execution status.

   * Call the [GetWorkflowExecutionResult](https://docs.byteplus.com/docs/byteplus-vod/getworkflowexecutionresult) to get the results of workflow execution.

* Event notification: Configure the [WorkflowComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete) event. For instructions on how to configure event notifications, see [Callbacks](https://docs.byteplus.com/docs/byteplus-vod/docs-system#aed0518b).
