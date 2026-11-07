---
title: "Workflows"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-workflow"
---

A workflow is responsible for managing the tasks involved in processing your files. Generally, a workflow consists of several tasks. The BytePlus VOD transcoding service processes tasks in a workflow sequentially according to the order in which they were added. The BytePlus VOD console offers a variety of pre\-built workflow templates that you can use to process your files with ease. You can also create a customized workflow that meets your unique business needs.

<span id="517a74b9"></span>
## Pre\-built workflows

The following table lists the pre\-built workflows at your disposal, making it effortless for you to process your files.


|**Workflow name** |**Workflow ID** |**Description** |
|---|---|---|
|Single\-bitrate template for short video feeds (including H.265) |c3841b3122fd460db2bc99a6ec131cb8 |This workflow template contains six video transcoding tasks. You can use this template to transcode short video feeds. This template outputs multiple MP4 files with a fixed bitrate. The resolutions of the output files are 360p, 480p, and 540p. |
|Multi\-bitrate template for copyrighted HLS videos (including H.265) |25524a2dae4541db93b2e891d7daf4b9 |This workflow template contains six video transcoding tasks. You can use this template to encrypt long online videos for protecting digital media from unauthorized use. This template outputs multiple HLS files with different bitrates, which are suitable for playing on the Web. The resolutions of the output files are 360p, 480p, and 720p. |
|Multi\-bitrate template for general online videos (including H.265) |06853553c4d3402698a17ff5dff87fd7 |This workflow template contains six video transcoding tasks. You can use this template to transcode online videos. This template outputs multiple files with different bitrates. The resolutions of the output files are 360p, 480p, and 720p. |
|Multi\-bitrate template for short video feeds (including H.265) |1ddda0dd053c4c7488926eb2eb77eb34 |This workflow template contains eight video transcoding tasks. You can use this template to transcode short video feeds. This template is suitable for customers requiring ABR. This template outputs multiple files with different bitrates. The resolutions of the output files are 360p, 480p, 540p, and 720p. |


<span id="a9136274"></span>
## Creating a custom workflow

Follow the steps below to create a custom workflow tailored to your specific business requirements:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media processing** \> **Workflows** on the left navigation bar.

5. Click **Create workflow**.

6. Fill in the workflow name and description. It is recommended to use a workflow name that identifies the content of the template. The length of the workflow name and description should not exceed 64 characters.

7. Tick the tasks based on your business needs. The specific configurations of the ticked tasks automatically appear. Click the task tabs in turn to configure the tasks. For some tasks, you can add multiple tasks by clicking **Add task**.

   
   |**Task name** |**Multiple task support** |**Description** |
   |---|---|---|
   |Video transcoding task |Yes |See [Configuring the video transcoding or low-bitrate HD transcoding task](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#70cda070). |
   |Low\-bitrate HD transcoding task |Yes |See [Configuring the video transcoding or low-bitrate HD transcoding task](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#70cda070). |
   |Audio transcoding task |Yes |See [Configuring the audio transcoding task](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#585e6d88). |
   |Snapshot task |Yes |See [Configuring the snapshot task](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#71d17bde). |
   |Video enhancement task |No |See [Configuring the video enhancement task](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#60b905aa). |
   |Smart subtitling task |No |See [Configuring the smart subtitling task](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#8352e0a6). |
   |ABR streaming |Yes |See [Configuring the ABR streaming transcoding task](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#da6cf877). |
   |Auto publishing |No |Select the auto publishing condition.<br><br><br>* **Publish all**<br><br>* **Publish on all successful transcoding**: The output files will be automatically published after all input files have been processed.<br><br>* **Publish on any successful transcoding**: The output files will be automatically published once they have been processed. |
   

8. Click **Save**. The page automatically redirects to the **Workflows** page.


<span id="70cda070"></span>
### Configuring the video transcoding or low\-bitrate HD transcoding task


1. Select a pre\-built or custom video transcoding or low\-bitrate HD transcoding template.

2. (Optional) Set the execution condition. When enabled, the task will only be executed if the input video meets the specified condition. If no conditions are set, the task will be forcefully executed by default. You can set the following types of conditions:

   * **Resolution of input video**: Set the range for the short side of the input video.

   * **Bitrate of input video**: Set the range for the input bitrate. The custom bitrate range varies based on the resolution, as shown in the table below.

3. (Optional) Add watermark or in\-stream ad. When enabled, you need to select a watermark template from the dropdown list.

4. (Optional) Add hardcoded subtitles. Enable this option to burn subtitles permanently into video frames during transcoding.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To use this feature, you must ensure that a subtitle file for the selected language already exists and is associated with the source video. The subtitle file can be generated via a smart subtitling task or uploaded manually. For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-smart-captioning#bb1c402a">Step 1: Prepare the subtitle file</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Choose a subtitle style whose font supports the selected subtitle language and all characters in the subtitle file. If the font or subtitle file format is unsupported, subtitles may appear garbled or may not be displayed. In addition, some custom video transcoding templates may contain parameters that conflict with hardcoded subtitle settings and prevent subtitles from being displayed. Avoid using such templates with hardcoded subtitles.   </div>
   

   * **Subtitle language**: Select the language of the subtitle file you want to burn into the video. See [Supported hardcoded subtitle languages](https://docs.byteplus.com/en/docs/25/7868#hardcoded-subtitle-languages).

   * **Subtitle style:**  Select a pre\-configured **Hardcoded subtitle styling template** to define the font, size, color, and position of the subtitles. To create or manage templates, see [Subtitle templates](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-subtitle-template).

5. (Optional) Customize the file path. By default, the system generates a random file path after processing. For details, see [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path).


<span id="585e6d88"></span>
### Configuring the audio transcoding task


1. Select a pre\-built or custom audio transcoding template.

2. (Optional) Customize the file path. By default, the system generates a random file path after processing. For details, see [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path).


<span id="71d17bde"></span>
### Configuring the snapshot task


1. Select a pre\-built or custom snapshot template.

2. (Optional) Set the execution condition. When enabled, the task will only be executed if the input video meets the specified condition. You can set the input video duration.

3. (Optional) Customize the file path. By default, the system generates a random file path after processing. For details, see [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path).


<span id="60b905aa"></span>
### Configuring the video enhancement task


1. Select a custom video enhancement template.

2. (Optional) Set the execution condition. When enabled, the task will only be executed if the input video meets the specified condition. You can set the resolution of input video.

3. (Optional) Enable separate storage. When a workflow includes both transcoding and video enhancement tasks, the system will first perform the video enhancement task, followed by transcoding of the enhanced video. If you do not need to store the enhanced video separately, you can turn off the switch.

4. (Optional) Customize the file path. By default, the system generates a random file path after processing. For details, see [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path).


<span id="8352e0a6"></span>
### Configuring the smart subtitling task


1. Select a pre\-built or custom smart subtitling template.

2. (Optional) Auto subtitle publishing. When enabled, all subtitles generated by the workflow will be automatically published.


<span id="da6cf877"></span>
### Configuring the ABR streaming transcoding task


1. Select a custom ABR streaming template.

2. (Optional) Add watermark or in\-stream ad. When enabled, you need to select a watermark template from the dropdown list.

3. (Optional) Add hardcoded subtitles. Enable this option to burn subtitles permanently into video frames during transcoding.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To use this feature, you must ensure that a subtitle file for the selected language already exists and is associated with the source video. The subtitle file can be generated via a smart subtitling task or uploaded manually. For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-smart-captioning#bb1c402a">Step 1: Prepare the subtitle file</a>.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Choose a subtitle style whose font supports the selected subtitle language and all characters in the subtitle file. If the font or subtitle file format is unsupported, subtitles may appear garbled or may not be displayed.   </div>
   

   * **Subtitle language**: Select the language of the subtitle file you want to burn into the video. See [Supported hardcoded subtitle languages](https://docs.byteplus.com/en/docs/25/7868#hardcoded-subtitle-languages).

   * **Subtitle style:**  Select a pre\-configured **Hardcoded subtitle styling template** to define the font, size, color, and position of the subtitles. To create or manage templates, see [Subtitle templates](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-subtitle-template).

4. (Optional) Customize the file path. By default, the system generates a random file path after processing. For details, see [Customizing output file path](https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-output-file-path).


<span id="hardcoded-subtitle-languages"></span>
### Supported hardcoded subtitle languages

The **Subtitle language** dropdown supports the following language options.


|**Language option** |**Language code** |
|---|---|
|Mandarin Chinese (Simplified) |`cmn-Hans-CN` |
|English (United States) |`eng-US` |
|Japanese |`jpn-JP` |
|Korean |`kor-KR` |
|Vietnamese |`vie-VN` |
|Thai |`tha-TH` |
|Mandarin Chinese (Traditional) |`cmn-Hant-CN` |
|Indonesian |`ind-ID` |
|Malay |`msa-MY` |
|Filipino |`fil-PH` |
|Russian |`rus-RU` |
|Ukrainian |`ukr-UA` |
|Hindi |`hin-IN` |
|Spanish |`spa-ES` |
|Mexico \- Spanish |`spa-MX` |
|German |`deu-DE` |
|Chinese and English (bilingual) |`cmn-Hans-CN\|eng-US` |
|French |`fra-FR` |
|Portuguese |`por-PT` |
|Afrikaans |`afr-ZA` |
|Bengali (Bangladesh) |`ben-BD` |
|Bulgarian |`bul-BG` |
|Burmese |`mya-MM` |
|Czech |`ces-CZ` |
|Danish |`dan-DK` |
|Croatian |`hrv-HR` |
|Dutch |`nld-NL` |
|Finnish |`fin-FI` |
|Greek |`ell-GR` |
|Hungarian |`hun-HU` |
|Irish |`gle-IE` |
|Icelandic |`isl-IS` |
|Italian |`ita-IT` |
|Norwegian |`nor-NO` |
|Polish |`pol-PL` |
|Swedish |`swe-SE` |
|Turkish |`tur-TR` |
|Urdu |`urd-PK` |
|Arabic |`ara-SA` |
|French (Canada) |`fra-CA` |
|Hebrew (Israel) |`heb-IL` |
|Javanese (Indonesia) |`jva-ID` |
|Romanian |`ron-RO` |
|Bengali (India) |`ben-IN` |
|Khmer |`khm-KH` |
|Bosnian (Philippines) |`bos-PH` |
|Estonian |`est-EE` |
|Latvian |`lav-LV` |
|Slovak |`slk-SK` |
|Lithuanian |`lit-LT` |
|Uyghur |`uyg-CN` |


<span id="e6ad1664"></span>
## Triggering a workflow

BytePlus VOD supports triggering workflows in the following ways.

<span id="a4c2517e"></span>
### Setting default workflow at space level

Follow the steps below to set the default workflow at space level. All audio and video files uploaded to this space will be processed by the default workflow.


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter the specified space.

2. Click **System settings** \> **Post\-upload actions** on the left navigation bar.

3. Click the **Modify** button in the **Automatic actions** section and enable **Default workflow trigger**.

4. Click the **Modify** button in the **Default settings** section and select the desired workflow from the default dropdown list.


<span id="8ff04425"></span>
### Specifying the workflow during uploading

BytePlus VOD supports specifying the workflow during audio and video uploads by using the console, OpenAPI, and Server SDKs as described below:


* Use the BytePlus VOD console: Select the desired workflow during video upload on the video upload page, as shown in the image below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/527709b4fcf04087a73334da9e939e5d~tplv-goo7wpa0wc-image.image) </span>

* Use the OpenAPI or Server SDKs:

   * When calling [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo), pass the workflow ID through the upload function to specify the workflow you want to trigger.

   * When calling the [UploadMediaByUrl](https://docs.byteplus.com/docs/byteplus-vod/reference-uploadmediabyurl), pass the workflow ID through the `TemplateId` parameter to specify the workflow you want to trigger.


<span id="17ab30a5"></span>
### Manually triggering the workflow after uploading

You can manually trigger workflows for uploaded audio and video files by using the console, OpenAPI, and Server SDKs as described below:


* Use the BytePlus VOD console: On the **Videos** page, select the videos you want to process and click the **Process video** button in the action bar, as shown in the image below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/861392854a854ab1adeee9ccf5f8c16e~tplv-goo7wpa0wc-image.image) </span>

* Use the OpenAPI or Server SDKs: Call the [StartWorkflow](https://docs.byteplus.com/docs/byteplus-vod/reference-startworkflow) with the workflow ID to trigger the workflow.


<span id="e1c04cd6"></span>
## Retrieving workflow execution status and results

After triggering a workflow, you can retrieve the workflow execution status and results by using the console, OpenAPI, Server SDKs, and event notification, as explained below:


* Use the BytePlus VOD console: On the **Media processing** \> **Transcoding tasks** page, view the status of a specific workflow task. Click the **View details** button to see the status and outputs of each sub\-task within the workflow.

* Use the OpenAPI or Server SDKs: Call [GetWorkflowExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getworkflowexecution) to retrieve the workflow execution status.

* Event notification: Configure the notification for the [WorkflowComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete) event. Refer to the [Callback notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-) for detailed configuration methods.
